## Practice 2.1

### Objectives:

- configure the remote repositories
- learn basic push / 
- Create new folder (eg: practices/2.1)
cd 
- Create repoA:
	- Create a subfolder called "repoA" and make it a repository
		- > git init
	- Create a file inside (eg: work.txt). Leave empty
	- commit it
		- > git add .
		- > git commit -m "first commit"
	- Config repo to allow pushing on checked out branch (explain why)
		- > git config receive.denyCurrentBranch warn
		- why this? we are going to send code to the 'master' branch of this repo while it is checked out. This migth be dangerous, so it is disabled by default

- Create repoB:
	- Note: advised to do this in a different terminal window to stress the 'independence' of the repositories

	- back to practice folder (practices/2.1)
	- Create a subfolder called "repoB" and make it a repository (git init)
	- Configure for alowing receiving
		- > git config receive.denyCurrentBranch warn
	- Configure "repoA" as a remote repository for "repoA"
		- > git remote add repoA ../repoA/.git
	- Check that "repoA" is a remote
		- > git remote -v
	- Get all the contents from repoA
		- > git pull repoA master

- Send some update from repoB to repoA
	- (in repoB folder) edit work.txt and add this text: "update done in folder repoB"
	- commit this change with a message like "updated in repoB"
	- Push the current state of repoB into repoA
		- > git push repoA master

- See updates in repoA
	- go back to repoA terminal
	- > git log -2
		- shows the commit done in the repoB
	- open repoA/work.txt: the changes are not there!, why?
		- we have updated the repoA repository but not the working directory
		- 'git status' shows a change to be commited
		- 'git checkout -f' updates the working directory according to the branch last commit
git 
- Send some update form repoA to repoB
	- (in repoA folder) edit work.txt and add this text: "update done in folder repoA"
	- Configure repoB as a remote for repoA
		- > git remote add repoB ../repoB/.git
		- > git push repoB master

- See updates in repoB
	- go back to repoB terminal
	- > git log -3
	- > git checkout -f
	- open work.txt

- Create a repoC using clone
	- go back to practice folder and create repoC folder (eg: practices/2.1/repoC)
	- turn repoC folder into a git repository and config for allowing recieveing data
		- > git init
		- > git config receive.denyCurrentBranch warn

- Exercise
	- Insert modification in repoB/work.txt
	- Must apply this changes in repoA BUT without push/pull from/to repoB/repoA
	- trainees must (one option):
		- make modification in repoB/work.txt
		- configure repoC as remote for repoB
		- push from repoB to repoC
		- configure repoA as remote for repoC
		- push form repoC to repoA


- Deal with conflicting push
	- repoA and repoB must be syncronzed after last exercise
	- edit repoA/work.txt
		- add text line "second update in folder repoA"
		- commit this change as "second update in repoA"
	- go to repoB and edit repoB/work.txt
		- add text line "third update in folder repoB"
		- commit this change as "third update in repoB"
	- (on repoB folder) try to push from repoB to repoA
		- > git push repoA master
		- get error becouse we are stepping on some not merged work
	- need to pull remote changes first
		- form repoB
		- > git pull repoA master
		- might find a conflict in merging with remote: fix it
		- commit as "merged with repoA. fix conflict"

- Go to repoA and see the changes there