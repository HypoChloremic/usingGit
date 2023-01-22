# Github cheat-sheet

`git pull --rebase`

`git push`

The full syntax is:

`git pull --rebase origin master`

`git push origin master`

That way, you would replay (the --rebase part) your local commits on top of the newly updated origin/master (or origin/yourBranch: `git pull origin yourBranch`).

See a more complete example in the chapter 6 Pull with rebase of the Git Pocket Book.

I would recommend a:

`git push -u origin master`

That would establish a tracking relationship between your local master branch and its upstream branch.
After that, any future push for that branch can be done with a simple:

`git push`

See "Why do I need to explicitly push a new branch?".


# basic commands

Cheat Sheet

Using Git Bash or the Terminal navigate to the actual project folder. If you are using Git Bash you can right-click the project folder and select “Git Bash Here” and it will start you in that working directory.

`git init` This will create a .git repository in your project. A repository or “repo” is a collection of all the changes you’ve made to your project over time and will build a history of these changes. This is the first thing you want to do with a new project.

`git config --global user.name "Your Name"`

`git config --global user.email "yourEmail@mail.com"` This sets up your information that is used every time you commit. This only needs to be done once when you first install Git.

`git add filename.extension Replace “filename.extension”` to whatever file you are trying to add like “index.html”. This will add the file you specify to what is called a “staging area” or index. Think of the staging area like a section where things are getting set up to be moved to your repository.

`git add .` If you want to add everything from the project folder to the staging area this command will do that instead of having to add each file one by one.

`git add *.html` If you want to add all .html files to your staging area this would be the command to use. The extension can be changed to whatever you want.

`git status` Shows what has already been added to the staging area and what files have been changed that need to be added to the staging area.



## RESETING STUFF
`git reset filename.extension` Removes specified file from the staging area.

`git rm --cached filename.extension` This will remove the file from the staging area and sets it to be untracked.



`git commit -m "Description of the commit"` Takes the files from your staging area and commits them to your local repository. In quotes will be a brief description of what was changed with each commit. Try to describe the commit in brief detail such as “fixed bug where user name wasn’t updating” rather than a commit message like “some changes.”

touch .gitignore This will create a file called .gitignore. You can open that file with a text editor and write the name of files or folders you want to be ignored from your repository. Ignored files won’t show up when you run git status to prevent you from committing files you’ve previously said you don’t want to commit or even know about their changes.

`git branch branchName` Creates what is called a branch. A branch is a direct copy of your codebase from previous branch you were on (often the master branch).

`git checkout “branchName”` Will allow you to checkout the branch you created and work within that branch. You can make any changes to your code that you want here. When it’s ready, you can commit your code and push the branch to GitHub (see below) or you can delete the branch if something goes wrong or you decide you don’t need that feature or bug fix any longer.

`git merge branchName` While inside Master you can use this command to take the commits from the branch you were working in and merge them together with the main repository.

`git remote add origin https://github.com/userName/project.git` This adds the location of your remote repository. Everything up until now has been on your local repository on your computer. You will need to go to your GitHub account and create a new remote repository where you will be able to push your local repository. After you created your remote repository you will be provided with a link and that link is the location you will want to use in the above command.

`git remote` List of your remote repositories that have been associated with your project.

`git push -u origin master` This will push your local repository to your remote repository. This command only needs to be written like this when you do it for the first time.

`git push` This is what you will use to push your code to GitHub after your initial push.

`git clone https://github.com/userName/project.git` If you don’t have your project on the computer you’re working with this will allow you to clone (or download) the entire project into the directory you are working.

`git pull` If you are working on the same codebase with other people, this command will allow you to pull the latest version from the remote repository and update your local version so you can work with the latest updates as their changes enter the codebase

`git remote set-url origin git@github.com:USERNAME/REPOSITORY.git`, to change a remote origin url


`git diff-tree --no-commit-id --name-only -r bd61ad98` to list the inside commit

`git reset HEAD^` to remove the latest commit from the staging area

## Solving too big files in commit
This is a very irritating issue for sure. 
The first thing to do would be to identify the files that are too big:
1. `git status`
2. `git rm --cached *.extension of the file` - note that by using `*` it is possible to find all files with that file extension, irrespective of path, as git deals with that. 
3. `git reset HEAD^` will then remove the latest commit


## "Changes not staged for commit"
if on `git status` or otherwise, the above notice is produced, one can do the following to correct that:
`git add -a` to commit all changes!

## Changing from ssh to HTTPs

Open Terminal.
Change the current working directory to your local project.
List your existing remotes in order to get the name of the remote you want to change.

```
$ git remote -v
> origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
> origin  git@github.com:USERNAME/REPOSITORY.git (push)
```
Change your remote's URL from SSH to HTTPS with the git remote set-url command.

`$ git remote set-url origin https://github.com/USERNAME/REPOSITORY.git`

