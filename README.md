# Secure-Ec2-Web-Hosting-Vpc-Endpoint
Deployed an NGINX web server on EC2, initially configured with a public IP and later secured by removing public access and enabling private connectivity using a VPC Endpoint.

# Secure EC2 Web Hosting Using VPC Endpoint

## 📌 Project Overview
This project demonstrates how to securely host a web application on an Amazon EC2 instance by initially using a public IP for setup and later removing the public IP to ensure private access using a VPC Endpoint.

The goal is to eliminate direct internet exposure while maintaining secure administrative access.

---

## 🧱 Step 1: Create Custom VPC
A custom VPC was created with a private CIDR range to isolate the resources.

![VPC Created](screenshots/vpc.PNG)


---

## 🧱 Step 2: Create Private Subnet
A private subnet was created inside the VPC to host the EC2 instance securely.

![Subnet Created](screenshots/subnet.PNG)

---

## 🌐 Step 3: Attach Internet Gateway (Initial Setup)
An Internet Gateway was attached to the VPC to allow internet access **only during the initial configuration phase**.

![Internet Gateway Attached](screenshots/IGW.PNG)


---

## 🛣️ Step 4: Configure Route Table
The route table was updated with a default route (`0.0.0.0/0`) pointing to the Internet Gateway.

![Route Table with IGW](screenshots/Route-table-with-route.PNG)

---

## 💻 Step 5: Launch EC2 Instance
An EC2 instance was launched inside the private subnet.

- Instance Type: t2.small  
- OS: Ubuntu  
- Auto-assign Public IP: Enabled (temporary)

![EC2 Instance](screenshots/ec2-instance.PNG)


---

## 🔧 STEP 6: INSTALL NGINX & DEPLOY CUSTOM HTML PAGE
---

This step covers installing **NGINX**, deploying a **custom HTML page**, and preparing the web server for verification.

---

### 🛠️ 6.1 Install NGINX

sudo apt update
sudo apt install nginx -y


📂 6.2 Navigate to NGINX Web Directory

cd /var/www/html

🗂️ 6.3 Backup Default NGINX Page 

sudo mv index.nginx-debian.html index.nginx-debian.html.bak

📝 6.4 Create a New index.html File

sudo nano index.html

🎨 6.5 Upload Custom HTML Code (BMW Showroom)


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>BMW Car Showroom</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, Helvetica, sans-serif;
            background-color: #0b0b0b;
            color: #ffffff;
            text-align: center;
        }

        header {
            background-color: #000000;
            padding: 25px;
            border-bottom: 4px solid #1c69d4;
        }

        header h1 {
            margin: 0;
            color: #1c69d4;
            letter-spacing: 3px;
        }
    </style>
</head>
<body>

<header>
    <h1>BMW CAR SHOWROOM</h1>
</header>

</body>
</html>
Save and exit the editor:
Ctrl + O → Enter → Ctrl + X

🔄 6.6 Restart NGINX Service

sudo systemctl restart nginx

![Insert HTML Code](screenshots/insert-html-code.PNG)



## 🌍 Step 7: Verify Website Using Public IP (Initial Phase)
After installing NGINX, the website was accessed using the EC2 public IP to verify that the web server was working correctly.

- URL: http://<Public-IP>
- Status: Website accessible

![Website Working via Public IP](screenshots/publicip-http-via-wesite-working.PNG)

---

## 📝 Step 8: Upload Custom HTML Page
The default NGINX page was replaced with a custom BMW Car Showroom static HTML page.


cd /var/www/html
sudo nano index.html

## 🚫 Step 8.1: Verify HTTP Access After Public IP Removal
After removing the public IP, the website was no longer accessible over HTTP from the internet.

- URL: http://<Public-IP>
- Status: Not reachable
- Reason: Public IP removed

![HTTP Access Blocked](screenshots/ec2-not-in-public.PNG)

---

## 🔒 Step 9: Disable Auto-Assign Public IP
Auto-assign public IP was disabled to prevent public IP assignment during instance restart.

![Stop Auto Assign Public IP](screenshots/stop-auto-assign-public-ip.PNG)

---

## ❌ Step 10: Remove Public IP from EC2
The public IPv4 address was manually unassigned from the EC2 instance to enhance security.

![Remove Public IP](screenshots/remove-public-ip-from-ec2.PNG)

![Public IP Disabled](screenshots/publi-ip-disabled.PNG)

---

## 🔐 Step 11: Create VPC Endpoint (EC2 Instance Connect)
An EC2 Instance Connect VPC Endpoint was created to allow secure private access to the EC2 instance.

![VPC Endpoint Created](screenshots/vpc-endpoint-created.PNG)

![VPC Endpoint Details](screenshots/vpc-endpoint.PNG)

---

## 🔑 Step 12: Connect to EC2 Using Private IP
The EC2 instance was accessed securely using its private IP through the VPC Endpoint.

![EC2 Connect via Endpoint](screenshots/ec2-connect-via-endpoint.PNG)


sudo apt install nginx -y

