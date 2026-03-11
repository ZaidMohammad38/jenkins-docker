🚀 Jenkins + Docker + Ansible CI/CD Pipeline

This project demonstrates a simple DevOps CI/CD pipeline where Jenkins builds a Docker image, pushes it to Docker Hub, and Ansible deploys it to a remote server running Docker.

The pipeline automatically builds and deploys a static web application using Nginx.

🏗 Architecture

Developer
   │
   ▼
GitHub Repository
   │
   ▼
Jenkins Server (CI)
   │
   ├── Build Docker Image
   ├── Push Image to Docker Hub
   │
   ▼
Ansible (CD)
   │
   ▼
Worker Server
   │
   ▼
Docker Container (Nginx Web App)

⚙️ Technologies Used

Jenkins – Continuous Integration

Docker – Containerization

Ansible – Configuration Management & Deployment

GitHub – Source Code Repository

Nginx – Web Server

📁 Project Structure
jenkins-docker/
│
├── Jenkinsfile
├── Dockerfile
├── inventory
├── playbook.yml
│
└── src/
     └── index.html

     
🔧 Jenkins Pipeline Stages
1️⃣ Clone Repository

Jenkins pulls the source code from GitHub.

git clone repository
2️⃣ Build Docker Image

Jenkins builds a Docker image using the Dockerfile.


3️⃣ Push Image to Docker Hub

The Docker image is pushed to Docker Hub.

docker push <dockerhub-username>/static-web
4️⃣ Deploy using Ansible

Jenkins triggers an Ansible playbook which connects to the worker server via SSH and deploys the container.


📜 Ansible Playbook

The playbook performs the following steps on the worker node:

Pull latest Docker image

Stop existing container

Run new container


🌐 Application Access

After deployment the application is available at:

http://<worker-public-ip>:8085

Example:

http://3.x.x.x:8085
🔐 SSH Setup

Jenkins connects to the worker node using SSH key authentication.

Steps:

Generate SSH key on Jenkins server

Copy public key to worker server

ssh-copy-id ansible@worker-ip

This allows passwordless login.

▶️ How to Run

1️⃣ Push code to GitHub
2️⃣ Trigger Jenkins pipeline
3️⃣ Jenkins builds Docker image
4️⃣ Jenkins pushes image to Docker Hub
5️⃣ Jenkins runs Ansible playbook
6️⃣ Worker node deploys container


🎯 Outcome

✔ Automated CI/CD pipeline
✔ Docker image build and push
✔ Automated deployment using Ansible
✔ Application deployed on remote server


stage view:
<img width="1178" height="811" alt="image" src="https://github.com/user-attachments/assets/661350ce-2c01-4194-99b2-77c788f054b8" />

deployed application:
<img width="1917" height="931" alt="image" src="https://github.com/user-attachments/assets/cb7b9cf4-5aae-482e-a095-e3d3bd8579ca" />
