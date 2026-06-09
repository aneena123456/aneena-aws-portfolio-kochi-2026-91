Cloud Computing & DevOps Internship Projects

Author

Aneena Liz Joseph
Cloud Computing & DevOps Internship
Maincrafts Technology

---

Project Overview

This repository contains internship tasks focused on Cloud Computing, AWS, Docker, and CI/CD Automation.

The projects demonstrate different approaches to hosting, deploying, containerizing, and automating the deployment of a portfolio website using AWS services, Docker, and GitHub Actions.

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
7. Set index.html as the default root object.
8. Verified website accessibility through CloudFront.

Live Website

CloudFront URL

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

EC2 Public URL

http://43.204.216.226

---

Task 3: CI/CD Automation for Dockerized Applications Using GitHub Actions

Objective

Automate Docker image building and deployment using GitHub Actions and Docker Hub.

Technologies Used

* GitHub Actions
* Docker
* Docker Hub
* GitHub
* YAML
* CI/CD Pipeline

Services and Tools Used

GitHub Actions

* Automated workflow execution on every push
* Continuous Integration and Deployment
* Workflow monitoring and logging

Docker Hub

* Docker image repository
* Automated image publishing

GitHub Secrets

* Secure storage of credentials
* Protected sensitive information during workflow execution

Workflow Process

1. Developer pushes code to GitHub.
2. GitHub Actions workflow starts automatically.
3. Repository code is checked out.
4. Docker image is built.
5. Docker Hub login is performed using GitHub Secrets.
6. Docker image is pushed to Docker Hub.
7. Workflow logs are generated for monitoring.

Workflow File

```text
.github/workflows/docker-ci.yml
```

CI/CD Features

* Automated Docker image build
* Automated Docker image push
* Secure credential management
* Continuous Integration
* Pipeline monitoring
* Automated deployment workflow

Workflow Status

Successfully executed GitHub Actions CI/CD Pipeline.

* Status: Success
* Triggered via Git Push
* Docker Image Built Successfully
* Docker Image Pushed Successfully

---

Project Structure

```text
portfolio-site/
│
├── index.html
├── styles.css
├── Dockerfile
├── .github/
│   └── workflows/
│       └── docker-ci.yml
└── README.md
```

---

Learning Outcomes

Through these internship tasks, I gained practical experience in:

* Static Website Hosting
* Amazon S3
* Amazon CloudFront
* Docker Containerization
* AWS EC2 Management
* Linux Server Administration
* SSH Connectivity
* Git & GitHub
* GitHub Actions
* CI/CD Pipeline Automation
* Docker Hub Integration
* Secure Secrets Management
* Cloud Deployment Workflows
* DevOps Fundamentals

---

Future Enhancements

* Custom Domain Integration
* SSL Certificate Management
* Infrastructure as Code (IaC)
* Advanced AWS Services Integration
* Kubernetes Deployment
* Automated Cloud Deployments

---

Acknowledgement

This project was completed as part of the **Cloud Computing & DevOps Internship Program at Maincrafts Technology.

Special thanks to Maincrafts Technology for providing practical exposure to AWS Cloud, Docker, DevOps practices, and CI/CD automation.
