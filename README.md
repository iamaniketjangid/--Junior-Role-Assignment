# --Junior-Role-Assignment
# DevOps CI/CD Project – Node.js Deployment with Jenkins, NGINX & Monitoring

Hi there! I'm Aniket Jangid, and this project is part of my DevOps engineer journey 

The goal? Build a complete CI/CD pipeline for a Node.js app — from code to production, secured and monitored end-to-end

# What I Did

##1. Set Up the App
- Cloned the Node.js project from GitHub
- Installed all dependencies using `npm install`
- Ran the app locally to make sure it works

---

#2. CI/CD with Jenkins
- Installed Jenkins on Ubuntu EC2
- Created a Jenkins pipeline job that:
  - Pulls code from Git
  - Installs dependencies
  - Runs tests (if any)
  - Deploys using PM2

---

##3. Jenkins Security (Matrix-based)
- Enabled matrix-based security
- Created two roles: `admin` and `developer`
- Removed access for anonymous users

---

#4. NGINX + SSL + DuckDNS
- Set up NGINX as a reverse proxy for the Node.js app
- Used DuckDNS for a free domain: `devlogin.duckdns.org`
- Installed SSL using Let's Encrypt + Certbot
- App now runs on **HTTPS**:  
  👉 [https://devlogin.duckdns.org](https://devlogin.duckdns.org)

---

#5. Monitoring Setup
- Installed **Node Exporter** for Linux system metrics (CPU, RAM, disk, etc.)
- Set up **Prometheus** to collect those metrics
- Used **PM2** to monitor Node.js process health
- Now I can track everything in real-time

---

## 🗂 Folder Structure
├── app/ # Node.js app
├── scripts/ # Bash scripts (Jenkins, DuckDNS, etc.)
├── nginx/ # NGINX config
├── monitoring/ # Prometheus and Node Exporter setup
├── screenshots/ # Setup screenshots
└── README.md


Install Prerequisites
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install git -y
sudo apt install nodejs npm -y


install jenkins
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y

start jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins


Unlock Jenkins Web Dashboard
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

http://ip:8080



PIPELINE
pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/heroku/node-js-sample.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || echo "No tests available"'
            }
        }

        stage('Start Application') {
            steps {
                sh 'nohup npm start &'
            }
        }
    }
}


git clone https://github.com/heroku/node-js-sample.git
cd node-js-sample
npm install
sudo npm install -g pm2
pm2 start index.js



give me 
