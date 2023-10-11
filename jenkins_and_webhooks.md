# Steps for using Jenkins

![Alt text](<images/CI CD diagram.jpg>)

## Creating Jobs

### Logging into Jenkins

1) Go to the Jenkins login page.
2) Log in with the correct credentials.

### Creating a job on Jenkins

1) To create a new job on Jenkins:
- In the left hand pane, click on `New item`.
- Enter an item name for the job you're (something relatable) e.g. `alex-first-job`.
- Choose the project type, in this case `Freestyle project`.
- Click `OK`.
2) On the next page:
- Add a description under the "General" tab.
- Also in "General", limit the number of previous builds that can be kept so you don't end up with loads of jobs and crash the system
- Scroll down until you're in the "Build" tab and run commands to test out what the OS environment is and if Jenkins can run it.
- 
3) Click `OK`

### Run the job

1) Next to the name of the job, in the dropdown list, click `Build now` to test the job.

### Linking jobs

1)

## Connecting Jenkins to GitHub using SSH

### 1) Connecting Local computer to GitHub

1) Follow the steps in https://github.com/AlexAnderson220994/GitHub_SSH/blob/main/README.md
2) Create the SSH key pair and add the PUBLIC SSH key to Github.

### 2) Adding Public SSH key to GitHub Repo

1) Generate an entirely new SSH key pair (name it something like `jenkins_ssh`).
2) On GitHub, navigate to the specific Repo you want to connect to Jenkins.
![Alt text](<images/connecting ssh key to repo.jpg>)
3) Click on `Settings` in the top ribbon.
4) Click on `Deploy keys` on the left hand pane
![Alt text](<images/deploy keys.jpg>)
5) Give the key a name
6) On Gitbash, navigate to your .ssh folder where your SSH keys are stored
7) Open the contents of the **PUBLIC** key using:
````
cat <key_name.pub>
````
8) Copy the public key that comes up (leave no spaces)
9) Paste they key into the "Key" box on the Deploy keys page.
10) Click `Allow write access`
11) Click `Add key`

