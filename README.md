# HNG-Tasks
# Static Website Deployment on AWS EC2 Using NGINX

This repository contains the deployment configuration and files for my static website as part of the HNG Internship Stage 0 Task. I deployed the website on AWS EC2 instance using NGINX as the web server.

## Steps in the Deployment 

### 1. Launch an AWS EC2 Instance
1. I logged in to my AWS account.
2. I navigated to the EC2 dashboard and clicked "launch instance".
3. I chose Ubuntu as the Amazon Machine Image (AMI).
4. I chose t3.micro as the instance type.
5. Then, i configured the details including storage, tags, security group (SSH and HTTP).
6. I reviewed the settings, downloaded the key pair file (aws.pem) and launched the instance.

### 2. Connect to the Instance
1. I opened my ubuntu terminal and connected to the instance using SSH:
    ```bash
    ssh -i aws.pem ubuntu@51.20.3.59
    ```

### 3. Install NGINX
1. I updated the package list and installed NGINX:
    ```bash
    sudo apt update
    sudo apt install nginx -y
    ```

### 4. Prepare the Static Website
1. I created a directory for my website and created a new html file to add the approriate details to my website:
    ```bash
    sudo mkdir -p /var/www/html/kafayat@hng
    touch stage0.html ; then, i added my name, username, email and HNG site link.
    ```

2. I uploaded my static website files to the EC2 instance:
    ```bash
    scp -i aws.pem -r /var/www/html/kafayat@hng/stage0.html ubuntu@51.20.3.59:/var/www/html/kafayat@hng
    ```

### 5. Configure NGINX
1. I opened the NGINX default configuration file using nano file editor:
    ```bash
    sudo nano /etc/nginx/sites-enabled/default
    ```

2. And edited the file to point to my website directory:
    ```nginx
    server {
        listen 80;
        server_name ubuntu@51.20.3.59;

        root /var/www/html/kafayat@hng;
        index stage0.html ;

        location / {
            try_files $uri $uri/ =404;
        }
    }
    ```

3. I tested the NGINX configuration:
    ```bash
    sudo nginx -t
    ```

4. Finally, i reloaded the NGINX to apply the changes:
    ```bash
    sudo systemctl reload nginx
    ```

### 6. Access Your Website
1. I opened a web browser and navigated to `http://51.20.3.59` to see my deployed static website.

## Website Details
- Name:Kafayat Adeyemi 
- Username:Twinmom
- Email: adeyemikafayat64@gmail.com
- HNG Internship Link: [HNG Internship](https://hng.tech) 
