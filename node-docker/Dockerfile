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

