# Node.js Todo Application using Docker

A simple Node.js Todo application containerized using Docker and deployed on an AWS EC2 Ubuntu instance.

---

# Project Overview

This project demonstrates how to:

* Launch an AWS EC2 Ubuntu instance
* Connect to the EC2 instance using SSH
* Install Docker on Ubuntu
* Clone the project from GitHub
* Build a Docker image
* Install Node.js dependencies inside the Docker image
* Run automated tests during the Docker build process
* Run the Node.js application inside a Docker container
* Configure the EC2 Security Group
* Access the application through a web browser
* Push the project to GitHub

---

# Tech Stack

* Node.js
* Express.js
* Docker
* Ubuntu 22.04
* AWS EC2
* Git
* GitHub
* Mocha (Testing)

---

# Project Structure

```text
node-todo/
├── app.js
├── package.json
├── package-lock.json
├── Dockerfile
├── README.md
├── routes/
├── public/
├── views/
└── test/
```

---

# Step 1: Launch an EC2 Instance

* Launch an Ubuntu EC2 instance.
* Select the **t2.micro** instance type.
* Create or select an existing Key Pair.
* Allow **SSH (Port 22)** in the Security Group.
* Launch the instance.

---

# Step 2: Connect to the EC2 Instance

```bash
chmod 400 my-key.pem
```

```bash
ssh -i my-key.pem ubuntu@<EC2-PUBLIC-IP>
```

---

# Step 3: Update Ubuntu

```bash
sudo apt update
sudo apt upgrade -y
```

---

# Step 4: Install Docker

```bash
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl start docker
```

Enable Docker:

```bash
sudo systemctl enable docker
```

Verify Docker installation:

```bash
docker --version
```

Check Docker status:

```bash
sudo systemctl status docker
```

---

# Step 5: Clone the Repository

```bash
git clone https://github.com/<username>/<repository-name>.git
```

```bash
cd node-todo
```

---

# Step 6: Dockerfile

```dockerfile
FROM node:12.2.0-alpine

WORKDIR /node

COPY . .

RUN npm install

RUN npm run test

EXPOSE 8000

CMD ["node","app.js"]
```

---

# Step 7: Build the Docker Image

```bash
sudo docker build -t node-app .
```

Verify the image:

```bash
sudo docker images
```

---

# Step 8: Run the Docker Container

If the application runs on **port 8000**, use:

```bash
sudo docker run -d --name node-container -p 8000:8000 node-app
```

If you want to access it using **port 80** from the browser:

```bash
sudo docker run -d --name node-container -p 80:8000 node-app
```

Verify the running container:

```bash
sudo docker ps
```

View logs:

```bash
sudo docker logs node-container
```

---

# Step 9: Configure the EC2 Security Group

Depending on the port mapping, configure the Security Group.

### If using Host Port 80

Add the following inbound rule:

| Type | Protocol | Port | Source               |
| ---- | -------- | ---- | -------------------- |
| HTTP | TCP      | 80   | Anywhere (0.0.0.0/0) |

### If using Host Port 8000

Add the following inbound rule:

| Type       | Protocol | Port | Source               |
| ---------- | -------- | ---- | -------------------- |
| Custom TCP | TCP      | 8000 | Anywhere (0.0.0.0/0) |

Save the changes.

---

# Step 10: Access the Application

If mapped to port **80**:

```text
http://<EC2-PUBLIC-IP>
```

If mapped to port **8000**:

```text
http://<EC2-PUBLIC-IP>:8000
```

---

# Useful Docker Commands

### Build Image

```bash
sudo docker build -t node-app .
```

### Run Container

```bash
sudo docker run -d --name node-container -p 8000:8000 node-app
```

### List Images

```bash
sudo docker images
```

### List Running Containers

```bash
sudo docker ps
```

### List All Containers

```bash
sudo docker ps -a
```

### View Logs

```bash
sudo docker logs <container-id>
```

### Stop Container

```bash
sudo docker stop <container-id>
```

### Remove Container

```bash
sudo docker rm <container-id>
```

### Remove Image

```bash
sudo docker rmi <image-id>
```

---

# Git Commands

### Initialize Repository

```bash
git init
```

### Check Status

```bash
git status
```

### Add Files

```bash
git add .
```

### Commit Changes

```bash
git commit -m "Initial commit"
```

### Rename Branch

```bash
git branch -M main
```

### Add Remote Repository

```bash
git remote add origin https://github.com/<username>/<repository-name>.git
```

### Check Remote

```bash
git remote -v
```

### Update Existing Remote

```bash
git remote set-url origin https://github.com/<username>/<repository-name>.git
```

### Push to GitHub

```bash
git push -u origin main
```

### Push Future Changes

```bash
git push
```

---

# Troubleshooting

## Remote Already Exists

```bash
git remote -v
```

```bash
git remote set-url origin https://github.com/<username>/<repository-name>.git
```

---

## Permission Denied (403)

This happens when the repository points to someone else's GitHub repository.

Update the remote URL:

```bash
git remote set-url origin https://github.com/<username>/<repository-name>.git
```

Then push again:

```bash
git push -u origin main
```

---

## Application Not Accessible

Check the following:

* Docker container is running.
* The application is listening on port **8000**.
* Docker port mapping is correct.
* EC2 Security Group allows the required port.
* The correct EC2 Public IP is being used.

---

# Learning Outcomes

After completing this project, you will understand:

* Dockerizing a Node.js application
* Installing dependencies inside Docker
* Running automated tests during image build
* Building Docker images
* Running Docker containers
* Port mapping in Docker
* Configuring AWS EC2 Security Groups
* Deploying applications on AWS EC2
* Managing Git and GitHub repositories

---

# Author

**OM**
