# learn-git
For educational purpose only

```commandline
# on Linux (fedora, ubuntu)
sudo dnf install git
sudo apt install git

# on Windows : https://git-scm.com/download/win
```

## fork
```commandline
# fork a repository by clicking 'fork' from the owner's repo,
# then a copy of the repo will be appear in your account

# now clone the forked repo
git clone https://github.com/fggo/Parking.git
cd ./Parking  # now on (master)
git remote -v
    origin  https://github.com/fggo/Parking.git (fetch)
    origin  https://github.com/fggo/Parking.git (push)

# add upstream(original repository from the owner)
git remote add upstream https://github.com/YoonYeoSong/Parking.git
git remote -v
    origin  https://github.com/fggo/Parking.git (fetch)
    origin  https://github.com/fggo/Parking.git (push)
    upstream  https://github.com/YoonYeoSong/Parking.git (fetch)
    upstream  https://github.com/YoonYeoSong/Parking.git (push)

git config --global user.name 'junholee'
git config --global user.email 'jnuho@outlook.com'

# fetch the changes from original repo and it will
# store the changes in the branch 'upstream/master' of your forked repo
git fetch upstream

# merge the branch
git checkout master
git merge upstream/master

# now push my changes to make my forked repo is up-to-date
# it only updates the forked repo(copy)
git push origin master

# now go to original repo,
# click pull request -> create pull request

# now original owner of repo can confirm 'merge pull request'
# ALL DONE!
```

## branching
```commandline
git branch junk/testbranch
git checkout junk/testbranch
# changes made
git add *
git commit -m 'branch commit'
git push origin junk/testbranch
# remote branch name has been set as same 'junk/testbranch'
# one can change different remote branch name
# git push origin local-branch-name:remote-branch-name

git checkout junk/testbranch
git pull origin junk/testbranch # git pull origin remote_branch
git checkout master
git pull origin master # git pull
git merge --no-ff --no-commit test

git status # resolve merge conflict

git commit -m 'merge test branch, junk/testbranch'
git push

```

REMOTE REPO 'origin' <-> LOCAL
```commandline
git clone https://github.com/github_user/repo_name.git
cd repo_name

# local -> remote
mkdir -p $HOME/repo_name
cd $HOME/repo_name
git init
git remote add origin https://github.com/github_user/repo_name.git

# after making changes : 
git add '*'  #ADD TO STAGE
git commit -m 'Add all local files' 
git push -u origin master

git show HEAD //latest commit log

git checkout HEAD filename //discard changes and restore back to the last commit
git checkout -- filename  //does the same thing as 'checkout HEAD'

git add scene-2.txt
git reset HEAD scene-2.txt //unstage file from the staging area using
// It does not discard file changes from the working directory, 
// it just removes them from the staging area.

git reset commit_SHA //undo commits

git reset commit_b_SHA
//Before reset :  a-b-c-d-HEAD
//After reset :  a-b-HEAD

git diff HEAD
git diff --staged
git reset octofamily/octodog.txt    #unstaging
git checkout -- octocat.txt
git branch clean_up

git branch //check what branch is it currently

git branch bugFix // create new branch
git checkout bugFix //switch to new branch

git checkout -b bugFix //create & switch to new branch at the same time
// you can make commits on the new branch that have no impact on master.

git checkout master
git merge bugFix
// merge the new branch bugFix(giver) into master(receiver) branch
// no merge conflict since master had not changed

git checkout bugFix
git merge master //merge master into bugFix

// Since bugFix was an ancestor of master, 
// git didn't have to do any work; it simply just moved bugFix 
// to the same commit master was attached to.

// Now all the commits are the same color, 
// which means each branch contains all the work in the repository!


// merge conflict : 
//  <<<<<<< HEAD
//  master version of line
//  =======
//  fencing version of line
//  >>>>>>> fencing

git add conflict_file_name
git commit -m 'merge conflict resolved'

git branch -d branch_name //delete branch after merged to 'master' branch

//  Imagine that you’re a science teacher, developing some quizzes with Sally, 
//  another teacher in the school. You are using Git to manage the project.
//  To collaborate followings are required :
//  A complete replica of the project on your own computers
//  A way to keep track of and review each other’s work
//  Access to a definitive project version

//  You can accomplish all of this by using remotes. 
//  A remote is a shared Git repository that allows multiple 
//  collaborators to work on the same Git project from different locations
//  Collaborators work on the project independently, 
//  and merge changes together when they are ready to do so.

//  Sally has created the remote repository, science-quizzes 
//  in the directory curriculum, which teachers on the school’s shared network 
//  have access to. In order to get your own replica of science-quizzes, 
//  you’ll need to clone it with:
//  remote_location = file_path or web address(url)
git clone remote_location clone_name
git clone science-quizzes my-quizzes
cd my-quizzes

//  list of a Git project’s remotes with the command:
git remote -v


//  Sally changed the science-quizzes Git project in some way. 
//  If so, your clone will no longer be up-to-date.
//  An easy way to see if changes have been made to the remote 
//  and bring the changes down to your local copy is with:
git fetch

//  Even though Sally’s new commits have been fetched to 
//  your local copy of the Git project, those commits are 
//  on the origin/master branch. 
//  Your local master branch has not been updated yet, 
//  so you can’t view or make changes to any of the work she has added.

//  In Lesson III, Git Branching we learned how to merge branches. 
//  Now we’ll use the git merge command to integrate origin/master 
//  into your local master branch. The command:
git merge origin/master


//  Git has performed a “fast-forward” merge, 
//  bringing your local master branch up to speed 
//  with Sally’s most recent commit on the remote.

//  In the output, notice that the HEAD commit has changed. 
//  The commit message now reads same as Sally's
git log


//  Now that you’ve merged origin/master into your local master branch, 
//  you’re ready to contribute some work of your own. The workflow for Git 
//  collaborations typically follows this order:

//  1. Fetch and merge changes from the remote
//  2. Create a branch to work on a new project feature
//  3. Develop the feature on your branch and commit your work
//  4. Fetch and merge from the remote again 
//      (in case new commits were made while you were working)
//  5. Push your branch up to the remote for review

//  Steps 1 and 4 are a safeguard against merge conflicts, 
//  which occur when two branches contain file changes that cannot 
//  be merged with the git merge command. Step 5 involves git push, 
//  a command you will learn in the next exercise.

```
![git checkout master](merge1.jpg)
![git merge bugFix](merge2.jpg)
![git checkout bugFix; git merge master](merge3.jpg)
