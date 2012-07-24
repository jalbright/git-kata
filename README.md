git-kata
========

## 1. Working with a remote repository

    mkdir copy1 # make a directory for the first repository
    cd copy1 # navigate into the directory
    touch file01 # make a file
    echo "Hello" > file01 # put some text into the file
    git init # initialize the repository
    git add . # add all files and directories to the repository
    git commit -m "Initial commit" # make your first commit
    git clone --bare . ../copy2.git # clone copy1 into the remote repository copy2
    echo "Greetings" > file01 # make a change to the file
    git commit -a -m "A change" # commit the change
    git push ../copy2.git # push the change to the remote
    git remote add origin ../copy2.git # associate copy2 with origin
    echo "Salutations" > file01
    git commit -a -m "Test for origin" # commit the change
    git push origin # push the change to copy2
    echo "Howdy" > file01
    git commit -a -m "Howdy"
    git push origin master # another way of pushing the change to copy2
    echo "Hey" > file01
    git commit -a -m "Hey commit"
    git push origin master:master # yet another way to push
    echo "We will make a new branch" > file01
    git commit -a -m "Commit for new branch"
    git push origin master:new-branch # push to a new branch on copy2
    git push origin :newbranch # delete the new branch
These pages may be helpful:  http://www.gitguys.com/topics/git-and-remote-repositories/

http://www.vogella.com/articles/Git/article.html