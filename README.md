git-kata
========

The purpose of this project is to provide a practice kata for several useful git functionalities.

## 1. Working with a remote repository

We'll start by initializing a repository and making a commit.

    mkdir copy1 # make a directory for the first repository
    cd copy1 # navigate into the directory
    touch file01 # make a file
    echo "Hello" > file01 # put some text into the file
    git init # initialize the repository
    git add . # add all files and directories to the repository
    git commit -m "Initial commit" # make your first commit

Now we will clone the repository.

    git clone --bare . ../copy2.git # clone copy1 into the remote repository copy2
    echo "Greetings" > file01 # make a change to the file
    git commit -a -m "A change" # commit the change
    git push ../copy2.git # push the change to the remote

There are several ways to push changes to the clone.

    git remote add origin ../copy2.git # associate copy2 with origin
    echo "Salutations" > file01
    git commit -a -m "Test for origin" # commit the change
    git push origin # push the change to copy2
    echo "Howdy" > file01
    git commit -a -m "Another commit"
    git push origin master # another way of pushing the change to copy2
    echo "Hey" > file01
    git commit -a -m "Yet another commit"
    git push origin master:master # yet another way to push

Finally, we will add a new branch to our repository and its clone.

    echo "We will make a new branch" > file01
    git commit -a -m "Commit for new branch"
    git push origin master:new-branch # push to a new branch on copy2
    git push origin :new-branch # delete the new branch

## 2. Resolving conflicts

We'll start by initializing a repository and making a commit.

    mkdir conflicts # make a directory for the repository
    cd conflicts # navigate into the directory
    touch file01 # make a file
    echo "Hello, World" > file01 # put some text into the file
    git init # initialize the repository
    git add . # add all files and directories to the repository
    git commit -m "Initial commit" # make your first commit

Add a branch and make different changes in master and the branch

    git branch branch1 # make a new branch
    echo "Greetings, World" > file01 # change the first word in master
    git commit -a -m "Change1" # commit the change
    git checkout branch1 # switch to the branch
    vim file01 # Substitute vim for your favorite text editor, and change "Hello, World" to "Hello, Earth"
    git commit -a -m "Change2" # commit the change

Try to merge branch1 into master

    git checkout master # switch to master
    git merge branch1

The auto merge will fail, so file01 will have to be edited manually

    vim file01 # substitute vim for your favorite text editor

The file will look like this:

    <<<<<<< HEAD
    Greetings, World
    =======
    Hello, Earth
    >>>>>>> branch1

Edit the file so it says "Greetings, Earth".

Merge the file into master

    git commit -a -m "Manual merge"

## 3. Working in a feature branch

We are going to model a setup where there is an official repository on github, from which you have your own fork,
with a clone of your fork on your local machine.

We'll start by initializing a repository and making a commit.

    mkdir official # make a directory for the first repository
    cd official # navigate into the directory
    touch file01 # make a file
    echo "Hello" > file01 # put some text into the file
    git init # initialize the repository
    git add . # add all files and directories to the repository
    git commit -m "Initial commit" # make your first commit

Clone the repository

    mkdir ../my-fork
    git clone . ../my-fork

Clone the repository again

    cd ../my-fork
    mkdir ../on-my-machine
    git clone . ../on-my-machine
    cd ../on-my-machine
    git remote add upstream ../official # set the upstream for on-my-machine

Now we have our 3 repos set up.  Imagine we are about to work on on-my-machine, and want to make sure it is up to date
with my-fork.  We can do a pull in order to get our master up to date, then start work on a branch.

    git pull --rebase
    git checkout -b feature1 # make and switch to a new branch
    echo "An update" > file01
    git commit -a -m "Update on new branch"

Imagine we are coming back later and want to make sure our branch hasn't fallen behind.

    git fetch upstream
    git rebase upstream/master # pulls any new commits from upstream and then rebases our work on top of them
    echo "Another update" > file01
    git commit -a -m "Update again"

Now we can push our work to github.

    git push origin feature1 # creates the branch on github (my-fork) and pushes our branch to it

The final step would be to create a pull request on github for branch feature1

This page may be helpful:  http://www.vogella.com/articles/Git/article.html