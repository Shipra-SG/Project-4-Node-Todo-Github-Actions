# Node.js Todo Application - CI/CD with GitLab, Docker & AWS EC2
---

## Project Overview
This project demonstrates how to build and deploy a Node.js Todo application using a **complete CI/CD pipeline** with **GitLab CI/CD**, **Docker**, and **AWS EC2**.

The goal of this project was to automate the entire software delivery process — from code commit to production deployment — following real-world DevOps practices.

---

## Project Objectives
- Automate build, test, and deployment using GitLab CI/CD
- Containerize the application using Docker
- Deploy the application automatically on AWS EC2
- Secure sensitive information using CI/CD variables
- Gain hands-on experience with DevOps tools

---

## Tech Stack Used
- **Application:** Node.js, Express.js
- **Containerization:** Docker
- **CI/CD Tool:** GitLab CI/CD
- **Cloud Platform:** AWS EC2 (Ubuntu)
- **Container Registry:** Docker Hub
- **OS:** Linux (Ubuntu)

---

## Project Structure
```
node-todo-cicd/
│ ├── views/
│ └── app.js
├── Dockerfile
├── package.json
├── package-lock.json
├── .gitlab-ci.yml
├── .gitignore
└── README.md
```

---

## STEP-BY-STEP PROJECT IMPLEMENTATION

---

## STEP 1: Clone the Application Repository
The base Node.js Todo application was cloned from GitLab:

```bash
git clone https://gitlab.com/twsdevops1/node-todo-cicd.git
cd node-todo-cicd
```

---

## STEP 2: AWS EC2 Setup

Created an Ubuntu EC2 instance
```
sudo apt-get update
sudo apt-get install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
newgrp docker
```

Allowed port 8000 in the security group
Configured SSH access for deployment

---

## STEP 3: Run Application Locally
Installed dependencies and verified the application locally:
```
npm install
npm start
```

Tests were executed using:
```
npm test
```

---

## STEP 4: Create Dockerfile
A Dockerfile was created to containerize the Node.js application.

Key actions performed:
> Used Node base image
> Copied application files
> Installed dependencies
> Ran tests inside Docker image
> Exposed application port

This ensured consistency across environments.

---

## STEP 5: Build & Test Docker Image Locally
```
docker build -t node-todo-app .
docker run -p 8000:8000 node-todo-app
```

Verified that the application works inside the container.

---

## STEP 6: Create Docker Hub Repository
A Docker Hub repository was created:
```
<docker-username>/node-todo-cicd
```

This repository stores Docker images built by the CI/CD pipeline.

---

## STEP 7: Configure GitLab CI/CD Variables
Sensitive data was securely stored using GitLab CI/CD Variables:

Variable Name	Description:
```
1) Key: DOCKER_USERNAME	, Value: Docker Hub username 
2) Key: DOCKER_PASSWORD, Value: Docker Hub password/Token
3) Key: EC2_HOST , Value: Public IP of EC2 instance
4) Key: EC2_KEY, Value: Private SSH key- .pem file (masked & protected)
```
✔ No secrets were hardcoded in the repository.

---

## STEP 8: Create GitLab CI/CD Pipeline
A .gitlab-ci.yml file was created with three stages:

🔄 Pipeline Stages

Build – Build Docker image

Push – Push image to Docker Hub

Deploy – Deploy container to AWS EC2

Pipeline automatically triggers on every push to the main branch.

---

## STEP 9: Automatic Deployment to EC2
The deploy stage performs the following actions:

> Pulls the latest Docker image from Docker Hub
> Stops old container (if running)
> Starts a new container with updated image
> Deployment happens automatically via SSH.

---

## Application Access
Once deployed, the application is accessible at:
```
http://<EC2_PUBLIC_IP>:8000
```

---

## Security Best Practices Followed

> CI/CD secrets stored as masked variables
> No credentials pushed to GitHub
> .gitignore used to exclude sensitive files
> SSH key permissions restricted

---

## Key Learnings
End-to-end CI/CD automation
Docker image lifecycle management
Secure deployment using SSH
Real-world GitLab CI/CD usage
Cloud deployment on AWS EC2

---

👩‍💻 Author
Shipra
Aspiring DevOps / Cloud Engineer

---

# Future Enhancements

Add GitHub Actions pipeline
Deploy using Kubernetes
Add monitoring with Prometheus & Grafana
Enable HTTPS with Nginx & SSL
