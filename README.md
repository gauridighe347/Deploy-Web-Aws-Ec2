
# Deploy Web Application on AWS EC2

## 📘 Overview
This project demonstrates how to manually deploy a web application on an AWS EC2 instance.

---

## ⚙️ Steps

### Step 1: Update and Upgrade Packages
Commands:

sudo apt update
sudo apt upgrade -y

Step 2: Install and Verify Node.js
Copy code
node -v

Step 3: Configure Security Group
Allow inbound rules for HTTP (80), HTTPS (443), and SSH (22).

Step 4: Connect to EC2 Instance
sss-i "myker-pair.pem" ubuntu@ec2-13-235-79-99.ap-south-1.compute.amazonaws.com

Step 5: Enable Firewall
Commands:
sudo ufw enable
sudo ufw allow 'Nginx Full'
sudo ufw reload

Step 6: Clone GitHub Repository
Command:
git clone https://github.com/gauridighe347/Deploy-Web-Aws-Ec2.git

Step 7: Run Application
Command:
node app.js

Step 8: Verify Output

Check your browser using EC2 public IP.
>>>>>>> f7d1b63 (Recreated clean README)