Verify that the remote URL has changed.

```
$ git remote -v
# Verify new remote URL
> origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
> origin  https://github.com/USERNAME/REPOSITORY.git (push)
```

## Changing from HTTPs to ssh


Open Terminal.
Change the current working directory to your local project.
List your existing remotes in order to get the name of the remote you want to change.

```
$ git remote -v
> origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
> origin  https://github.com/USERNAME/REPOSITORY.git (push)
```
Change your remote's URL from HTTPS to SSH with the git remote set-url command.

`$ git remote set-url origin git@github.com:USERNAME/REPOSITORY.git`

Verify that the remote URL has changed.

```
$ git remote -v
# Verify new remote URL
> origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
> origin  git@github.com:USERNAME/REPOSITORY.git (push)
```


## Large file storage and commit 
Something called git lfs (large file storage): 
https://git-lfs.github.com/


## Removing files from git history even if deleted
```git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch logs/debug.log" HEAD```
Say we would like to remove a debug.log file, then we can use the above command to erase it from the history, if it contains sensitivte information


# Production staging and development workflow
I have a programming project, and use git. Give me all the commands from commit to branch for a good workflow for development staging and production development
Here is a good workflow for using Git for development, staging, and production:

Start by committing your changes to your local repository:
Copy code
git add .
git commit -m "Commit message describing changes"
Push your changes to the development branch:
Copy code
git push origin development
Once your changes have been reviewed and tested, merge them into the staging branch:
Copy code
git checkout staging
git merge development
Finally, push your changes to the production branch:
Copy code
git push origin production
If you find issues or bugs in the production version, you can always create new branch from production, fix the issues and then merge it back to production.
Copy code
git checkout -b hotfix
#Fix the issues
git add .
git commit -m "Fixed production issues"
git checkout production
git merge hotfix
git push origin production
It's important to keep in mind that this is a basic workflow and can be adjusted to fit the specific needs of your project.




Ali Rassolie
Currently I only have one main branch, how would I setup all of these branches
If you currently only have one main branch, you can set up additional branches by following these steps:

Create a new branch for development:
Copy code
git branch development
Switch to the development branch:
Copy code
git checkout development
Make some changes and commit them:
Copy code
git add .
git commit -m "Initial commit for development branch"
Create a new branch for staging:
Copy code
git branch staging
Switch to the staging branch:
Copy code
git checkout staging
Create a new branch for production:
Copy code
git branch production
switch to the production branch:
Copy code
git checkout production
8.You can now work on these branches independently and merge them to the main branch when ready.

Copy code
git checkout development
#make some changes
git add .
git commit -m "Development changes"
git checkout main
git merge development
It's important to note that the main branch could be any name that you like, it is not necessary to be called "main", you can use any name that you want.
It's also important to note that you can do this steps in one command by using

Copy code
git checkout -b development
This command will create and switch to the new branch at the same time.




Ali Rassolie
how do I list all of the branches
You can list all of the branches in your local repository by using the command:

Copy code
git branch
This command will show all of the branches in your local repository, with the current branch marked by an asterisk (*).

You can also list all of the branches in your remote repository by using the command:

Copy code
git branch -a
This command will show all of the branches in your remote repository in addition to your local branches, with remote branches prefixed by "remotes/origin/".

To list all branches in your local and remote repository with the last commit date, you can use:

Copy code
git branch -av
This command will show all branches and the last commit date for each one, and it will also indicate the current branch with an asterisk (*)

You can also use this command to list branches in remote repositories:

Copy code
git ls-remote --heads origin
This command will list all branches in the remote repository "origin"

It's important to note that the name "origin" could be different depending on the remote repository that you have configured.




Ali Rassolie
I have a nextjs vercel project, one production environment and one staging environment. The staging environment needs to be linked to a staging branch, how do I create this
Here's one way to set up a staging environment for your Next.js Vercel project that is linked to a staging branch:

Create a new branch for staging:
Copy code
git branch staging
Switch to the staging branch:
Copy code
git checkout staging
Make some changes and commit them:
Copy code
git add .
git commit -m "Initial commit for staging branch"
Push the staging branch to your remote repository:
Copy code
git push origin staging
Go to your Vercel dashboard and create a new project for your staging environment.

In the settings, under the Git Integration section, select "Add Git Provider" and link your remote repository.

Select the staging branch from the dropdown list under the "Linked Branch" field.

Set up your environment variables and build settings as needed.

Press deploy, your staging environment will be deployed and will be linked to your staging branch, and every time you push a new change to the staging branch it will be automatically deployed to your staging environment.

It's important to note that the steps to link a branch in Vercel may vary depending on the version of the platform and the integrations you have set up. But the basic idea is that you should link the branch you want to deploy to the environment you want.

Also, it's important to keep in mind that you should have a different set of environment variables and configurations for each environment (production and staging) to avoid unexpected behaviors.
