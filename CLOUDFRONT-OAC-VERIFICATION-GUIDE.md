# AWS S3 + CloudFront with OAC - Verification Guide

## Correct S3 Bucket Policy for CloudFront OAC

Your S3 bucket policy should allow CloudFront to access objects while keeping the bucket private.

### Key Components to Verify

#### 1. **Principal**
```json
"Principal": {
  "Service": "cloudfront.amazonaws.com"
}
```
- Allows CloudFront service to assume this permission
- This is the correct principal for CloudFront distributions

#### 2. **Action**
```json
"Action": "s3:GetObject"
```
- Allows CloudFront to **read** objects from S3
- This is the only action CloudFront needs
- Do NOT include `s3:ListBucket` - CloudFront doesn't need it with OAC

#### 3. **Resource**
```json
"Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
```
- Replace `YOUR_BUCKET_NAME` with your actual S3 bucket name
- The `/*` ensures the policy applies to all objects in the bucket
- Use `arn:aws:s3:::YOUR_BUCKET_NAME/*` (NOT the bucket ARN without /*) for GetObject

#### 4. **Condition (Critical for OAC)**
```json
"Condition": {
  "StringEquals": {
    "AWS:SourceArn": "arn:aws:cloudfront::YOUR_AWS_ACCOUNT_ID:distribution/YOUR_DISTRIBUTION_ID"
  }
}
```
- Replace `YOUR_AWS_ACCOUNT_ID` with your AWS Account ID (12 digits)
- Replace `YOUR_DISTRIBUTION_ID` with your CloudFront Distribution ID (e.g., `E1234ABCD5F6G7`)
- This condition ensures **only your CloudFront distribution** can access the bucket
- This is the security benefit of OAC - it's more restrictive than older Origin Access Identity (OAI)

---

## Verification Checklist

### ✅ Before Applying the Policy

1. **Verify CloudFront Distribution ARN format:**
   ```
   arn:aws:cloudfront::YOUR_AWS_ACCOUNT_ID:distribution/YOUR_DISTRIBUTION_ID
   ```
   - Find this in CloudFront console → Select distribution → General tab
   - Distribution ID is shown as: `E1234ABCD5F6G7`

2. **Verify S3 Bucket Name:**
   - Go to S3 console and confirm the exact bucket name (case-sensitive)
   - Example: `my-portfolio-site-bucket`

3. **Verify S3 Bucket is Private:**
   - S3 console → Select bucket → Permissions tab
   - Ensure "Block all public access" is enabled
   - No bucket policy should allow public access

### ✅ After Applying the Policy

1. **Verify Policy is Attached:**
   ```
   AWS Console → S3 → Your Bucket → Permissions → Bucket Policy
   ```
   - Policy should show only CloudFront (no public access principals)
   - Status should show "Policy is public" only if incorrectly configured

2. **Test CloudFront Access:**
   - Go to your CloudFront distribution URL: `https://d123456789.cloudfront.net/index.html`
   - If you see your website → ✅ Policy is correct
   - If you get 403 Access Denied → ❌ Policy needs fixing

3. **Check S3 Error Logs:**
   ```
   AWS Console → S3 → Your Bucket → Properties → Server access logging
   ```
   - Look for 403 errors from CloudFront's IP range
   - If present after policy update, wait a few minutes for policy to take effect

4. **Verify OAC is Associated:**
   - CloudFront console → Select distribution → Origins tab
   - Verify your S3 origin shows OAC association
   - If showing blank or "Origin Access Identity", it's using old OAI (not OAC)

---

## Common Issues & Solutions

### Issue: 403 Access Denied when accessing CloudFront URL

**Possible causes:**
1. Policy not yet propagated (wait 1-2 minutes)
2. Wrong Distribution ID in condition
3. Wrong AWS Account ID in condition
4. Typo in S3 bucket name
5. S3 bucket policy not saved/applied

**Fix:**
- Double-check all values in the condition block
- Redeploy policy and wait 2 minutes
- Test with `aws s3 cp s3://your-bucket/index.html .` to verify S3 permissions separately

### Issue: CloudFront distribution shows "No Origins" or OAC not applying

**Possible causes:**
1. OAC created but not associated to origin
2. Origin still using public S3 website endpoint instead of REST endpoint

**Fix:**
- CloudFront console → Edit distribution
- Check Origins section → Verify:
  - Origin domain: `your-bucket.s3.amazonaws.com` (NOT `your-bucket.s3-website-region.amazonaws.com`)
  - Origin Access Control: Shows your OAC name
  - Click "Update Origin Policy" button to auto-update S3 bucket policy

### Issue: Policy shows IAM principals or allows public access

**Problem:**
```json
"Principal": "*"  // ❌ WRONG - allows anyone
"Principal": {
  "AWS": "arn:aws:iam::ACCOUNT:root"  // ❌ Wrong for CloudFront
}
```

**Solution:**
- Use only `"Principal": {"Service": "cloudfront.amazonaws.com"}`
- Use the Condition block to restrict to your specific distribution

---

## Minimum Policy (Correct Configuration)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontOACAccess",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-portfolio-bucket/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::123456789012:distribution/E1234ABCD5F6G7"
        }
      }
    }
  ]
}
```

Replace:
- `my-portfolio-bucket` → your S3 bucket name
- `123456789012` → your AWS Account ID
- `E1234ABCD5F6G7` → your CloudFront Distribution ID

---

## Additional Security Best Practices

1. **Bucket versioning** (optional but recommended):
   - Enables rollback if needed
   - S3 console → Bucket → Versioning → Enable

2. **Enable S3 Block Public Access:**
   - S3 console → Account settings → Block Public Access → Enable all
   - Prevents accidental public exposure

3. **CloudFront Origin Shield** (optional):
   - Adds caching layer between CloudFront and S3
   - Reduces S3 requests and costs
   - CloudFront console → Edit distribution → Origins → Enable Origin Shield

4. **Logging** (optional but recommended):
   - CloudFront: CloudFront console → Logs
   - S3: S3 console → Properties → Server access logging
   - Monitor for access patterns and issues

---

## How to Apply the Policy

### Via AWS Console

1. Go to S3 console → Select your bucket → Permissions tab
2. Click "Bucket Policy" button
3. Paste your policy JSON (with values replaced)
4. Click "Save"

### Via AWS CLI

```bash
aws s3api put-bucket-policy \
  --bucket my-portfolio-bucket \
  --policy file://S3-BUCKET-POLICY.json
```

### Via CloudFront Console (Auto-Update)

1. CloudFront console → Select distribution → Edit
2. Go to Origins section
3. Select your S3 origin
4. Verify Origin domain and OAC are set
5. Click "Update Origin Policy" button
6. CloudFront will automatically update your S3 bucket policy

---

## Verification Commands (AWS CLI)

### Check current bucket policy:
```bash
aws s3api get-bucket-policy \
  --bucket my-portfolio-bucket \
  --query 'Policy' \
  --output text | jq .
```

### Check bucket is private:
```bash
aws s3api get-bucket-acl --bucket my-portfolio-bucket
```
(Should show only your account as owner)

### Check CloudFront distribution:
```bash
aws cloudfront get-distribution --id E1234ABCD5F6G7
```

### Test object access via CloudFront URL:
```bash
curl -I https://d123456789.cloudfront.net/index.html
```
(Should return 200 or 304, not 403)
