# Integrating CD into the Pipeline

## CI/CD Pipeline Diagram

![Alt text](<images/Diagram v2.jpg>)

## Development Process to make CD Architecture

- **STEP 1** - Set up a new job on Jenkins
- **STEP 2** - Set up the App Virtual Machine
- **STEP 3** - Set up the DB Virtual Machine
- **STEP 4** - Test all this by altering code
- **STEP 5** - Manual checks by SSH into instance

## 1) Setting up the CD Environment on Jenkins

1) Make a Jenkins job that will connect to EC2 create an App and a DB virtual machine.
- Name it `alex-CD`.
2) Go to your merge job `alex-merge` and set the post build to trigger `alex-cd` if the changes are successful.
3) Add the SSH connection in `alex-cd` with tech254.pem
![Alt text](<images/Git Merge/Screenshot 2023-10-12 113637.jpg>)
4) Change the restriction to the App EC2 instance.
![Alt text](<images/office 365.jpg>)

4) In the "Build" section, add the following shell script:
````
# Allow yes to connect via SSH
-y

# cd into app repo
cd /home/ubuntu/sparta_app/app

# restart nginx
sudo systemctl restart nginx

# do npm install
npm install
````
## 2) Set up the App Virtual Machine on EC2

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

## 3) Set up the Database Virtual Machine on EC2

1) Launch an EC2 instance on AWS
2) Configure security group to allow Port 27017 for MongoDB 
3) Use -y to SSH into the instance on first connection from local host.
4) `sudo apt update` and `sudo apt upgrade -y`
5) Get the correct version of MongoDB (version 3.x) with the curl command.
6) Install this version of MongoDB
7) Change the bindip from 127.0.0.0 to 0.0.0.0.
8) Do `sudo systemctl start mongod` and `sudo systemctl enable mongod`.

## 4) Make changes to APP code to test the pipeline is working

1) In gitbash, cd into your repo folder.
2) Make sure you're on the dev branch.
3) Change a setting within the app test file to allow for your name in the title of the app.
- Change this from the repo on your local host
- Change the test settings by going into `app`-`test`-`test_server.js`
- Modify the line in the JS file that says the app must display the word "Sparta" to say "your_name Sparta"
- Modify the actual name by going into `app` - `views` - `index.ejs` (use the nano command to edit or open it in VS code)
4) Push this change from your dev branch so it goes through the test process.
5) If the test is successful, Jenkins will push the change to the main branch.
 

