# github
how to use this space

Here is a good article: https://medium.com/anne-kerrs-blog/using-git-and-github-for-team-collaboration-e761e7c00281

About Branches and Merging
A branch is a point-in-time copy of your main project branch that can be worked on in isolation, then later merged back into the master project branch. Branches allow collaborators to work separately without stepping on each others’ code, and to test their changes against the main branch to resolve any conflicts before merging their contribution into the project.
Git knows about changes made to each file it tracks. If the same tracked file is changed in two branches, a merge conflict may arise. If Git can merge the two files without conflict it will do so. E.g., if one person added function a and another person added function b, there will be no conflict. Both functions will exist in the merged file. If, however, both people modify function c, and the changes conflict, it may not be possible for git to know which changes save. In this case, Git will create an edited version of the file with both changes highlighted and a person must decide what to include in the final file.
This can cause additional confusion, especially if you are new to the process. Coordination and communication with other developers up front is the best way to avoid this confusion. Avoid working on the same files where possible.
Terminology
master is a branch name. By default, when you first create a repo on GitHub, the first branch is called ‘master.’
origin is a reference to a repository, usually the repository on a remote computer from which the local branch has been created.
When you execute:
$ git push origin your_branch_name
…you are pushing local code to the repo pointed to by origin, and creating a new branch on that repo with your branch name. From there you would have to issue a ‘pull request’ to merge your branch into master.
remote refers to a repo on some other computer, such as GitHub. This is configured in the hidden .git/config file, where .git is a hidden folder at the root level of each local repo.) Most projects will have both a remote master (from which you typically ‘clone’ your branch) and a local ‘master’ (which may be out of date with the remote, if someone else has merged in code after you created your local copy.) The remote repo from which you ‘clone’ is given the alias ‘origin.’
Git Workflow and Commands
Git commands are issued from the local command line and can interact with the local or the remote system. The specific commands are discussed in the context of a typical workflow. Workflow actions include creating a new repo, cloning a repo, saving work-in-progress locally, pushing work the GitHub, and merging with the main branch.
Team Workflow Decisions
There are a few configuration options to make when setting up the project repo. Discuss these with your team and decide how you want to work together.
Require pull requests
A ‘pull requests’ is issued by a developer who has completed work on a branch and would like to have it merged into the main code branch. Requiring pull requests is a configuration option. Without a pull request, developers can push directly to the main branch, and if there are no conflicts, the code is automatically merged. Requiring pull requests is an extra step, but it ensures communication among team members and helps prevent potentially disastrous mistakes. I highly recommend it, especially if your team is new to the process.
Set number of reviewers
Defining who can review and accept a pull request, and how many reviews are required, is another configuration option. If you are using pull requests, require at least one review, and at least one reviewer. In my experience, it was sufficient to require one review, and we set it up so any team member could perform that review. It was flexible enough that we weren’t waiting for any one person, but gave us checkpoint we needed to bypass automatic (and possibly accidental) merges to the main branch.
branch naming conventions. (e.g., name/feature)
Branch names can be anything, but it is good practice to have a naming convention that identifies the developer and the feature they are working creating or modifying. E.g., on one project our convention was: name/feature. When I created a branch to update a news reader I called it: anne/news.
Communication and coordination
No source control system is a replacement for good communication among team members. Know who is working on what files, and avoid making git resolve conflicts for you, if possible.
A word of caution about Jupyter notebooks: Because they are text files, Git will insert conflict markers if it finds a conflict, just like with any other code file. Ipynb files with these markers cannot easily be edited by Jupyer or a code editor. There are articles on the web about how to address these issues, but the simplest approach is to avoid them in the first place by ensuring only one person works on a notebook at a time.
Installation and Setup
If you have not already done so, you will need to install Git on your local computer and sign up for a free GitHub account. Downloads and instructions can be found at these links.
Download and instructions for installing Git.
Sign up for a free GitHub account
Once you (and your team) have Git installed locally and have each created GitHub accounts. You are ready to start.
Create a New Repository on GitHub
Note: Only one repo is needed on GitHub, so only the team member who will host the repo on their GitHub account should perform this step.
On GitHub, under ‘Your Repositories’:
Press the green New button.
Fill in the Repository Name
Provide an optional description
Other things to configure when setting up your repo:
Select whether you want it to be private or public
Select the checkbox to initialize the new repo with a README (The README is the front page of your repo and should summarize the project. Having a README in place will keep you from having an empty project. You can edit or replace the README later.)
Select whether or not to include a .gitignore file. (File names and patterns listed in the .gitignore file will not be tracked by git. It is useful to list temporary files you know will be created during your project but that you don’t want to track in your repo. E.g., Jupyter notebook checkpoint files.)
GitHub will prompt you to create your local git repo several different ways. I prefer to initialize a copy of the newly created GitHub repo by cloning it to my local hard drive, then copying or creating content. Copy the URL shown in the first option:
Quick setup — if you’ve done this kind of thing before
Clone the New Repository to your Local Machine(s)
Note: Each team member will need to perform this step.
On GitHub, navigate to the project repo:
Press the green Clone or download button.
Ensure that clone with HTTPS is selected. (If you setup GitHub to use SSH key and passphrase, you may select that option, but these instructions assume you are using HTTPS.)
Copy the URL provided.
In your local terminal, from the top level folder under which you want to place your repo:
$ git clone paste-copied-url-here
NOTE: Be careful not to issue this command from a directory already being tracked by git. Do a git status first to verify. You see something like this message fatal: not a git repository (or any of the parent directories): .git This means it is safe to clone.
Create and Checkout a Local Branch for Your Work
Each contributor should create their own local branch for their work. This new branch will be a copy of the main branch.
Navigate to the top directory of the repo you just cloned. The ‘master’ branch should be active.
Check which branch is active using the command:
$ git branch
Create a new branch, giving it a name consistent with the naming conventions developed by your team.
$ git branch your_branch_name
Check out the new branch. It will create a copy of the cloned master and set the current working branch
$ git checkout your_ branch_name
Alternately, you can check out and create the new branch in one command:
$ git checkout -b your_branch_name
Save Incremental Changes Locally
It is a good idea to save versions of your work frequently. Do this with the ‘git commit’ command. The process involves staging the work you want to ‘check in’, using the ‘git add’ command, then using ‘git commit’ to tell Git to save the staged changes. Git keeps track of each commit batch and allows you to roll back to any prior commit if necessary. You can repeatedly ‘git add’ and ‘git commit’ in your local environment without ever pushing to GitHub. You may want to occasionally ‘git push’ unfinished code to GitHub (without doing a pull request) to have a backup copy, but it is good practice to merge to the master branch only code that has been tested and ready for release.
Use the ‘git status’ command to check what files have changed, what files git is tracking, and what files have been staged for commit:
$ git status
Git will notice new files and let you know they are not yet being tracked.
Use the ‘git add’ command to add a file to staging. Do this to add a new file to Git or to add a modified file to staging:
$ git add your_file_name
A word of caution. You can do ‘git add -a’ to add all the files in the tracked directory, including subdirectories, to staging. However, there may be files you do not want to track, such as temporary files created by you or by the software you use. For this reason, I would caution against using the -a option.
You can create a .gitignore file to tell Git to always ignore certain files. I will not cover that here, but you may wish to investigate on your own.
Remove Files from Git To remove a file. This removes the file from git and the branch:
$ git rm your_file_name
Commit the Staged Files When you have added the files you wish to have Git save to staging, you are ready to issue the ‘git commit’ command.
$ git commit -m'descriptive message here'
Use the message parameter (-m) to provide a descriptive message for the set of files being committed. It is good practice to be as explicit as possible. This will be available in the commit history and will be helpful if you want to review or roll back older files, and should also give reviewers meaningful information about what is contained in the code.
Push Changes to GitHub
Here is where team communication comes into play. Has anyone updated the main branch on GitHub since you created your branch? Are there likely to be conflicts? If so, it is much easier for you to ‘rebase’ your local code by fetching a new copy of the master branch and resolving any conflicts locally. If others are doing this at the same time it could get even messier. To avoid problems, let your team-mates know what you are doing and coordinate pushes and pulls.
Pushing your code to GitHub If you need to rebase, follow the steps below before coming back to this step.
$ git push -u origin your-branch_name
This pushes your changes upstream (-u) to the repo pointed to by origin and creates a copy of your branch in the repo on GitHub.
To push again to this same branch, use the ‘git push’ command from within the active branch, without any additional parameters. (If you are doing this subsequent times, GitHub already knows about the branch because you created it previously.) You would do this if you wanted to push more work and use GitHub as a backup, before doing the Pull Request.
$ git push
Note: Once your branch has been merged into the master, you don’t want to use that branch name again. If you are going to continue working on the project, create a new branch as described previously.
Create a Pull Request to ask for the code to be merged into the main (master) branch on GitHub.
On GitHub, navigate to the branches tab.
Issue Pull Request Locate your named branch and select the ‘New Pull Request’ button.
Select Reviewers From the list of reviewers, select whom you would like to review this request. Each reviewer will get an email notification of your request. If your workflow only requires one review, and you select multiple reviewers, any one of them will be able to approve the request.
Reviewers The reviewer has the option to approve the request, deny the request, or ask for changes. If the request is approved, the reviewer can choose to merge the code at that time or ask the requester to do the merge. This decision should be made based on whom you want to perform any merge conflicts that may arise. Ideally, precautions will have been taken to handle any conflicts prior to this point, but there is no guarantee.
Other Tasks
Rebase with the current version of GitHub
If others have pushed to GitHub since you created your local branch, you may want to bring a fresh copy of the master branch to your local system to resolve conflicts prior to pushing your code to GitHub. This is called ‘rebasing’. It is easier to resolve conflicts locally than if occur while pushing to GitHub.
Refresh your local git environment with what is on GitHub.
$ git fetch
Note: The above brings down the current copy of the master branch to your git environment, but does not update your local master branch.
Rebase to add your commits (the changes you have checked-in locally) to the head of the master pointed to by the origin.
$ git rebase origin/master
or
$ git rebase -i origin/master
*Interactive Rebase Using the -i parameter will open a file that tells you what actions are going to be taken. When you close that file, those actions will be taken. You can edit the actions while the file is open. This can be handy if you want to clean up your history, or for troubleshooting. If you don’t want Git to take any action, delete the update instructions before closing the file.
If this works, you are ready to push to GitHub.
If there are conflicts, you can abort this rebase:
$ git rebase --abort
…or try to resolve the conflicts and continue.
If the rebase failed due to conflicts, Git will have placed conflict markers in the offending files. Use ‘git status’ to see what files have been changed.
$ git status
Edit each of these files, fix the conflicts, remove the markers, and save the files. When you get each file the way you want it, use ‘git add’ to save the modified file.
$ git add
Then continue the rebase:
$ git rebase --continue
To Merge Separate Work to a Single Repo
If each team member has worked separately and you need to combine your work to complete the project, follow these steps for seamless check-in.
One-at-a-time, each team member should do the following :
1) Clone the repo from GitHub (as described previously)
$ git clone paste-copied-url-here
2) Create and check out a new branch (branch can be your name)
$ git checkout -b your_branch_name
3) Copy the files you want to upload into the relevant folders (README into the main folder, notebooks into code, images into images, etc)
4) Add the files to git. To be safe, add each individually instead of ‘add -a’ to ensure you are only adding the files you want to be included in the final check-in.
$ git add your_file_name
4) Commit the set of files to git
$ git commit
5) Push your branch to Github (push your branch name — NOT master)
$ git push -u origin your_branch_name
6) Go to GitHub, find your branch, issue a Pull Request
7) Reviewers review and approve the request
8) Merge the code with the main branch
9) Repeat for the next person
Clean Commit History
It is possible to merge several commits into a single commit, preserving only the first commit message, use the interactive rebase to ‘fixup’, or ‘squash’ the commits. You may wish to do this if you have saved work-in-process along the way and don’t want to preserve and push to GitHub all the intermediate commit messages.
To ‘squash’ one or more commits into the prior commit, preserving only that prior commit message, use the interactive rebase to ‘fixup’ the commits.
find the prior commit in the log
$ git log
e.g., commit 372619f2b2f2940eb256db6a236c2555831c8911
grab the commit it and use it in an interactive rebase command
$ git rebase -i 372619f2b2f2940eb256db6a236c2555831c8911
Troubleshooting
To see previous commits:
$ git log
e.g., commit 372619f2b2f2940eb256db6a236c2555831c8911
To use a previous commit in an interactive rebase command:
$ git rebase -i 372619f2b2f2940eb256db6a236c2555831c8911
