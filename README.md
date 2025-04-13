# Travel-Memory-Application-Deployment
A distributed, full-stack web application for managing travel journals, architected with the MERN stack (MongoDB, Express.js, React, Node.js), deployed on AWS EC2 with Nginx for reverse proxying, integrated with MongoDB Atlas for persistence, and designed for high availability via AWS Application Load Balancer and Cloudflare DNS management.

## Architecture Overview
- API Endpoints: CRUD operations for travel memory entities (/trip), implemented with Express routes and Mongoose ODM.
- Frontend: React-based with component-driven UI for creating and viewing memories.
- Database: MongoDB Atlas cluster with sharded replica sets for high availability.
- Networking: Nginx reverse proxy to route external HTTP requests to internal Node.js processes.
- Scalability: AWS ALB with target groups for load distribution.
- DNS: Cloudflare integration for custom domain resolution (e.g., api.yourname.site).

## 📂 Project Repository

🔗 [GitHub - Travel Memory](https://github.com/UnpredictablePrashant/TravelMemory)

---

## ✨Highlights

- Scalable backend using Node.js & Express.
- Interactive UI powered by React.
- MongoDB Atlas as a managed NoSQL database solution.
- Nginx-based reverse proxy configured for port forwarding.
- Multi-instance deployment using AMIs on AWS EC2.
- Load balancing through AWS ALB.
- Domain routing and SSL support via Cloudflare (`shraddhabhat.site`).

---

## Tech Stack Overview

| Layer       | Tech                             |
|-------------|----------------------------------|
| Frontend    | React                            |
| Backend     | Node.js, Express                 |
| Database    | MongoDB Atlas                    |
| Cloud       | AWS EC2, Load Balancer, VPC, AMI |
| Server      | Nginx                            |
| DNS         | Cloudflare                       |

---

## Getting Started

### Prerequisites

- Ensure your MongoDB Atlas cluster has your backend EC2 IP whitelisted.
- EC2 instances are launched in **ap-south-1 (Mumbai)** region.
- Use AMIs for easy replication and scaling of environments.
  
---

## 🧱 Backend Deployment

**EC2 Instance (Backend)**  
- Public IP: `13.235.68.5`  
- Private IP: `172.31.0.49`
<img src="https://github.com/user-attachments/assets/ebf539d8-f12e-49c3-8740-f94462120082" width="600">

### Deployement Instructions

```bash
# Install fnm
curl -o- https://fnm.vercel.app/install | bash

# Install Node.js
fnm install 22

# Check Node and npm versions
node -v  # v22.14.0
npm -v   # 10.9.2

# Install Git and clone the repo
sudo yum install git -y
git clone https://github.com/UnpredictablePrashant/TravelMemory

# Navigate to backend and configure environment
cd ~/TravelMemory/backend
sudo nano .env

# Add the following:
MONGO_URI=your_mongo_uri
PORT=3000

# Install dependencies and run server
sudo npm install
sudo node index.js
```
<img src="https://github.com/user-attachments/assets/9b9c65b5-4d9e-4b51-9a8e-1d7ccc963851" width="600">
<img src="https://github.com/user-attachments/assets/9149d0b1-fe7a-4935-b351-e861f319e2f6" width="600">
<img src="https://github.com/user-attachments/assets/14fd3c11-0b12-4fe0-8f43-aa3c50f4ca92" width="600">
<img src="https://github.com/user-attachments/assets/19a2c7d1-72c5-4acd-aac9-258abec5a75c" width="600">

```bash    
# Configure Nginx reverse proxy:
sudo yum install nginx -y
sudo systemctl enable nginx
sudo nano /etc/nginx/nginx.conf

# Nginx config example:
server {
 listen 80;
 server_name _;
 location / {
     proxy_pass http://localhost:3000;
  }
}

# Apply and test Nginx:
sudo systemctl reload nginx
sudo systemctl restart nginx
sudo nginx -t #to validate nginx config file

# Start the backend:
node index.js
```
<img src="https://github.com/user-attachments/assets/cdc5a807-1b0c-4b9b-9996-23fcdb756b65" width="600">
<img src= "https://github.com/user-attachments/assets/6e67bc5f-7c25-44d4-bb57-caeb8ef50a5d" width="600">

---

## 🧱 Frontend Deployment

**EC2 Instance (Frontend)**  
- Public IP: `65.0.110.135`  
- Private IP: `172.31.1.233`

<img src= "https://github.com/user-attachments/assets/36efd4ea-9bd0-4579-ae73-4a0278922159" width="600">

### Deployement Instructions

```bash
# Install fnm
curl -o- https://fnm.vercel.app/install | bash

# Install Node.js
fnm install 22

# Check Node and npm versions
node -v  # v22.14.0
npm -v   # 10.9.2

# Install Git and clone the repo
sudo yum install git -y
git clone https://github.com/UnpredictablePrashant/TravelMemory

# Navigate to backend and configure environment
cd ~/TravelMemory/frontend
sudo nano .env

# create .env file
sudo nano .env

# Put the following content: 
REACT_APP_BACKEND_URL=http://backend_server_ip #eg. - http://13.235.68.5

# install the dependencies
npm install

# Update urls.js with backend IP or domain.

# Go to frontend/src directory
cd ~/TravelMemory/frontend/src
   
# Put the following content: 
export const baseUrl = process.env.REACT_APP_BACKEND_URL 

# Start the frontend application at port 3000 and validate.   
npm run build
npm start
```
<img src="https://github.com/user-attachments/assets/618ebd4c-9819-4d3c-8d94-2b8b4984c165" width="600">
<img src="https://github.com/user-attachments/assets/1dc7cb49-80a4-4432-bc31-7582af517baa" width="600">

```bash    
# Configure Nginx reverse proxy:
sudo yum install nginx -y
sudo systemctl enable nginx
sudo nano /etc/nginx/nginx.conf

# Nginx config example:
server {
 listen 80;
 server_name _;
 location / {
     proxy_pass http://localhost:3000;
  }
}

# Apply and test Nginx:
sudo systemctl reload nginx
sudo systemctl restart nginx
sudo nginx -t #to validate nginx config file

# Start the backend:
npm run build
npm start
```
<img src="https://github.com/user-attachments/assets/030e806b-a664-4664-892b-545d764e4887" width="600">

---

## Scaling & Load Distribution

### Create AMIs
Generate Amazon Machine Images (AMIs) for both frontend and backend instances to enable rapid scaling:  
<img src="https://github.com/user-attachments/assets/a4cd6556-8411-4362-a2ab-3541fc801b3e"  width="600">

### Deploy Instances
Launch additional EC2 instances using the created AMIs for scalability:  
<img src="https://github.com/user-attachments/assets/08d078be-864c-434d-abda-f404d1bab728" alt="Instance Deployment" width="600">

### Configure Target Groups
Set up target groups to manage traffic for load balancing:  
- Backend Target Group:  
  <img src="https://github.com/user-attachments/assets/01382a96-0f2d-4c1e-9105-6e4cfe408f39" width="600">  
- Frontend Target Group:  
  <img src="https://github.com/user-attachments/assets/f715fca9-424b-45ee-96f1-c52f82c2a86d" width="600">

### Establish Load Balancers
Configure AWS Application Load Balancers with multi-AZ support for high availability:  
<img src="https://github.com/user-attachments/assets/317c9fb1-89f3-42dc-a74c-3a104cb98dd3" width="600">  
<img src="https://github.com/user-attachments/assets/d97d9ca3-4987-49e9-9498-8a6efb7dea30" width="600">

---

## Custom Domain Integration

### Cloudflare Setup
Connect your domain and subdomain to the application using Cloudflare:  
- **Domain**: shraddhabhat.site  
- **Subdomain**: api.shraddhabhat.site

Add a CNAME record pointing to the load balancer endpoint:  
<img src="https://github.com/user-attachments/assets/e9f09dc9-b45e-4226-a740-58c8f637dc74" width="600">

### Update Frontend
Modify the frontend to use the custom domain:

```bash
# Go to frontend directory
cd ~/TravelMemory/frontend

# Create .env file
sudo nano .env

# Add the following content (customize as needed):
REACT_APP_BACKEND_URL=http://backend_api_url #e.g. - http://api.shraddhabhat.site

# Build the dependencies
npm run build

# Start the application
sudo npm start

<img src="https://github.com/user-attachments/assets/e9f09dc9-b45e-4226-a740-58c8f637dc74" width="600">

#Access the application through the custom domain with DNS fully configured:
<img src="https://github.com/user-attachments/assets/1fec3d3d-0945-4708-8982-aded059b8717" width="600">

#Use the "Add Experience" feature to input new travel entries:  
<img src="https://github.com/user-attachments/assets/b5ef034e-acf7-4401-a974-96c3d1951211" width="600">

#All entries are securely saved in MongoDB Atlas:  
<img src="https://github.com/user-attachments/assets/f5848beb-c723-418e-94a7-1d7eb721e0d4" width="600">

## Deployment Summary
- Backend: Deployed on EC2 with Nginx handling port 80.  
- Frontend: Active on EC2 with Nginx on port 80.  
- Database: Linked to MongoDB Atlas for persistence.
- Load Balancing: Enabled with multi-AZ coverage.  
- Domain: Fully integrated via Cloudflare.






















