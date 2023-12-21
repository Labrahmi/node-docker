# Node.js and Docker Quick Start Guide

![alt text](https://blog.codewithdan.com/wp-content/uploads/2023/06/Docker-Logo.png)


Welcome to the Node.js and Docker Quick Start Guide! This guide will walk you through the process of setting up a basic Node.js application using Docker on an Ubuntu system. If you're new to Docker or want a quick refresher, follow the steps below to install Docker and create a Dockerized Node.js app.

## Installing Docker on Ubuntu

### Step 1: Update the APT package index

```bash
sudo apt update
```

### Step 2: Install packages for HTTPS repository access

```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

### Step 3: Add Docker's official GPG key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

> Adding Docker's GPG key ensures the authenticity and integrity of Docker packages.

### Step 4: Set up the stable Docker repository

```bash
echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Step 5: Update the APT package index again

```bash
sudo apt update
```

### Step 6: Install Docker Engine and containerd

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

### Step 7: Start the Docker service

```bash
sudo systemctl start docker
```

> Check the status of your Docker service using `sudo systemctl status docker`

### Step 8: Enable Docker to start on boot

```bash
sudo systemctl enable docker
```

### Step 9: Add your user to the docker group

```bash
sudo usermod -aG docker $USER
```

> Log out and log back in or run `newgrp docker` for the changes to take effect.

## Install Node.js in the Docker image

### Step 1: Create a new project directory

```bash
mkdir node-docker
cd node-docker
```

### Step 2: Create a Dockerfile

```bash
touch Dockerfile
```

Edit the Dockerfile with the following content:

```docker
# Dockerfile

# Use the official Ubuntu base image
FROM ubuntu:latest

# Update package lists and install Node.js
RUN apt-get update && apt-get install -y nodejs npm

# Create and set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy the application files
COPY . .

# Expose a port
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
```

## Build image and run container

### Step 1: Build the Docker Image

```bash
docker build -t express-docker-image .
```

### Step 2: Run a Docker Container

```bash
docker run -p 3000:3000 --name express-docker-container express-docker-image
```

### Step 3: Stop a Docker container

```bash
docker ps
docker stop express-docker-container # or CONTAINER_ID
docker rm express-docker-container # or CONTAINER_ID
```

Feel free to explore and modify this setup based on your project requirements. Happy coding!
