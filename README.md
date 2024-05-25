# Deploying Static Website on AWS EC2 with Bash provisioning
As part of my DevOps engineer journey, I've created this project to enhance my Linux skills. This repository serves as a comprehensive guide and toolkit for hosting static websites on AWS EC2 instances using Bash script. Whether you're a beginner exploring the fundamentals of web hosting or an experienced developer seeking efficient deployment strategies, this repository provides practical insights and solutions tailored to your needs.
Provisioning with Bash script involves automating the setup and configuration of software and infrastructure using Bash, a popular Unix shell and scripting language. By writing Bash scripts, DevOps engineers can define the desired state of servers, applications, and environments, enabling efficient and repeatable deployment processes.

# Static Website Hosting with Nginx

In this project, we unzip a static website into the nginx folder using the powerful Bash script tool. This approach allows us to deploy a collection of HTML, CSS, and JavaScript files on EC2 on one click, making the deployment process smooth and efficient.

## Benefits

1. **Ease of Sharing**: Putting your website in Nginx folder creates a automation for see the website with a one click
2. **Deployment Skills**: This project introduces the fundamental skill of deploying web applications with bash scripting , which is essential in modern software development.

## Getting Started

Follow these instructions to build an instance with Website.

### Prerequisites


1.Create a Security Group on AWS EC2 : Allow port 80 (http) and 22 (ssh) inbound rule <br>
2.Create an EC2 Instance, Use Amazon Linux Base Image. <br>
3.Create an EC2 Instance using below provision shell script:
```
#!/bin/bash
# Set environment variables
ZIP_URL=https://www.free-css.com/assets/files/free-css-templates/download/page296/carvilla.zip
sudo yum update -y
sudo yum update -y && yum install -y wget unzip nginx && yum clean all
sudo systemctl start nginx
sudo mkdir -p /tmp/static-html
sudo wget -O /tmp/static-html/carvilla.zip $ZIP_URL
sudo unzip /tmp/static-html/carvilla.zip -d /tmp/static-html
sudo cp -r /tmp/static-html/carvilla-v1.0/* /usr/share/nginx/html/
sudo rm -rf /tmp/static-html

```


### Accessing the Website
Open your web browser and navigate to http://(Public-Ipv4-Of-Ec2) to see your static website hosted by Nginx.


## Acknowledgments
Nginx - A high-performance HTTP server and reverse proxy. <br>


## License
This project is licensed under the MIT License - see the [MIT](https://choosealicense.com/licenses/mit/) file for details

