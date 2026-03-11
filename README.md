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

docker build -t <dockerhub-username>/static-web .
3️⃣ Push Image to Docker Hub

The Docker image is pushed to Docker Hub.

docker push <dockerhub-username>/static-web
4️⃣ Deploy using Ansible

Jenkins triggers an Ansible playbook which connects to the worker server via SSH and deploys the container.

ansible-playbook -i inventory playbook.yml
📜 Ansible Playbook

The playbook performs the following steps on the worker node:

Pull latest Docker image

Stop existing container

Run new container

---
- name: docker operation using jenkins
  hosts: dev
  user: ansible
  become: true
  connection: ssh

  tasks:

  - name: Pull latest image
    command: docker pull zaidmohammad038/static-web

  - name: Stop existing container
    command: docker rm -f webapp
    ignore_errors: yes

  - name: Run container
    command: docker run -d -p 8085:80 --name webapp zaidmohammad038/static-web
📦 Dockerfile
FROM nginx:latest
COPY src/ /usr/share/nginx/html
EXPOSE 80

This image runs a static website using Nginx.

🖥 Inventory File
[dev]
172.31.0.136 ansible_user=ansible ansible_ssh_private_key_file=/var/lib/jenkins/.ssh/id_ed25519

This allows Ansible to SSH into the worker node.

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

stage view:
<img width="1178" height="811" alt="image" src="https://github.com/user-attachments/assets/661350ce-2c01-4194-99b2-77c788f054b8" />

🎯 Outcome

✔ Automated CI/CD pipeline
✔ Docker image build and push
✔ Automated deployment using Ansible
✔ Application deployed on remote server
