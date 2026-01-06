# DevOps Capstone Project – CI/CD Pipeline using Jenkins & Docker

##  Project Overview
This project demonstrates a complete **CI/CD (Continuous Integration and Continuous Deployment)** pipeline using **Jenkins**, **Docker**, and **Docker Compose**.  
The pipeline automatically builds Docker images, pushes them to Docker Hub, and deploys the application after every successful code change.

---

##  Tools & Technologies Used
- **Git & GitHub** – Source code management  
- **Jenkins** – CI/CD automation  
- **Docker** – Containerization  
- **Docker Hub** – Docker image registry  
- **Docker Compose** – Application deployment  
- **Flask** – Backend service  
- **Nginx** – Frontend service  

---

##  Application Architecture
The application consists of two main services:

- **Backend**
  - Flask-based API
  - Exposes `/` and `/health` endpoints
- **Frontend**
  - Nginx-based web application

Both services are containerized and managed using Docker Compose.

---

##  CI/CD Workflow

Code Push (GitHub)
↓
Jenkins CI Pipeline
↓
Build Docker Images
↓
Push Images to Docker Hub
↓
Pull Images from Docker Hub
↓
Deploy using Docker Compose
↓
Health Check Verification


---

##  Continuous Integration (CI)
CI is implemented using **Jenkins**.  
Whenever code is pushed to GitHub, Jenkins performs the following steps:

1. Clone the GitHub repository  
2. Build Docker images for backend and frontend  
3. Run containers for basic validation  
4. Push Docker images to Docker Hub  

This ensures the application is always in a buildable and testable state.

---

##  Continuous Deployment (CD)
CD starts after a successful CI build.

Deployment is done using **Docker Compose** with images pulled from Docker Hub.

### CD Steps:
1. Pull latest Docker images from Docker Hub  
2. Start containers using `docker-compose.deploy.yml`  
3. Deploy backend and frontend services automatically  
4. Verify deployment using health check  

---

##  Health Check
The backend exposes a `/health` endpoint.

Example:
http://localhost:5000/health


Jenkins uses this endpoint to confirm that the deployment was successful.

---

##  Important Files
- `Jenkinsfile` – Defines CI/CD pipeline stages  
- `docker-compose.yml` – Used for CI and local builds  
- `docker-compose.deploy.yml` – Used for CD deployment  
- `backend/app.py` – Backend application with health endpoint  

---

##  Project Outcome
- Automated CI pipeline using Jenkins  
- Docker images stored in Docker Hub  
- Automated CD using Docker Compose  
- Application deployed without manual intervention  
- Health checks ensure deployment reliability  

---

##  Conclusion
This project demonstrates real-world DevOps practices by implementing a complete CI/CD pipeline.  
It highlights how automation improves deployment speed, consistency, and reliability using Jenkins and Docker.

---

##  Author
Nivas Voruganti  
DevOps Capstone Project
