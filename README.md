# 🚀 DevOps Project 2 — Dockerized Web Application on AWS EC2

## 📌 Project Overview

This project demonstrates how to deploy a static website using Docker on an AWS EC2 instance.

It focuses on containerization and server-level deployment using CLI.

---

## 🏗️ Architecture

User → Browser → EC2 Instance → Docker → Nginx Container → Static Website

---

## ⚙️ Technologies Used

* AWS EC2
* Ubuntu Linux
* Docker
* Nginx (inside container)
* SSH

---

## 🪜 Step-by-Step Implementation

### 1️⃣ Launch EC2 Instance

* Created Ubuntu EC2 instance (t2.micro)
* Configured Security Group:

  * Port 22 (SSH)
  * Port 80 (HTTP)

---

### 2️⃣ Connect via SSH

```bash
ssh -i your-key.pem ubuntu@your-ec2-ip
```

---

### 3️⃣ Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
```

Re-login to apply changes.

---

### 4️⃣ Transfer Application Files

```bash
scp -i your-key.pem index.html ubuntu@your-ec2-ip:~
```

---

### 5️⃣ Create Application Directory

```bash
mkdir app
mv index.html app
cd app
```

---

### 6️⃣ Create Dockerfile

```Dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
```

---

### 7️⃣ Build Docker Image

```bash
docker build -t my-app .
```

---

### 8️⃣ Run Docker Container

```bash
docker run -d -p 80:80 --name my-app my-app
```

---

### ⚠️ Issues Faced & Fixes

#### ❌ Port 80 already in use

* Cause: Nginx was already running
* Fix:

```bash
sudo systemctl stop nginx
```

---

#### ❌ Container name already in use

* Cause: Existing container with same name
* Fix:

```bash
docker rm -f my-app
```

---

## 🌐 Output

Application successfully deployed and accessible via:
http://75.101.223.47/

---

## 📸 Screenshots

### 🔹 SSH Connection

<img width="1262" height="315" alt="image" src="https://github.com/user-attachments/assets/d6cab13f-134a-44fb-9720-9a328fe60045" />


### 🔹 Docker Running Container

<img width="1897" height="727" alt="image" src="https://github.com/user-attachments/assets/75e1d815-4d93-4e50-a141-5db2facce401" />


### 🔹 Website Output

<img width="1918" height="671" alt="image" src="https://github.com/user-attachments/assets/50d4fdc2-0a36-4ed8-afb6-4e433fb6a32b" />


---

## 🧠 Key Learnings

* Installed Docker on EC2 using CLI
* Built and ran Docker containers
* Resolved port conflicts and container issues
* Deployed application using containerization

---

## 💬 Interview Explanation

"I installed Docker on an EC2 instance, containerized a static application using a Dockerfile, and deployed it by running a container mapped to port 80. I also handled real-world issues like port conflicts and container name conflicts."

---

## 🔮 Future Improvements

* Add CI/CD using GitHub Actions
* Use Docker Compose
* Implement reverse proxy (Nginx + Docker)
