#TD Ameritrade VEO
================

#Using Git

##Cloning the repository
	
	git clone https://github.com/emcconsulting/tdameritrade-veo.git
	cd tdameritrade-veo
	
##Starting your work

Update your local repository

	git checkout master
	git pull

Start your new feature branch, by convention use the jira issue, e.g. TVOAD-123

	git checkout -b TVOAD-123 master

if your feature needs a new branch you can append a descriptor e.g.

	TVOAD-123-fixtests
	TVOAD-123-hotfix
etc.

Each time you reach some point you can commit to your local branch

	git add .
	git commit -m "[TVOAD-123] Meaningful description of your change"

If there are changes inbetween, now is a good time to get them and solve conflicts with your code

	git fetch origin
	git rebase origin/master

If there are new changes, get the files from the main branch

	git checkout master
	git pull

you can rebase your local branch as much as you need to keep up with local changes.

##Commiting your feature

Once your feature has been completed, merge your chenges into remote branch 

	git checkout master
	git merge --no-ff TVOAD-123

Push your changes to the remote repo

	git push origin master

Your local branch can be safely deleted

	git branch -d TVOAD-123


##Solving Conflicts

Occasionally two developers work in the same file and there are conflicts when rebasing, example:

	CONFLICT (content): Merge conflict in app/dir/myfile.html
	Failed to merge in the changes.
	Patch failed at 0001 [TVOAD-123] homepage refresh

	When you have resolved this problem run "git rebase --continue".
	If you would prefer to skip this patch, instead run "git rebase --skip".
	To check out the original branch and stop rebasing run "git rebase --abort".

Conflicts are only in your local branch, so the will not break the workflow for others.

Conflicts are marked in the common files, you can use your IDE or 

	git mergetool
	
in order to make a decision on which lines should be modified.

After you made the changes to the conflicted files, add them to index:

	git add .
	git rebase --continue

**Summary** 

If you follow the steps in the workflow shown above, using a git repository viewer (e.g., [gitk](http://www.kernel.org/pub/software/scm/git/docs/gitk.html), [GitX](http://gitx.laullon.com/) or even just 

	git log --pretty=format:'%h : %s' --date-order --graph
	
You will be able to see that your work from the dev branch is kept together neatly. This is because the --no-ff option tells git to preserve the existence of the dev branch instead of removing that history and simply squashing all the work into the master branch. <!--In the image below, notice the three groups of work that are neatly grouped together. Each of these groups of work is a history of the fact that a dev branch did exist so that you can see all of the work that took place there visually and easily. If one of these groups of work needs to be backed out it is easy to see all of the commits in that group before backing them out.-->

If you don't follow this workflow, the work that took place on a dev branch will be interspersed amongst a bunch of other commits. This makes a quick visual inspection of the repository much more difficult. <!--In the image below, notice that there are commits from four different people. Commit 1 followed this workflow, but commits 2, 3 and 4 did not follow the workflow and were committed by three different people. Instead of being orderly and keeping each group of work together neatly as shown above, the work is scattered amongst a bunch of other commits from other people. This is because either a dev branch was not used at all or a dev branch was used but the --no-ff option was not used when performing the merge back to the maser branch.--> Without the --no-ff option when merging back to the master branch, the existence of a dev branch is not preserved and a quick visual inspection of the tree does not easily yield a quick understanding. If a group of work needs to be backed out, locating all the commits in a given group could be very difficult.


#### Changing your git username and email

**Please make sure to set your git username and email so that it reflects the correct info in your commits.**

You can set your git username in two different ways: 

* Globally for all repositories that you have cloned on your machine, or 
* Locally on a per repository basis 

Follow the steps below to understand how this works. 

**How to change your git username and email globally:**

    $ git config --global user.name "Spongebob Squarepants"
    $ git config --global user.email "robert.squarepants@vmware.com"

Now just list the user.name and user.email to check them:

    $ git config user.name
    Spongebob Squarepants
    $ git config user.email
    robert.squarepants@emc.com

**How to change your git username and email for a single repository:**

    $ cd /path/to/repository/on/local/disk
    $ git config user.name "Spongebob Squarepants"
    $ git config user.email "robert.squarepants@vmware.com"

Now just list the user.name and user.email to check them: 

    $ git config user.name
    Spongebob Squarepants
    $ git config user.email
    robert.squarepants@vmware.com

#### Git line endings

If you are on a UNIX line ending machine (Linux, Mac, etc.) please run the following from your command line:

    $ git config --global core.autocrlf input

If you are on a Windows line ending machine please run the following command from inside of your Git Bash window:

	$ git config --global core.autocrlf true

This configuration setting tells Git to checkout in your platform's line ending, but only to commit files with UNIX line endings.
For more info on line endings, see [Formatting and Whitespace from the Pro Git book](http://progit.org/book/ch7-1.html#formatting_and_whitespace).

#### Git Whitespace Changes

When git grabs files from a remote repo, it filters the files according to your local git preferences for line endings. This can result in line endings for a given file changing and 'git status' will report that the file has changed but 'git diff' won't show explicit changes. In this case, you would need to use a proper diff tool to see the whitespace changes along with the 'git difftool' command. 

### Git Resources

* [A succesful git model] http://nvie.com/posts/a-successful-git-branching-model/
* [Git Community Book](http://book.git-scm.com/)
* [Pro Git Book](http://progit.org/book/)

* [How To Add An Existing Git Project to Eclipse](http://bsnyderblog.blogspot.com/2012/01/how-to-add-existing-git-project-to.html)
*[Rebase Vs. Merge in git
] http://gitguru.com/2009/02/03/rebase-v-merge-in-git/






