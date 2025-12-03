 DEPLOYMENT OF index.html USING AWS EC2 INSTANCE
🔹 Step 1: Login to AWS / Canvas Account

Open the course invitation mail → click Start

AWS Academy page opens → choose Student Login → enter credentials

Click Modules

Scroll down → select Launch AWS Academy Lab

Click Start Lab → wait for AWS status to turn Red → Green

Click AWS to enter the console

🔹 Step 2: Create an EC2 Instance
1. Click “EC2” → “Launch Instance”
Stage 1 – Name

Enter a name like ubuntu

Stage 2 – Select AMI

Choose Ubuntu Server (Free Tier Eligible)

Make sure “Free-tier eligible” is visible

Stage 3 – Architecture

Select 64-bit (x86)

Confirm AMI + Architecture are correct

Stage 4 – Instance Type

Choose t2.micro

1 vCPU

1GB RAM

Free tier compatible

Stage 5 – Key Pair

Click Create new key pair

Give a name (example: mykey)

Download the .pem file

Save it in a folder (ex: AWS/ on Desktop)

Stage 6 – Network Settings (Security Group)

Enable these inbound rules:

Port	Protocol	Reason
22	SSH	To connect to server
80	HTTP	To load web pages
443	HTTPS	Secure access

Check all relevant checkboxes.

Stage 7 – Storage

Default 8GB (root volume) is enough

Stage 8 – Launch Instance

Click Launch Instance

Go to Instances

Wait for the green message “Successfully launched”

Instance Status

Wait for:

2/2 checks passed

Select the instance → click Connect

Your EC2 machine is now running.

🔹 Step 4: Connect Local System to EC2 (SSH)
a. Copy the .pem file path

Example:

D:\SUNNY\SELABWEB\AWS

b. Open PowerShell (Admin Mode)

Go to the folder:

cd D:\SUNNY\SELABWEB\AWS

c. Go to AWS Console → EC2 → Connect

Copy the SSH command:

ssh -i "mykey.pem" ubuntu@<public-ip>

d. Paste & run SSH command in PowerShell

You are now connected to the Ubuntu server.

🔹 Step 5: Install Required Software

Run these commands one by one:

1. Update system
sudo apt update

2. Install Docker
sudo apt-get install docker.io

3. Install Git
sudo apt install git

4. Install Nano editor
sudo apt install nano

🔹 Step 6: Create Application, Push to GitHub, Build Docker Image
a. Create folder Example and add index.html

Create a simple HTML file.

b. Open Git Bash in the Example folder

Right-click → Git Bash Here

c. Initialize Git repo
git init
git add .
git commit -m "first commit"

d. Create GitHub Repository

Example: repo name AWS

e. Connect local folder to GitHub

Copy commands from GitHub and execute:

git branch -M main
git remote add origin <https-url>
git push -u origin main

f. Refresh GitHub

You should now see index.html in the repo.

g. Copy repository URL (HTTP)
h. Clone repo inside EC2

In the SSH terminal:

git clone <copied-url>

i. Navigate to cloned folder
cd AWS
ls

j. Create Dockerfile
nano Dockerfile

k. Add this content inside Dockerfile
FROM nginx
COPY . /usr/share/nginx/html


Save:

Ctrl + O → Enter

Ctrl + X

l. Build Docker image
sudo docker build -t mywebapp .

m. Run container on port 80
sudo docker run -d -p 80:80 mywebapp

🔹 Step 7: Test the Deployment
a. Go to EC2 → Instances

Copy Public IPv4 Address

Example:

http://3.110.23.90

 Open it in browser → Your index.html loads successfully!
🔹 Step 8: Stop and Terminate Resources
Q. Stop running container
sudo docker ps
sudo docker stop <container-id>

Terminate the EC2 instance

Go to Instances

Instance State → Terminate

Confirm deletion

End the Lab

Click End Lab in AWS Academy.