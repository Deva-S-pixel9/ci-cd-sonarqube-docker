# CI/CD Pipeline with Jenkins, SonarQube & Docker

This project demonstrates an end-to-end **CI/CD pipeline** that automates code quality checks, containerization, and deployment of a web application using **Jenkins, SonarQube, Docker, and AWS EC2**.

---

## 🚀 Project Overview

The goal of this project is to create a fully automated workflow where every code push triggers:

- Build and test the Python app
- Static code analysis using SonarQube
- Docker image creation
- Push Docker image to Docker Hub
- Deploy the container on an AWS EC2 instance

The application runs inside a **Docker container** and is accessible via **EC2 public IP on port 5000**.

---

## 🛠️ Tech Stack

- **Version Control:** Git, GitHub  
- **CI/CD:** Jenkins, GitHub Webhook  
- **Code Quality:** SonarQube  
- **Containerization:** Docker  
- **Image Registry:** Docker Hub  
- **Cloud:** AWS EC2  
- **OS:** Ubuntu Linux  
- **Language:** Python 3  

---

## 🔁 CI/CD Pipeline Flow

1. Developer pushes code to GitHub  
2. GitHub Webhook triggers Jenkins pipeline  
3. Jenkins stages:
   - Checkout source code
   - Install dependencies and run `pytest` for tests
   - Perform SonarQube code analysis
   - Build Docker image
   - Push image to Docker Hub
4. Jenkins deploys the latest Docker container on AWS EC2  
5. Application is accessible via EC2 public IP over port **5000**

---

## 🧱 Architecture Diagram (ASCII)


Developer
   |
   | git push
   v
GitHub
   |
   | Webhook triggers
   v
Jenkins
   |
   | Checkout Code
   | Build & Test
   | SonarQube Analysis
   | Docker Build
   v
DockerHub
   |
   | Pull latest image
   v
EC2 (Docker Container running Python app)
   |
   | http : 5000
   v
User Browser


📂 Project Structure

.
├── app.py                   # Your main Python application
├── requirements.txt         # Python dependencies
├── Dockerfile               # Docker instructions to build image
├── Jenkinsfile              # CI/CD pipeline configuration
├── sonar-project.properties # SonarQube configuration
├── test_app.py              # Python test script
└── README.md                # Project documentation

---

## 🧪 Testing

- Python tests are run using `pytest`  
- Ensures code correctness before building Docker image  

---

## 📊 Code Quality

- SonarQube performs static code analysis  
- Pipeline fails if the Quality Gate is not met  
- Ensures minimal bugs, vulnerabilities, and code smells  

---

## 🐳 Docker & Deployment

- Docker image is built in Jenkins  
- Image is pushed to Docker Hub  
- Jenkins pulls the latest image on EC2  
- Existing container is stopped and removed  
- New container is run to reflect the latest changes  

---

## 🌐 Application Access

http://<EC2_PUBLIC_IP>:5000

## ✅ Key Outcomes

- Fully automated CI/CD pipeline for Python applications  
- Improved code quality with SonarQube quality gates  
- Zero manual deployment steps  
- Consistent and repeatable deployments  
- Real-world DevOps workflow implementation

