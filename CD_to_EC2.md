# Integrating CD into the Pipeline

## 1) Setting up the CD Environment

1) Make a Jenkins job that will connect to EC2 create an App and a DB virtual machine.
- Name it `alex-CD`.
2) This job needs to be triggered if job 2 is successful.
3) SSH in with tech254.pem
2) In the "Build" section, add the following shell script:
````
# Allow yes to connect via SSH
-y

# Create the database environment varaiable
export DB_HOST=mongodb://<public/private_IP_of_DB_instance>:27017/posts

# cd into app repo
cd /home/ubuntu/sparta_app/app
sudo systemctl restart nginx
npm install

node seeds/seed.js

sudo npm install pm2 -g
pm2 kill
pm2 start app.js
````
## 2) Set up the App Virtual Machine

1) Launch an App instance on AWS
2) Configure the security group to allow Port 8080 for Jenkins
3) Use -y to SSH into the instance on first connection from local host.
4) `sudo apt update` and `sudo apt upgrade -y`
5) Install nginx.
6) Start and enable nginx
7) Change the configure settings to allow for the reverse proxy to Port 3000
8) Restart nginx
9) Make sure the correct version of nodejs has been installed (version 12.x)
10) Install pm2

## 3) Set up the Database Virtual Machine

1) Launch an EC2 instance on AWS
2) Configure security group to allow Port 27017 for MongoDB 
2) Use -y to SSH into the instance on first connection from local host.
3) `sudo apt update` and `sudo apt upgrade -y`
4) Get the correct version of MongoDB (version 3.x) with the curl command.
5) Install this version of MongoDB
6) Change the BindIP to 0.0.0.0
7) Do `sudo systemctl start mongod` and `sudo systemctl enable mongod`.

## 4) Make a change to test the pipeline is working

1) In gitbash, cd into your repo folder.
2) Make sure you're on the dev branch.
3) Change a setting within the app test file to allow for your name in the title of the app.
4) Change the app name in the settings.
5) Push this change and test it on the pipeline.

## 5) Manually Check that the App is running

1) SSH into the app on your local host.