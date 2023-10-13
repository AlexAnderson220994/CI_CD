# Connecting EC2 to the CI/CD Pipeline

## CD Diagram

![Alt text](<images/Diagram v2.jpg>)

## 1) SSH to EC2 and setting up nginx

![Alt text](<images/CD/2. SSH to EC2 diagram..jpg>)

### Step 1 - Set up a new EC2 Instance

1) Name the instance.
2) Choose the Ubuntu 20.04 AMI
3) Create a new Security Group to allow the following:
- SSH (22)
- HTTP (80)
- Nginx (3000)
- Jenkins (8080)

### Step 2 - SSH into EC2 Instance and start nginx

1) Create a new job on Jenkins called "alex-CD".
2) Under "Build", Select `Execute Shell` from the dropdown list
3) Input the following script to allow SSH access and start running nginx:
````
# Input command to disable host checking for SSH connection
rsync -avz -e "ssh -o StrictHostKeyChecking=no" app ubuntu@34.243.73.114:/home/ubuntu

ssh -o "StrictHostKeyChecking=no" ubuntu@34.243.73.114 <<EOF
	sudo apt update -y
    sudo apt upgrade -y
    sudo apt install nginx -y
    sudo systemctl restart nginx
    sudo systemctl enable nginx
    
EOF
````
![Alt text](<images/CD/1.Screenshot 2023-10-13 124509.jpg>)

- The `rsync` command copies the code from the app folder to the instance.

4) Manually trigger this job in Jenkins first to test it works.
5) If the public IP shows the nginx page it has run successfully.
6) If there's an error, open the console output and see what the error is.
7) If the test is successful, add it to the post build options on your merge job `alex-merge`.

## 2) Make new job to run the app

![Alt text](<images/CD/3. App set up.jpg>)

1) Create a fourth job on Jenkins called `alex-app`.
2) Set up the rest of the job as per `alex-cd`.
3) In "Build", in "Execute Commands", add the following script:
````
ssh -A -o "StrictHostKeyChecking=no" ubuntu@34.243.73.114 <<EOF

# install Node.js and npm
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt install nodejs -y

# move to app folder
cd app

# restart nginx
sudo systemctl restart nginx

# install dependencies
npm install

# install pm2 globally
sudo npm install pm2 -g

# kill pm2
pm2 kill

# Start the Node.js application
pm2 start  app.js

pm2 restart app.js
````
4) Add a post build action to `alex-cd` to trigger `alex-app`
5) Run the build on `alex-cd` again to test the script works.
6) Remember to add **:3000** to the end of your public IP before the reverse proxy is set up.

## 3) Make new job to run DB


