# Steps for using Jenkins

## Logging into Jenkins

1) Go to the Jenkins login page.
2) Log in with the correct credentials.

## Creating a job on Jenkins

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

## Run the job

1) Next to the name of the job, in the dropdown list, click `Build now` to test the job.

## Linking jobs

1)