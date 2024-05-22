# **Git Fundamentals**

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
nano .gitignore
```
Add stars.txt to .gitignore
Now let's check check our directory and git status:
```
ls -a
git status
git add .
git status
```

Git now knows that it’s supposed to keep track of our selected files, but it hasn’t recorded these changes as a commit yet. To get it to do that, we need to run one more command:
```
git commit -m "Start notes on Mars and create the moons directory"
```
When we run **git commit**, Git takes everything we have told it to save by using git add and stores a copy permanently inside the .git directory. 
This permanent copy is called a commit (or revision) and its short identifier is listed in the brackets []. 

We use the **-m** flag (for “message”) to record a short, descriptive, and specific comment that will help us remember later on what we did and why. If we just run **git commit** without the **-m** option, Git will launch nano (or whatever other editor we configured as core.editor) so that we can write a longer message.

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

No we'll push our repository to github.com.  First we need to create the repository on github.com and then we run the following command(use your repository command):
```
git remote add origin https://github.com/j-demayo/folder.git
```
We confirm we're on the right branch:
```
git branch -M main
```
Now we can push our local .git repository to our remote repository.
```
git push -u origin main
```

If there are issues adding via git remote add you can add an existing repository via GitHub Desktop and then publish that repo to GitHub.com

We can now see our published Repo on github.com

Now let's clone a repository.  There are several ways to achieve this but most commonly will be from the command line.

```

```
