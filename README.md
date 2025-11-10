Deploy a Web Application on AWS EC2

Prerequisites

Launched EC2 instance
AMI: Ubuntu
Created Key Pair
Created Security Group
Step 1: Launch EC2 Instance
Choose Ubuntu AMI
Select an instance type (e.g., t2.micro)
Add Key Pair
Create a Security Group with inbound rules:
SSH → Port 22
HTTP → Port 80
Launch the instance ✅ 
![instance img](Screenshots%instance.png)


6.Security group
 Website Screenshot

Step 2: Connect to the EC2 Instance
Use your key pair to SSH into the instance:

ssh -i "MY-KEY.pem" ec2-user@ec2-43-204-148-151.ap-south-1.compute.amazonaws.com
Website Screenshot

Step 3: Install Packages and Dependencies
1️⃣ Update and upgrade the system

sudo apt update -y
sudo apt upgrade -y
Website Screenshot

2️⃣ Install Node.js

curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
Website Screenshot Website Screenshot

3️⃣ Install Git and Nginx

sudo apt install -y git nginx
Website Screenshot

4️⃣ Check installations

git --version
node --version
Website Screenshot

Step 4: Deploy Your Application
git clone https://github.com/Maheshbharambe45/Deploy-Webapp-Aws-Ec2.git
cd Deploy-Webapp-Aws-Ec2
project has dependencies, install them

npm install
Step 5: Add Firewall Rules
1️⃣ Install firewalld

sudo yum install -y firewalld
2️⃣ Enable and start the firewall service

sudo systemctl enable firewalld
sudo systemctl start firewalld
Website Screenshot Website Screenshot

3️⃣ Allow HTTP (port 80) and HTTPS (port 443)

sudo firewall-cmd --permanent --add-service=http
4️⃣ Reload firewall to apply changes

sudo firewall-cmd --reload
Step 6: Set Up Reverse Proxy Using Nginx
Edit the Nginx configuration: Website Screenshot

sudo nano /etc/nginx/nginx.conf
Add this block inside the http block

server {
    listen 80;
    server_name your-ec2-public-ip;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
restart nginx

sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl status nginx
Step 7: Start Your Application
node index.js
Website Screenshot

Step 8: Access Your Application
http://<your-ec2-public-ip>
Website Screenshot

Website Screenshot