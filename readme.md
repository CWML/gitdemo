# **Git & GitHub: An Introduction to Version Control**
In this repository you will find all workshop materials.
Powerpoint file is included and the hands on portion of the class is located below in the [Git Fundamentals](#Git-Fundamentals) section.


**Learning Objectives**

- Benefits & basics of a Version Control System 
- Differences between git and GitHub 
- About remote repositories and why they are useful 
- How to use git in the terminal to initialize, add, and commit files to a repository 
- Publish a repository to GitHub.com 
- Overview of GitHub.com & GitHub desktop 
- What git clone is and how to clone a remote repository in the terminal & desktop application 
 
**Required software/accounts:**
 
github.com account:<br>
https://github.com/signup
 
If you are bringing your own laptop, you will need to install the following:
 
GitHub Desktop:<br>
  https://desktop.github.com/
 
Windows only:<br>
Git bash is required and installed via Git below<br>
Git installer 64 bit direct link:<br>
https://github.com/git-for-windows/git/releases/download/v2.45.2.windows.1/Git-2.45.2-64-bit.exe<br>
You can just click (several pages) through this installer to accept all of the defaults. 
 
Mac only:
X-Code Developer tools<br>
Open the Terminal application, which you can find in your Applications > Utilities folder or by searching with Spotlight.<br>
Type the following command and press Enter:<br>
```
xcode-select --install
```
Follow the on-screen instructions to install the Command Line Tools.<br>
This can also be installed via the app store via the 'Xcode' app.







# **Git Fundamentals**
This readme file is the hands on portion of the class!

## Creating a Repository

First let's change directory or cd to our desktop and then create our working directory:

```
cd ~/Desktop
mkdir planets
cd planets
```
Then we tell git to make planets a repository -- a place where git can store versions of our files:

```
git init
```

It is important to note that git init will create a repository that can include subdirectories and their files—there is no need to create separate repositories nested within the planets repository, whether subdirectories are present from the beginning or added later. Also, note that the creation of the planets directory and its initialization as a repository are completely separate processes.
If we use ls to show the directory’s contents, it appears that nothing has changed:

```
ls
```
But if we add the -a flag to show everything, we can see that Git has created a hidden directory within planets called **.git**

``` 
ls -a
```

Git uses this special subdirectory to store all the information about the project, including the tracked files and sub-directories located within the project’s directory. If we ever delete the .git subdirectory, we will lose the project’s history.



Next, we will change the default branch to be called main. This might be the default branch depending on your settings and version of git. 
```
git checkout -b main
```
We can check that everything is set up correctly by asking Git to tell us the status of our project:

```
git status
```
## Tracking Changes

First let's confirm our working directory
```
pwd
```
Let’s create a file called mars.txt that contains some notes about the Red Planet. We’ll use nano to edit the file.
```
nano mars.txt
```
```
Add text: Mars is the 4th planet from the Sun.
```
Let’s first verify that the file was properly created by running the list command (ls):
```
ls
```
mars.txt contains a single line, which we can see by running:
```
cat mars.txt
```
If we check the status of our project again, Git tells us that it’s noticed the new file:

``` 
git status
```
The “untracked files” message means that there’s a file in the directory that Git isn’t keeping track of. We can tell Git to track a file using git add:
```
git add mars.txt
```
and then check that the right thing happened:
```
git status
```
Git now knows that it’s supposed to keep track of our selected file, but it hasn’t recorded these changes as a commit yet. To get it to do that, we need to run one more command:
```
git commit -m "Start notes on mars in mars.txt"
```
When we run **git commit**, Git takes everything we have told it to save by using git add and stores a copy permanently inside the .git directory. 
This permanent copy is called a commit (or revision) and its short identifier is listed in the brackets []. 

We use the **-m** flag (for “message”) to record a short, descriptive, and specific comment that will help us remember later on what we did and why. If we just run **git commit** without the **-m** option, Git will launch nano (or whatever other editor we configured as core.editor) so that we can write a longer message.

Let's check our **git status** again:
```
git status
```

You can also add multiple files at one time.  First we will create a new folder:
```
mkdir moons
```
Git's design philosophy is to track content (files) rather than empty directories. This ensures that the repository remains lightweight and efficient, only tracking actual data changes

Here we'll use the **touch** command to create 2 files inside of the moons directory:
```
touch moons/phobos.txt moons/deimos.txt 
```
Let's see check out status:
```
git status
```
Now we'll add the files:
```
git add .
```
What does the status show now?
```
git status
```

Adding files to track is great, but what if we don't want to track a file?  We can create a **.gitignore** file that lists files git will ignore.  We'll do that now as well as add the file we want to ignore:
```
touch stars.txt
touch 1.o 2.o 3.o
mkdir logs
nano .gitignore
```
Add the following to to **.gitignore**:
```
stars.txt
*.o
logs/
```

Now let's check check our directory and **git status**:
```
ls -a
git status
git add .
git status
```

Now that we have more files tracked or not tracked, we'll need to commit those changes:
```
git commit -m "Update mars.txt and add moons directory. .gitignore updated"
```

If we run **git status** now:
```
git status
```
It tells us everything is up to date. If we want to know what we’ve done recently, we can ask Git to show us the project’s history using git log:
```
git log
```
**git log** lists all commits made to a repository in reverse chronological order. The listing for each commit includes the commit’s full identifier.

## Publish a repository to GitHub.com

**This requires authorizing with GitHub.**

In order to push our repository to github.com we need to authenticate with our account via SSH.

Let's check if we have ssh keys already.
```
ls ~/.ssh
```
In your terminal, run the following command to generate an ssh key to use with GitHub.com.

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
If you are using a legacy system that doesn't support the Ed25519 algorithm, you can use:
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

When prompted to "Enter a file in which to save the key," press Enter to accept the default file location.

Next, you'll be prompted to enter a passphrase. This is optional but recommended for added security. You can press Enter to skip creating a passphrase.

Run the following command to start the SSH agent:

```
eval "$(ssh-agent -s)"
```

Add your SSH Private key to the SSH agent:

```
ssh-add ~/.ssh/id_ed25519
```

Now we need to add the key to our GitHub account, but first we must copy our public key using pbcopy.

Run the following command to copy the key to your clipboard:
```
pbcopy < ~/.ssh/id_ed25519.pub
```
**For Windows:**
In Git Bash:

Type the following command and press Enter:
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Follow prompts, press enter to save at default location. 
Press enter for an optional passphrase.

Start the SSH agent by running the following command:
```
eval "$(ssh-agent -s)"
```
Add your SSH private key to the SSH agent with this command:
```
ssh-add ~/.ssh/id_rsa
```

Copy the contents of your public key to the clipobard.

```
cat ~/.ssh/id_rsa.pub | clip
```

How to add to github account.

1. Go to GitHub and log in to your account.
2. In the upper-right corner, click on your profile photo, then click 
3. Settings.
4. In the left sidebar, click SSH and GPG keys.
5. Click New SSH key or Add SSH key.
6. In the "Title" field, add a descriptive label for the new key.
7. Paste your key into the "Key" field.
8. Click Add SSH key.
9. If prompted, confirm your GitHub password.

Run the following command to test your connection:
```
ssh -T git@github.com
```

Now we'll push our repository to github.com.  First we need to create the repository on github.com and then we run the following command(use your repository command):
```
git remote add origin https://github.com/username/yourrepohere.git
```
We confirm we're on the right branch:
```
git branch -M main
```
Now we can push our local .git repository to our remote repository.
```
git push -u origin main
```

If there are issues adding via git remote add(due to authorization) you can add an existing repository via GitHub Desktop and then publish that repo to GitHub.com

We can now see our published Repo on github.com

## Workflow type
Remote first or local repo first?

## Clone a repository

Next we'll clone a repository.  There are several ways to achieve this but most commonly will be from the command line.  If a repository is not public you will need to authenticate with GitHub.com and have access before you can clone it.

```
git clone https://github.com/CWML/gitdemo
```

**GitHub Pages application:**
https://miku.github.io/activememory/

**GitHub Repo:**
https://github.com/miku/activememory

**GitHub Desktop/Website overview**
Covered in class.

**GitHub Documentation**<br>
https://try.github.io/<br>
**GitHub Cheat Sheet**<br>
https://training.github.com/downloads/github-git-cheat-sheet.pdf<br>
**Software Carpentry Git Novice workshop**<br>
https://swcarpentry.github.io/git-novice/<br>
**Yale Research Computing Git Workshop Video Recording**<br>
https://research.computing.yale.edu/training/version-control-git<br>
**REDCap@Yale's Developer Handbook git Intro**<br>
https://yale-redcap.github.io/developers-handbook/orientation/git-intro/<br>
**Distributed Workflows from Pro Git (Version 2) https://github.com/progit/progit2**<br>
https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows<br>
**git Large File Storage**<br>
https://git-lfs.com/<br>
**git.yale.edu**<br>
Data Classification : Moderate<br>
[Yale GitHub Enterprise Service Page](https://yale.service-now.com/it?id=service_offering&sys_id=bc29b84997f88a506f0430671153af28&table=u_service_offering_index)