
#  Inception-42


##  Installing Docker on Ubuntu.

- Update the APT package index
```bash
sudo  apt  update
```
###
- Install packages to allow apt to use a repository over HTTPS
```bash
sudo  apt  install-y  apt-transport-https  ca-certificates  curl  software-properties-common
```
###
- Add Docker's official GPG key
```bash
curl-fsSL  https://download.docker.com/linux/ubuntu/gpg  |  sudo  gpg--dearmor-o  /usr/share/keyrings/docker-archive-keyring.gpg
```
> When you add Docker's official GPG key, you are essentially importing
> the key into the GPG keyring on your system. This key is used to sign
> Docker packages, ensuring their authenticity and integrity. The GPG
> key is a form of cryptographic verification.
###
- Set up the stable Docker repository
```bash
echo  "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release-cs) stable"  |  sudo  tee  /etc/apt/sources.list.d/docker.list  >  /dev/null
```
###
- Update the APT package index again
```bash
sudo  apt  update
```
###
- Install the latest version of Docker Engine and containerd
```bash
sudo  apt  install-y  docker-ce  docker-ce-cli  containerd.io
```
###
- Start the Docker service
```bash
sudo  systemctl  start  docker
```
> you can check the status of your docker service using `sudo systemctl status docker`
###
- Enable Docker to start on boot
```bash
sudo  systemctl  enable  docker
```
###
- Add your user to the docker group to run Docker commands without sudo
```bash
sudo  systemctl  enable  docker
```



##  Install Node.js in the Docker image.

- Create a new directory for your project
```bash
mkdir  node-docker
cd  node-docker
```
###
- Create a file named Dockerfile in your project directory
```bash
touch  Dockerfile
```

```docker
#Dockerfile

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