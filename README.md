# Deploying an Application on AWS EC2
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







6.Security group



Step 2: Connect to the EC2 Instance
Use your key pair to SSH into the instance:

ssh -i "My-keypair.pem" ec2-user@ec2-43-204-148-151.ap-south-1.compute.amazonaws.com














Step 3: Install Packages and Dependencies
1️⃣ Update and upgrade the system

sudo apt update -y
sudo apt upgrade -y








## Step 4: Deploy Your Application
1. Clone your application repository:
   ```sh
   git clone https://github.com/your-repo/app.gitDeploy a Web Application on AWS EC2

   cd app
   ```
2. Install dependencies:
   ```sh
   npm install  # For Node.js apps
   ```
3. Start the application:
   ```sh
   node server.js &
   ```

## Step 5: Configure Firewall and Security Group
Ensure your EC2 instance allows inbound traffic on required ports:
```sh
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload
```

Modify security group in AWS to allow necessary ports.

## Step 6: Set Up a Reverse Proxy (Optional)
For production deployments, use Nginx as a reverse proxy:
```sh
sudo nano /etc/nginx/nginx.conf
```
Configure the `server` block:
```nginx
server {
    listen 80;
    server_name your-ec2-public-ip;
    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```
Restart Nginx:
```sh
sudo systemctl restart nginx
```

## Step 7: Enable Auto-Start (Optional)
Use **PM2** to keep your app running:
```sh
npm install -g pm2
pm2 start server.js
pm2 startup
pm2 save
```

## Step 8: Access Your Application
Visit `http://your-ec2-public-ip` in a browser.

## Conclusion
Your application is now live on AWS EC2! 🎉 For production, consider using **Elastic Load Balancing (ELB)** and **Auto Scaling** for better scalability.
