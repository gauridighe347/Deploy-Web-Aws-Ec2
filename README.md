# 🚀 Deploy a Web Application on AWS EC2

## 🧰 Prerequisites
- Launched EC2 instance  
- **AMI:** Ubuntu  
- **Created Key Pair**  
- **Created Security Group**

---

## 🪄 Step 1: Launch EC2 Instance

1. Choose **Ubuntu AMI**  
2. Select an instance type (e.g., `t2.micro`)  
3. Add **Key Pair**  
4. Create a **Security Group** with inbound rules:  
   - SSH → Port 22  
   - HTTP → Port 80  
5. Launch the instance  

📸 **Instance Screenshot:**  
![EC2 Instance](Screenshots/instance.png)

📸 **Security Group Screenshot:**  
![Security Group](images/security-group.png)

---

## ⚙️ Step 2: Connect to the EC2 Instance

Use your key pair to SSH into the instance:

```bash
ssh -i "MY-KEY.pem" ec2-user@ec2-43-204-148-151.ap-south-1.compute.amazonaws.com
📸 Connection Screenshot:

🧩 Step 3: Install Packages and Dependencies
1️⃣ Update and upgrade the system
bash
Copy code
sudo apt update -y
sudo apt upgrade -y
📸 Update Screenshot:

2️⃣ Install Node.js
bash
Copy code
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
📸 Node.js Installation Screenshot:

3️⃣ Install Git and Nginx
bash
Copy code
sudo apt install -y git nginx
📸 Git & Nginx Screenshot:

4️⃣ Check installations
bash
Copy code
git --version
node --version
📸 Version Check Screenshot:

🧱 Step 4: Deploy Your Application
bash
Copy code
git clone https://github.com/Maheshbharambe45/Deploy-Webapp-Aws-Ec2.git
cd Deploy-Webapp-Aws-Ec2
If the project has dependencies, install them:

bash
Copy code
npm install
📸 Clone & Install Screenshot:

🔥 Step 5: Add Firewall Rules
1️⃣ Install firewalld
bash
Copy code
sudo apt install -y firewalld
2️⃣ Enable and start the firewall service
bash
Copy code
sudo systemctl enable firewalld
sudo systemctl start firewalld
📸 Firewall Service Screenshot:

3️⃣ Allow HTTP (port 80) and HTTPS (port 443)
bash
Copy code
sudo firewall-cmd --permanent --add-service=http
4️⃣ Reload firewall to apply changes
bash
Copy code
sudo firewall-cmd --reload
📸 Firewall Reload Screenshot:

🌐 Step 6: Set Up Reverse Proxy Using Nginx
Edit the Nginx configuration:

bash
Copy code
sudo nano /etc/nginx/nginx.conf
Add this block inside the http block 👇

nginx
Copy code
server {
    listen 80;
    server_name your-ec2-public-ip;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
Restart Nginx:

bash
Copy code
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl status nginx
📸 Nginx Config Screenshot:

🟢 Step 7: Start Your Application
bash
Copy code
node index.js
📸 App Start Screenshot:

🌍 Step 8: Access Your Application
Open your browser and visit:

arduino
Copy code
http://your-ec2-public-ip
📸 Website Screenshot:

✅ Deployment Complete!
Your Node.js web application is now successfully deployed on AWS EC2 using Nginx reverse proxy 🎉

