# Deploying Static Website on AWS EC2 with Docker
As part of my DevOps engineer journey, I've created this project to enhance my Linux skills. This repository serves as a comprehensive guide and toolkit for hosting static websites on AWS EC2 instances using Docker containers. Whether you're a beginner exploring the fundamentals of web hosting or an experienced developer seeking efficient deployment strategies, this repository provides practical insights and solutions tailored to your needs.

# Static Website Hosting with Nginx

In this project, we package a static website into a Docker container using the powerful Nginx web server. This approach allows us to deploy a collection of HTML, CSS, and JavaScript files in a containerized environment, making the deployment process smooth and efficient.

## Benefits

1. **Ease of Sharing**: Putting your website in a Docker container creates a portable package that can be easily shared with others.
2. **Deployment Skills**: This project introduces the fundamental skill of deploying web applications in Docker containers, which is essential in modern software development.

## Getting Started

Follow these instructions to build and run your Docker container.

### Prerequisites


1.Create a Security Group on AWS EC2 : Allow port 80 (http) and 22 (ssh) inbound rule <br>
2.Use Amazon Linux Base Image

## Dockerfile

```
# Use the official Nginx image from Docker Hub
FROM nginx:alpine

# Set the maintainer label
LABEL maintainer="osherachamim@osherachamim.com"

# Set environment variables
ENV ZIP_URL=https://www.free-css.com/assets/files/free-css-templates/download/page296/carvilla.zip

# Update packages and install necessary tools
RUN yum update -y && \
    yum install -y wget unzip nginx && \
    yum clean all

# Create a temporary directory for downloading the ZIP file
RUN mkdir -p /tmp/static-html

# Download the ZIP file
RUN wget -O /tmp/static-html/carvilla.zip $ZIP_URL

# Unzip the file
RUN unzip /tmp/static-html/carvilla.zip -d /tmp/static-html

# Copy the unzipped files to the Nginx HTML directory
RUN cp -r /tmp/static-html/* /usr/share/nginx/html/

# Clean up the temporary files
RUN rm -rf /tmp/static-html

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]

```

### Building the Docker Image

Navigate to the project root directory in your terminal and run the following command to build the Docker image:

```
docker build -t my-static-website .
```
Running the Docker Container <br>
After building the image, you can run it with the following command:
```
docker run -d -p 80:80 --name static-website-container my-static-website
```
The -d flag runs the container in detached mode. <br>
The -p 80:80 flag maps port 80 on the host to port 80 on the container. <br>
--name static-website-container assigns a name to the running container <br>

### Accessing the Website
Open your web browser and navigate to http://(Public-Ipv4-Of-Ec2) to see your static website hosted by Nginx.

### Stopping the Container
To stop the running container, use the following command:
```
docker stop static-website-container
```
## Removing the Container
To remove the stopped container, use the following command: <br>
```
docker rm static-website-container
```

## Acknowledgments
Nginx - A high-performance HTTP server and reverse proxy. <br>
Docker - An open platform for developing, shipping, and running applications

## License
This project is licensed under the MIT License - see the [MIT](https://choosealicense.com/licenses/mit/) file for details

