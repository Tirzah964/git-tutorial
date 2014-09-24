git-tutorial
============

##Tutorial

1. Fork this tutorial 

###Basic Setup

1. Navigate to the repository on GitHub
2. Copy the clone URL
3. Open command line
4. cd to your working directory
5. enter `git clone https://github.com/<Your Username Here>/git-tutorial.git` This will be the url you copied in step 2
6. cd into the project directory `cd git-tutorial`

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
You have not actually yet pushed the file back to github. Git stores the repository locally on your machine, but can also push your changes back to github
7. Push your changes to github by running the command `git push`
You will be prompted for your github username and password.

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
Each commit will have a id number (a long string of characters).
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
1. To view all of the branches type `git branch`
2. Lets add a new branch. Run `git branch "Testing"`
This creates a Testing branch.
3. To switch to the Testing branch, type `git checkout Testing`.
You can get back to the master branch at any time by running `git checkout master`
4. Now that we are in the Testing branch, lets make some changes.
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
5. [Commit](#committing-a-file) these changes into the testing branch.

###Merging
1. Now it's time to bring our extremely effective tests back to the master branch.
First switch back to the master branch with `git checkout master`
2. Merge Testing into master with `git merge Testing`.
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
>>>>>>> Testing
	return 0;
}
```
This tells us that the testing branch added the
code between the `<<<<<<< HEAD =======` and the `>>>>>>> Testing`
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
You could also use a merging tool such as WinMerge to merge branches or files.
6. Type `git add *` to let git know you have finished merging the files.
7. Lets check the status again with `git status`.
Now it should say that all conflicts have been fixed.
8. Now all we have left to do is [commit](#committing-a-file) our merged changes.


