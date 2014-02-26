## Practice 1.2

### Objectives

- Create and move through branches
- Merge branches
- Fix merge conficts

### Story

Now the article for sending to a journal. We will track the particular modifications they ask us using git 'banches'

### Start

- Read 'Journal of Good Science' reply: rejected

- First day: prepare the paper for 'Journal of Better Sciene'
	- what is a branch? --> explain
	- create a 'branch' for the adapted version of the paper for this particular journal
	- > git branch
		- shows the branches we have: master
	- > git checkout -b jobs
		- crates and moves to a new branch called 'jobs' for the journal
		- any commit will go to this branch (not to master)
	- Adapt paper to J.O.B.S. policies:
		- Introduction must have just 2 lines
		- Must come with a file 'data.txt' with 'Data Anexes'
		- make changes and commit (in branch jobs) as "adaptation to jobs journal policy"
	- > git log -3

- Second day: Read 'Journal of Better Science' reply: rejected
	- Also they point out that you have a typo in line 3 of 'Analysis'
	- go back to master branch, fix the typo and commit it (in master)
		- > git checkout master

- Third day: prepare the paper for 'Journal of Awesome Science'
	- create a branch for 'joas' based on branch 'master'
		- > git checkout master
			- back to 'master' branch
		- > git checkout - b joas
		- > git branch
			- see all three
	- Adapt paper to J.O.A.S. policies:
		- 4 lines introduction. Must rewrite lines. Different text
		- Add chapter 5. Thanks to
		- Must add a file with the cvs of the authors called 'authors.txt'. 
		- Add it and commit (in joas)
		- Must add a file with the data set: data.txt created for 'jobs'
			- Need to merge with changes in 'jobs'
			- > git merge jobs
			- !!! CONFLICT: becouse the same lines in article.txt are modified in the other paralell version
			- note that file 'data.txt' is in place
		- Fix confilct
			- edit article.txt
			- note how conflict is shown in the introduction
			- note there is no conclict in '5. Thanks to'
			- edit and commit as "adaptation to joas journal policy"
	- Send to JOAS ....

- Fourth day: Read 'Journal of Awesome Science' reply: ACCEPTED!
	- Apply all changes in joas branch to master branch
		- > git checkout master
		- > git merge joas
			- messages says "Fast-forward". 'master' is not merging just moving on in time
		- (optional) remove branch 'joas' (now it is merged)
			- > git branch -d joas
		- (optional) remove branch 'jobs'
			- > git branch -d jobs
