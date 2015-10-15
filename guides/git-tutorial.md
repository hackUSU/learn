# hackUSU Git Tutorial

**A GitHub Account is required for this tutorial.** Please get one here: http://github.com/

## What is Git?
* Git is a Version Control System.

#### Git is like saving your work as you go.
* Every project evolves in little steps.
  * Added a Headline to a page.
  * Created about page.
  * Changed the layout of the page.
* Each one of these changes is essentially a new "version" of your project.
* You can save versions like you'd save information in a database.
* You can see the history of the file throughout it's creation.

#### Tracking Files In the Past
* People used folders. Lots and Lots and Lots of folders.
* This has MANY drawbacks
  * What **exactly** was changed?
  * What do these changes **mean**?
  * Why are we storing the **whole project** instead of just the modifications?
  * How do we keep variants of the project in **sync** while it moves on?

#### Git Saves Versions in a proper and professional way
* It saves the important information.
* It allows you to easily see the changes.
* You can restore previous versions and undo changes.
* Collaborate without overwriting each other!
* Every team member has a backup of the FULL project including the complete history of changes.

## Installation and Setup
Note: Some of you may have already done this. You can skip the install part.
* Download Git from the following link: https://git-scm.com/
* Install Git by running the file you just downloaded.
* To Verify you have git installed open a Command Prompt, Terminal, or PowerShell Window and type:
  * `git --version` - this should show you the current version of git you have installed.
* Installation is now complete!

## Configure Git
* We need to tell git who we are so it knows how to track our changes. (Note: You'll want to use your Github email for this part.)
* Let's tell git our user name - `git config --global user.name "John Doe"`
* Let's tell git our email address - `git config --global user.email "john@doe.org"`
* Let's tell git to use pretty colors if it can - `git config --global color.ui auto`

## Git Workflow
1. Creating or Cloning an existing project.
  * Create a new project on GitHub!
  * Click the **PLUS** sign in the top right of Github.com and click **Repository**
  * Name it whatever you want. I'll name mine **hackusu-git-tutorial**
  * Check the box **Initialize this repository with a README** - we want this file.
  * Click **Create repository**

**You've created your first git repository on Github's server!**

2. Let's clone or copy this project down to our computer.
  * On the main repository page, look for the **HTTPS clone URL** box and copy everything in there to your clipboard. This is the unique URL for the repository and the project.
  * Open a Terminal or Git Bash window and type:
    `cd ~` - this moves you to a location on your computer that isn't random. This is typically called your HOME directory.
    `mkdir projects` - this creates a folder called "projects" in your "home" directory.
    `git clone https://github.com/alexinslc/hackusu-git-tutorial.git`
  * You just copied the GitHub project to your computer!
3. Let's start playing with some git commands!
  * Enter the folder from the command line by typing: `cd <the name of your folder>` for example I'm using `cd hackusu-git-tutorial` - this puts the command line program INSIDE that folder so you can now see the files in it.
  * To see the files in the folder, type `ls`
  * Let's see what git "thinks" about these files. `git status` - shows us the status of the files in the directory. Here we see there's nothing that has changed.
  * Let's make a change to the README file.
  * Open the README file with any text editor and let's change the title.
    * README files use Markdown for formatting. Markdown is a quick way to type up documentation about your project.
  * Save your changes and go back to your command prompt.
  * Type `git status` again.
  * Now we see the README.md file has been modified. It's RED which means those changes have not been tracked. We need to track those changes!
  * Type `git add README.md` - This command adds the file to the git staging area. It's ready to be committed.
  * Another `git status` will show us that it's GREEN and ready to be committed to the repository.
  * Let's commit this sucker! Type `git commit -m "Changed the README file!"`
  * What's git think has happened? Type `git status`
  * We can see our "branch" is ahead of origin/master by 1 commit. This means the file is committed and it's ready to send to back to our remote GitHub repository so that our teammates can download our changes.
  * Let's push the changes up to GitHub! Type `git push` 
    * It may ask you for your GitHub username and password, go ahead and enter them.
    * Overtime, this can get really annoying. We need to add SSH keys so the GitHub server knows who we are. Let's do it!

## Setting Up SSH Keys for git and GitHub
1. We first need to generate a public and private key pair.
  * These are used to encrypt data and verify your identity on the GitHub servers.
  * To generate the key, type `ssh-keygen -t rsa -b 4096 -C "your_email@address.com"`
  * When it says "Enter file in which to save the key" - just hit ENTER.
  * When it says "Enter passphrase" - just hit ENTER.
  * It should spit out a fingerprint for your key.
2. Next we need to add our key to the ssh-agent.
  * Git Bash type `ssh-agent -s` - this will make sure the ssh-agent is now running.
  * Terminal type `eval $(ssh-agent -s)`- same thing as above
  * Let's add our key. `ssh-add ~/.ssh/id_rsa` - this adds it to the ssh-agent.
3. Finally let's add the key to our account.
  * In Git-Bash type `clip < ~/.ssh/id_rsa.pub` - this copies the key to your clipboard
  * Login to GitHub and click your profile photo, then click **Settings**.
  * In the user settings sidebar, click **SSH Keys**
  * Click **Add SSH key**
  * Name the key something that makes sense and then paste the key into the space provided.
  * Click **Add Key**.
  * Let's make sure it worked! In the terminal type `ssh -T git@github.com`
  * Woohoo! Now we don't have to type in our username and password every time we do a `git push` :) .
