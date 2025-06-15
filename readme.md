# Cloud Engineering Dynamic Landing Page – AltSchool Project

> **AltSchool of Engineering – Cloud Engineering (Second Semester Project)**

This project demonstrates how to provision a Linux server (AWS EC2), configure a web server (Nginx), and deploy a personalized dynamic landing page powered by Node.js. The landing page is reverse proxied by Nginx and served professionally to simulate a production-ready environment.

---

## 📑 Table of Contents

- [Project Objective](#project-objective)  
- [Getting Started](#getting-started)  
- [Server Setup](#server-setup)  
- [App Structure](#app-structure)  
- [Reverse Proxy with Nginx](#reverse-proxy-with-nginx)  
- [Dependencies](#dependencies)  
- [Deployment Details](#deployment-details)  
- [Screenshot](#screenshot)  
- [License](#license)

---

## 🎯 Project Objective

To showcase the deployment of a dynamic web prototype for a startup concept — using modern infrastructure, secure networking, and scalable deployment methods — hosted on an Ubuntu EC2 instance. This is aimed at displaying cloud engineering skills to potential investors.

---

## 🚀 Getting Started

To replicate this project:

<!-- 1. **Clone the Repo**
   ```bash
   git clone https://github.com/folacode22/altshool-tinyuka-ss-exam.git
   cd altshool-tinyuka-ss-exam -->

## 🖥Server Setup
1. **Provisioning the Server**
 Using AWS EC2 (Ubuntu 22.04 LTS recommended)
- Log in to AWS Console

- Launch an EC2 instance:

- AMI: Ubuntu 22.04 LTS

- Instance type: t2.micro (free tier eligible)

- Key pair: Create/download key

- Security Group: Allow HTTP (80), HTTPS (443), and SSH (22)

- Click "Launch"

- Copy the public IP address

2. **SSH into the EC2 Instance**
```
chmod 400 your-key.pem
ssh -i your-key.pem ubuntu@<your-ec2-public-ip>

```
3. **Install Nginx and Node.js**
```
sudo apt update
sudo apt install nginx -y

# Install Node.js and npm
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs


```
4. **Create Your Node.js App**
```
mkdir ~/tinyuka
cd ~/tinyuka

nano server.js
Paste this in server.js:

```
server.js

```
const express = require('express');
const app = express();
const port = 8080;

app.use(express.static('public'));

app.listen(port, () => {
  console.log(`App running at http://localhost:${port}`);
});

```
Install dependencies:
```
npm init -y
npm install express

```

5. **Create public/index.html and include your landing page**

content:Name, role

Project title: “The Future of [Your Startup Idea]”

2-3 sentence pitch

Bio

Style with Tailwind CSS or animations

## 📁App structure

```
project-root/
│
├── README.md
├── server.js
├── package.json
└── public/
    ├── index.html
    └── styles.css (optional)
```


## Reverse Proxy with Nginx
1. **Set Up Nginx Reverse Proxy**

```
sudo nano /etc/nginx/sites-available/default

```
Replace the location / block with:
```
location / {
    proxy_pass http://localhost:8080;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}

```
Then:

```
sudo systemctl restart nginx

```


## 📦Dependencies
| Package            | Purpose                                                       |
| ------------------ | ------------------------------------------------------------- |
| **Node.js**        | JavaScript runtime used to run the server                     |
| **Express**        | Lightweight web application framework for Node.js             |
| **Nginx**          | Web server used as a reverse proxy to forward traffic to Node |
| **HTML/CSS**       | Structure and styling for the landing page                    |
| **AWS EC2**        | Hosting platform (Ubuntu Linux instance)                      |
| **PM2 (optional)** | Keeps Node.js app alive in production                         |
| **OpenSSH**        | Secure remote access to the Linux server                      |




## 🚀Deployment Details
| Item                 | Description                                                                  |
| -------------------- | ---------------------------------------------------------------------------- |
| **Hosting Platform** | AWS EC2 (Ubuntu 20.04 LTS)                                                   |
| **Instance Type**    | t2.micro (Free Tier eligible)                                                |
| **Web Server**       | Nginx (acts as a reverse proxy)                                              |
| **App Runtime**      | Node.js server running on port `8080`                                        |
| **Reverse Proxy**    | Nginx forwards HTTP traffic from port `80` to the Node.js app on port `8080` |
| **Public IP**        | [http://<your-ec2-public-ip>](http://18.133.247.25/)   |
| **Firewall Rules**   | Opened ports `22` (SSH), `80` (HTTP), and `8080` (for test access only)      |
| **SSL**              | *(Skipped for now; can add Let's Encrypt via Certbot later)*                 |


## 🌐 Deployment Details
Public IP: http://18.133.247.25/

Hosting Type: EC2 Ubuntu Server

Server Access: SSH key-based authentication


## Screenshot
![image](../image/Screenshot%202025-06-15%20164043.png)
