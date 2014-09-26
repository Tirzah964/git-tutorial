git-tutorial
============

##Tutorial
This is meant to be a tutorial on using Git. This tutorial assumes that you
already have git downloaded and installed and that you have a GitHub account.
To start this tutorial, fork this project on GitHub by clicking the fork button
on the top right.

###Basic Setup

1. Navigate to your fork of the tutorial on GitHub. It will be listed 
under repositories on your user page.
2. Copy the clone URL. (It appears on the lower right hand side)
3. Open command line. If you are in a lab computer you will have to use GitBash
4. Change directory to the one you wish to create your repo in; `cd <your working directory>`
5. Clone your repo with the url from step 2; `git clone https://github.com/<your username>/git-tutorial.git`
6. Change directory to your newly created project directory; `cd git-tutorial`

###Add a File

1. Create a new file in the project directory. Name it `new.cpp`
2. Copy this code into the file:
```
int main() {
   cout << "Hello World!";
   int i = 0;
   return 0;
}
```
3. In the command line type `git status`. You will see that the file `new.cpp` is currently untracked and needs to be added to git.
4. Type `git add new.cpp` to add the file to git.
5. Run `git status` again and note that `new.cpp` is now ready to be commited.

###Committing a file

6. Commit files to git with `git commit -m "Added new.cpp"`.
Note that you have not yet pushed the file back to GitHub. Git has stored the changes to your local repository but pushing these changes back to GitHub is done seperately.
7. Push your changes to GitHub by running the command `git push`
You will be prompted for your GitHub username and password.

###Modifing a file
1. Hello World is such a boring message. Change it to `"Hello World!!!!!!!"`.
2. Call `git add new.cpp` again to stage the file for commit. Note you can do 
`git add *` to add all changed files.
3. Commit and push exactly the same as we did [above](#committing-a-file)
but use a message of `"Added more exclamation points"` this time.

###Reverting
1. Your co-worker thinks that the extra exclamation points are excessive
and frankly poor English. Lets revert that change.
2. Run `git log` to view the recent commits.
Each commit will have its SHA-1 checksum (a 40 hex character string) listed which is used as an id.
You can revert specific commits by using their id numbers.
3. Run `git revert <ID of the exclamation point commit>`.
Note you only need to use the first few characters of the id.
5 characters should be fine.
4. Git will launch your default text editor for you to
write the commit message. Type a message and save this
file to finish reverting.
5. By default git automatically commits this revert.
All you have left to do is run `git push`

###Branching
1. To view all of the branches enter `git branch`
2. Lets add a new branch. Run `git branch "testing"`
This creates a testing branch.
3. To switch to the testing branch, type `git checkout testing`.
Note that you can switch back to the master branch at any time by running `git checkout master`. Wait, don't do that yet! We want to make some changes to testing first.
4. While we are in the testing branch, lets make some changes.
Change new.cpp to be:
```
int main() {
	cout << "Hello World!";
	int i = 0;
	
	if (i == 0) {
		cout << "All tests passed.";
	}
	return 0;
}
```
6. Stage the new.cpp file with `git add new.cpp`.
5. [Commit](#committing-a-file) these changes into the testing branch.

###Merging
1. Now it's time to bring our extremely effective tests back to the master branch.
First switch back to the master branch with `git checkout master`
2. Merge testing into master with `git merge testing`.
3. Run `git status`. Note that new.cpp is listed as being in conflict.
4. Lets open the file and resolve those conflicts.
The file should look something like this:
```
int main() {
	cout << "Hello World!";
	int i = 0;
<<<<<<< HEAD
=======
	
	if (i == 0) {
		cout << "All tests passed.";
	}
>>>>>>> testing
	return 0;
}
```
This tells us that the testing branch added the
code between the `<<<<<<< HEAD =======` and the `>>>>>>> testing`
5. Since we have no conflicts to resolve, lets just remove those markers.
```
int main() {
	cout << "Hello World!";
	int i = 0;
	if (i == 0) {
		cout << "All tests passed.";
	}
	return 0;
}
```
Note that you could also use a merging tool such as WinMerge to merge branches or files.
6. Type `git add *` to let git know you have finished merging the files.
7. Lets check the status again with `git status`.
Now it should say that all conflicts have been fixed.
8. Now all we have left to do is [commit](#committing-a-file) our merged changes.


