git-kata
========

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

touch file02

echo "Salutations" > file02 # make a new file with some text in it

git add file02

git commit -m "Test for origin" # commit the change

git push origin # push the change to copy2

These pages may be helpful:  http://www.gitguys.com/topics/git-and-remote-repositories/

http://www.vogella.com/articles/Git/article.html