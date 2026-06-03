Cloud Computing & DevOps Internship Projects

Author

Aneena Liz Joseph
Cloud Computing & DevOps Internship
Maincrafts Technology

---

Project Overview

This repository contains internship tasks focused on Cloud Computing, AWS, Docker, and Web Deployment.

The projects demonstrate different approaches to hosting and deploying a portfolio website using AWS services and containerization technologies.

---

 Task 1: AWS Static Portfolio Website Hosting

Objective

Host a responsive portfolio website using Amazon S3 and Amazon CloudFront with HTTPS support.

Technologies Used

* HTML5
* CSS3
* Google Fonts
* Amazon S3
* Amazon CloudFront
* Git & GitHub

AWS Services Used

Amazon S3

* Created an S3 bucket for website hosting
* Uploaded website files
* Configured static website hosting
* Managed public access settings

Amazon CloudFront

* Created a CloudFront distribution
* Connected CloudFront with the S3 bucket
* Enabled secure website delivery using HTTPS
* Improved website performance through CDN caching

Deployment Steps

1. Developed the portfolio website using HTML and CSS.
2. Created an Amazon S3 bucket.
3. Enabled Static Website Hosting.
4. Uploaded website files.
5. Configured bucket permissions.
6. Created a CloudFront distribution.
7. Set `index.html` as the default root object.
8. Verified website accessibility through CloudFront.

Live Website

CloudFront URL:

https://deyz3n2ol0tvz.cloudfront.net

---

Task 2: Dockerized Portfolio Website Deployment on AWS EC2

Objective

Containerize a portfolio website using Docker and deploy it on an AWS EC2 instance.

Technologies Used

* HTML5
* CSS3
* Docker
* Nginx
* Git
* GitHub
* AWS EC2
* Ubuntu Linux
* SSH

Services and Tools Used

Docker

* Created a Dockerfile
* Built Docker images
* Created and managed containers
* Tested the application locally

GitHub

* Managed source code
* Version control and repository hosting

AWS EC2

* Launched Ubuntu EC2 instance
* Configured security groups
* Connected using SSH key pair authentication

Linux & Docker

* Installed Docker on EC2
* Built Docker image on the server
* Ran the application inside a Docker container

Dockerfile

```dockerfile
FROM nginx:alpine

COPY . /usr/share/nginx/html

EXPOSE 80
```

Deployment Steps

1. Developed the portfolio website using HTML and CSS.
2. Created a Dockerfile.
3. Built the Docker image locally.
4. Tested the website using Docker Desktop.
5. Uploaded the project to GitHub.
6. Launched an AWS EC2 Ubuntu instance.
7. Connected to the server using SSH.
8. Installed Docker on EC2.
9. Cloned the GitHub repository.
10. Built the Docker image on EC2.
11. Ran the Docker container.
12. Verified website accessibility through the EC2 public IP.

Live Website

EC2 Public URL:

http://43.204.216.226

---

Project Structure

```text
portfolio-site/
│
├── index.html
├── styles.css
├── Dockerfile
└── README.md
```

---

Learning Outcomes

Through these projects, I gained practical experience in:

* Static Website Hosting
* Amazon S3
* Amazon CloudFront
* Docker Containerization
* AWS EC2 Management
* Linux Server Administration
* SSH Connectivity
* Git & GitHub
* Cloud Deployment Workflows
* DevOps Fundamentals

---

Future Enhancements

* Custom Domain Integration
* SSL Certificate Management
* CI/CD Pipeline using GitHub Actions
* Infrastructure as Code (IaC)
* Advanced AWS Services Integration

---

Acknowledgement

This project was completed as part of the Cloud Computing & DevOps Internship Program at Maincrafts Technology.
