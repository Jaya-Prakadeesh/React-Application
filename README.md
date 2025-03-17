Application Development - React

Introduction

This document outlines the implementation of a DevOps pipeline designed for deploying a React-based web application. The process involves automation through CI/CD, containerization, and system monitoring to ensure reliability and security.

Key Components

Infrastructure & Hosting

The application is hosted on an AWS EC2 instance.

Security measures include restricted access through Security Groups.

Deployment & Automation

The application runs on port 800.

Docker is used for containerization.

Docker Compose manages multiple containers.

Jenkins facilitates CI/CD automation.

Version Control & Repository Management

Git & GitHub provide version control.

A structured branching strategy is implemented.

Docker images are stored in Docker Hub with separate repositories for development and production.

Monitoring & Alert System

Integrated open-source monitoring tools ensure application uptime.

Alerts notify administrators in case of application failures.

Step-by-Step Implementation

1. Setting Up the Application

The source code is obtained using:

git clone https://github.com/sriram-R-krishnan/devops-build.git

The application is configured to run on port 800.

2. Containerization Process

A Dockerfile is created for application containerization.

A docker-compose.yml file is configured to manage multiple containers.

3. Automation Scripts

build.sh handles Docker image creation.

deploy.sh is responsible for deployment to the server.

4. CI/CD Pipeline Execution

Jenkins is set up to:

Trigger builds based on commits to dev and master branches.

Push Docker images to development (public) and production (private) repositories.

5. Security & Access Control

A t2.micro EC2 instance is launched.

Security groups are configured:

Application access: Open to all users.

Server login: Restricted to a predefined IP address.

6. System Monitoring

Monitoring tools track application health and performance.

Alerts are configured for real-time issue detection.

Challenges & Solutions

Handling Prebuilt Artifacts

Since build artifacts were included in the repository, recompilation was unnecessary.

The application was deployed by relocating artifacts to the Nginx directory.

Managing Storage Limitations

To avoid storage issues, the following measures were implemented:

Proper storage planning based on software dependencies.

Removal of unused Docker images.

Cleanup of stopped containers.

Branch-Based Deployment

A system was implemented to:

Deploy changes from dev to the development Docker Hub repository.

Merge dev into master to push images to the production repository.

Securing DockerHub Credentials

To prevent exposure of credentials, DockerHub authentication details were stored securely within Jenkins credentials instead of being hardcoded in the repository.

Enhancements & Additional Features

SonarQube integration can be implemented for static code analysis.

Enhanced monitoring solutions can be integrated for better system insights.

Repository Overview

Main Branch: Contains project configuration and commands.

Dev Branch: Maintains files specific to development testing.

Technologies Used

Containerization: Docker, Docker Compose

CI/CD Tools: Jenkins, GitHub Actions

Cloud Platform: AWS EC2

Monitoring: Grafana

Version Control: Git & GitHub

Automation: Bash Scripting

Contributor: Jayaprakadeesh P G