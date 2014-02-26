## Practice 1.1

### Objectives:

- Create a repository: init
- Add and track changes to the repository: add, commit
- Remove files: add -u
- See repository changes over time: log
- Go back and forward in time
- Ignoring files with .gitignore
- Remove some change: reset


### Story:

We simulate the process of publishing a paper in a journal. We use git for tracking the evolution of the paper and deal with serveral eventualities.

### Start!:

- First day: We start writing the paper
	- create a folder for the paper (eg: practices/1.1) and a file called "article.txt" with text "first day"

- Turn this folder into a git repository
	- > git init
	- Note that:
		- a new hidden folder '.git' was created
		- we can type now 'git status': 'article.txt' is 'untracked'

- Say git to start 'tracking' this file: add + commit (c1)
	- > git add article.txt
	- Type 'git status': article.txt shows as in the list 'changes to be committed'
	- > git commit -m "a hard first day of work"

- Second day: write the 'Introduction' chapter of the article (c2)
	- edit article.txt and add a title '1. Introduction' followed by 10 lines (important) of dummy text. Remove text from first day.
	- > git add article.txt
	- > git commit
	- this time we don't add the comment in the command so git shows us a text editor for writing it. write this comment: "write the introduction" and exit the editor

- Third day: write the 'Methods' chapter (c3)
	- edit article.txt and add a title '2. Methods' followed by some dummy text.
	- > git add article.txt
	- > git commit -m "write the methods"

- Review evolution of repository (git log)
	- > git log -3

- Fourth day: write the 'Analysis' chapter and adds a 'plots' file (c4)
	- edit article.txt and add a title '3. Analysis' followed by some dummy text.
	- create a file called 'plots.txt' with some 'plot 1... plot 2' text
	- > git status
		- Note that 'article.txt' is 'modified' and 'plot.txt' is 'untracked'
		- see http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository for explanation on file states
	- > git add .
		- This time we 'stage' all the changes in the folder with 'git add .'. Add everthing (not ignored) to the 'staging' area
		- Alternative to 'git add article.txt plot.txt'
	- > git commit -m "write analysis and adds plots"

- Fifth day: change of mind, remove the plots (c5)
	- remove file 'plots.txt' from folder
	- > git status
	- plots.txt shows as 'deleted'
	- > git add -u .
	- '-u' needed to 'update the index' and track the 'deletion' of file
		- Note: more info on any command typing --help. eg: > git add --help
	- > git commit -m "remove the plots"

- Sixth day: writes 'Conclusion' and ignore a nasty file (c6)
	- edit article.txt and add a title '4. Conslusion' followed by some dummy text.
	- imagine we have edited the file with a software that creates some sort of 'configuration file' in our folder called 'nasty_file.ini'. eg: '.Rhistory' when working with RStudio
		- create a file called 'nasty_file.ini' with some dummy text
	- > git status
	- the file is 'untracked', if we make 'git add .' it will be added to the 'staged changes'
	- create a file called '.gitignore' with the content: 'nasty_file.ini'
	- > git status : doesn't show nasty_file.ini any more
	- commit .gitignore to the repo with message "write conclusions and ignore nasty file"

- Exercise on .gitignore
	- create a folder 'vendor' with two files 'lib1.R' and 'lib2.R'
	- ignore this: use 'vendor' in .gitignore

- Seventh day: you need to pick up one of the removed plots!! (c7)
	- we need to go back in time and pick what we removed

	- Method 1 (dirty): go back, copy and paste
		- > git log -5
		- find the 'hash' of the commit in which plots where added: 
		- go back in time
			- > git checkout 763abc
		- we are out of the 'master' branch
		- open 'plots.txt' and copy some of the content to some temporary file (wherever)
		- go forward in time (back to 'master' branch)
			- > git checkout master
		- create a file 'plots.txt' and paste the contents
		- commit changes

	- Learn to undo. But we don't like this method. Remove last commit (forever)
		- see commit hash of the previous commit "write conclusions and ignore nasty file"
		- > git log -2
		- > git reset COMMITHASH 
		- > git log -2 (again in c6)
		- remove plots.txt

	- Method 2 (nice): checkout some past file
		- git checkout COMMITHASH -- plots.txt
		- edit plots.txt remove what you don't want and commit changes with message "plot 2 back in time"

- Eight day: move plot to 'Analysis' chapter
	- apply learned stuff
		- make a commit with the 'plot 2' from plots.txt is in 'Analysis' chapter and remove plots.txt
	- commit with message "ready for peer review"