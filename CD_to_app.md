# Connecting EC2 to the CI/CD Pipeline

## CD Diagram

![Alt text](<images/Diagram v2.jpg>)

## Step 1 - Set up a new EC2 Instance

1) Name the instance.
2) Choose the Ubuntu 20.04 AMI
3) Create a new Security Group to allow the following:
- SSH (22)
- HTTP (80)
- Nginx (3000)
- Jenkins (8080)

## Step 2 - SSH into EC2 Instance and start nginx

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


