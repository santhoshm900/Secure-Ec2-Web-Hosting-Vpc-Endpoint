🔐 Secure EC2 Web Hosting Using VPC Endpoint

This project demonstrates how to securely host a web application on an EC2 instance by initially using a public IP for setup and later eliminating internet exposure by removing the public IP and enabling private access using a VPC Endpoint.

Built on Amazon Web Services, this architecture follows security best practices by restricting direct internet access while maintaining secure administrative connectivity.

📌 Project Objective

Deploy NGINX on EC2

Verify application using public IP (initial phase)

Remove all public internet exposure

Access EC2 securely using EC2 Instance Connect VPC Endpoint

Ensure the web server runs only inside private networking

🧱 Step 1: Create Custom VPC

Created a custom VPC with a private CIDR range

Used to isolate all resources

📸 screenshots/vpc.PNG

🧱 Step 2: Create Private Subnet

Created a private subnet inside the VPC

EC2 instance launched in this subnet

📸 screenshots/subnet.PNG

🌐 Step 3: Attach Internet Gateway (Temporary)

Internet Gateway attached only for initial setup

Required to install packages (NGINX)

📸 screenshots/IGW.PNG

🛣️ Step 4: Configure Route Table

Added default route:

0.0.0.0/0 → Internet Gateway


Enabled outbound internet access temporarily

📸 screenshots/Route-table-with-route.PNG

💻 Step 5: Launch EC2 Instance

Instance Type: t2.small

OS: Ubuntu

Subnet: Private

Auto-assign Public IP: Enabled (temporary)

📸 screenshots/ec2-instance.PNG

🔧 Step 6: Install NGINX Web Server

Connected to EC2 and installed NGINX:

sudo apt update
sudo apt install nginx -y

🌍 Step 7: Verify Website Using Public IP

Accessed NGINX using public IP

Confirmed web server is running

http://<Public-IP>


📸 screenshots/publicip-http-via-wesite-working.PNG

📝 Step 8: Upload Custom HTML Page

Replaced default NGINX page with a BMW Car Showroom static website.

cd /var/www/html
sudo nano index.html

🚫 Step 9: Disable Public Internet Access
9.1 Disable Auto-Assign Public IP

Prevents public IP assignment during restart

📸 screenshots/stop-auto-assign-public-ip.PNG

9.2 Remove Existing Public IP

Manually unassigned public IPv4 address

📸

screenshots/remove-public-ip-from-ec2.PNG

screenshots/publi-ip-disabled.PNG

Result

Website no longer accessible from the internet

Public exposure fully eliminated

📸 screenshots/ec2-not-in-public.PNG

🔐 Step 10: Create VPC Endpoint (EC2 Instance Connect)

Created EC2 Instance Connect Endpoint

Allows secure private access without public IP

📸

screenshots/vpc-endpoint-created.PNG

screenshots/vpc-endpoint.PNG

🔑 Step 11: Connect to EC2 Using Private IP

Connected securely via EC2 Instance Connect

No SSH, no public IP, no internet exposure

📸 screenshots/ec2-connect-via-endpoint.PNG
