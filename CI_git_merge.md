# Git Merge using Jenkins

## 1) Setting up CI job for 'dev' branch

1) On the Configuration settings for the CI job(job 1)
2) Go to "Source code management":
- Under "Branches to build", change this from `*/main` to `*/dev`
![Alt text](<images/Git Merge/Screenshot 2023-10-12 113240.jpg>)
3) Under "Post build actions"
- Choose your merge job (Heading 2)
- Press `Trigger only if build is stable`
![Alt text](<images/Git Merge/Screenshot 2023-10-12 113339.jpg>)

## 2) Setting up Merge job

![Alt text](<images/Git Merge/Screenshot 2023-10-12 113459.jpg>)
![Alt text](<images/Git Merge/Screenshot 2023-10-12 113550.jpg>)
![Alt text](<images/Git Merge/Screenshot 2023-10-12 113637.jpg>)
![Alt text](<images/Git Merge/Screenshot 2023-10-12 113708.jpg>)

## 3) Change repo from main to dev on Gitbash

1) `cd` into the folder for the Repo you're working with
2) Input the command `git branch dev` to create a dev branch within this repo.
3) Change to the dev branch from the main branch with the command `git checkout dev`.
4) The command from point 3 also works to change back to main.

## 4) Push from dev branch

1) Make sure you're on the 'dev' branch on your gitbash terminal.
2) Do the `git add` and `git commit` for any files you've made changes to.
3) Push to github using `git push -u origin dev`.
4) Check Jenkins to see if there are any errors.
