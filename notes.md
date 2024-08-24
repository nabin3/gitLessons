### There are two types of git commands:
* High level commands, named as **porcelain** commands. Most of the time this type of commands are used. Some examples are:-
	git status
	git add
	git commit
	git push
	git pull
	git log
		
* Low level commands, named as **plumbing** commands. Some examples are :- 
	git apply
	git commit-tree
	git hash-object

## Concepts
* ```git config --get user.name```, For retrieveing user name
* ```git config --get user.email``` For retrieveing user email
* ```git config --add --global user.name 'github_username"```. To set git username globally
* ```git config --add --global user.email "github_user_email_id"```. To set git user_email globally
* if omitted ```--global``` flag from abve commands of adding, key-value will be set in local firconfig file(.git/config).

* ```~/.gitconfig``` this file stores global git configaration.
```bash
* git's default branch name set with```git config --global init.defaultBranch master```
* A repo is a directory with a **.git** file in it. Git stores all it internal tracking and versioning information for the repo.
* to create a repo make directory with ```mkdir directory_name```. Then do ``` cd newly_created_directory && git init```
* A file can have sevaral stages in a git repo.Somes are:
	1. ```untracked```: Not being tracked by git.
	2. ```staged```: Marked for inclusion in the next commit
	3. ```committed```: Saved to the repository history
* The ```git status command``` shows you the current state of your repo. It will tell you which files are untracked, staged, and committed.
* to stage a file ```git add filename```
* to see status of files in a repo ```git status```
* After staging a file, we can commit it. A commit is a snapshot of the repository at a given point in time. It's a way to save the state of the repository, and it's how Git keeps track of changes to the project. A commit comes with a message that describes the changes made in the commit.
```bash
git commit -m "your message here"
```
* If you screw up a commit message, you can change it with the --amend flag. ```# Change the last commit message
git commit --amend -m "A: add contents.md"```
* ```git log``` command shows a history of the commits in a repository
* ```git --no-pager log -n 10``` -> this command shows last 10 commits without an interactive pager.
* Commit hashes depends on the commit message, author's name and email, date and time, parent commit hashes. So commit hases are always unique.
* git uses cryptographic hash function **SHA-1** to generate commit hashes. So commit hashes also reffred as **SHAs**

* git is made up of objects that are stored in the ```.git/objects```  

* ```tree```: git's way of storing a directory.
* ```blob```: git's way of storing a file.
```bash
git cat-file -p c6bcde86a279d18ecff887e78bb0564a6347379a
# -p fo pretty print and the c6bcde... is a commit. 
tree 5b21d4f16a4b07a6cde5a3242187f6a5a68b060f
author nabin3 <nabinchandramaiti6@gmail.com> 1723898518 +0530
committer nabin3 <nabinchandramaiti6@gmail.com> 1723898518 +0530

A: add contents.md

# to view the content of contents.md we need the blob file for contents.mf file
git cat-file -p 5b21d4f16a4b07a6cde5a3242187f6a5a68b060f
100644 blob ef7e93fc61a91deecaa551c4707e4c3049af42c9	contents.md

# Now that we have got hash file of bob by cat-file tree hash, we will again cat-file bob hash to reveal content of contents.md file

git cat-file -p ef7e93fc61a91deecaa551c4707e4c3049af42c9
# contents

```

* ```git log``` is a porcelain command, but ```git cat-file``` is a plumbing command

* git stores an entire snapshot of files on a per-commit level. 

* git **compresses & packs** files to store them more efficiently. git deduplicates files that are same across different commits.If a file doesn't change across different commits, git will only store it once. 

* You can actually store any old data in your Git configuration. Granted, only certain keys are used by Git, but you can store whatever you want.

* ```git config --list --local or git config --list --global``` for viewing contents of config.

* We can store any key-value in git configuration, but only certain keys certain keys are used by git.

* where ```--list``` is used for listing all key-value of config file, ```--get``` is used for retrieveing value of a mentioned key from config file. ```git config --get <section>.<keyname>```

* The ```--unset``` flag is used to remove a configuration value. 
```git config --unset <section>.<keyname>```

* git config allows of existence duplicate keys, when they exist you can unset all of them with ```--unset-all```
```bash
git config --unset-all <section>.<keyname> 

git config --add webflyx.ceo "Warren"
git config --add webflyx.ceo "Carson"
git config --add webflyx.ceo "Sarah"

git config --unset-all webflyx.ceo
```

* to remove an entire **section** from config file use ```git config --remove-section <section-name>```

### config-location:
There are several locations where Git can be configured. From more general to more specific, they are:

system: /etc/gitconfig, a file that configures Git for all users on the system
global: ~/.gitconfig, a file that configures Git for all projects of a user
local: .git/config, a file that configures Git for a specific project
worktree: .git/config.worktree, a file that configures Git for part of a project
In my experience, 90% of the time you will be using --global to set things like your username and email. The other 9% of the time you will be using --local to set project-specific configurations. The last 1% of the time you might need to futz with system and worktree configurations, but it's extremely rare.

If you set a configuration in a more specific location, it will override the same configuration in a more general location. For example, if you set user.name in the local configuration, it will override the user.name set in the global configuration.

### git branch:
a git branch allows us to keep track of different changes seperately.

under the hood a brach is just a named pointer to a specific commit. When you create a branch, you are creating a new pointer to a specific commit. The commit that the branch points to is called the tip of the branch.

we can check on which branch we are corrently in by ```git branch```

we can rename a brach with ```git branch -m oldname newname```

we can create new brach with ```git branch branch-name```, but we will use ```git branch switch -c branch-name```, where -c is for creating a branch if the named branchdon't exist.

* when we create a branch, it uses the commit we are on as the base of the branch.

* can use --decorate flag to controll git log msg display , with value **full** git log will show the ref name.A ref is just a pointer to a commit. All branches are refs, but not all refs are branches. value **no** will ommit the branch name and value **short** which will display only the branch name but not ref name.

* another flag is ```--online```, this show us more compact view of log. Combining both ```--decorate``` and ```--online``` we can get interesting log.
```bash
git log --decorate=full --oneline 
a4f0a34 (HEAD -> refs/heads/add_classics) D: added classics movies
755ba92 (refs/heads/main) C: added quotes
a7aa776 B: add titles
c6bcde8 A: add contents.md
```

### merge:
"What's the point of having multiple branches?" you might ask. They're most often used to safely make changes without affecting your (or your team's) primary branch. However, once you're happy with your changes, you'll want to merge them back into the main branch so that they make their way into the final product.

```git log --oneline --graph --all``` --all is for for displaying all branches and --graph is for ASCII art. 
example:
```bash
 git log --oneline --all --graph 

* 8583585 (HEAD -> main) E: write something in contents.md
| * a4f0a34 (add_classics) D: added classics movies
|/  
* 755ba92 C: added quotes
* a7aa776 B: add titles
* c6bcde8 A: add contents.md
```

* a merge commit is the result of marging two branches together. We can merege into the branch in where we are present by ```git merge branch-to-be-merged```. 
```bash
example:
git merge vimchadsonly

The merge will:

Find the "merge base" commit, or "best common ancestor" of the two branches. In this case, "A".
Replays the changes from vimchadsonly onto main starting from the best common ancestor.
Records the result as a new commit, in our case "F".
"F" is special because it has two parents, "C" and "E".
After:

A - B - C - F    main
   \     /
    D - E        vimchadsonly


this is from this repo:
git log --oneline --graph --parents

*   015e159 8583585 a4f0a34 (HEAD -> main) F: merge branch 'add_classics'
|\  
| * a4f0a34 755ba92 (add_classics) D: added classics movies
* | 8583585 755ba92 E: write something in contents.md
|/  
* 755ba92 a7aa776 C: added quotes
* a7aa776 c6bcde8 B: add titles
* c6bcde8 A: add contents.md
```

in case want to change most recent commit msg use this ```git commit --amend -m "F: new msg"```

This is a common workflow when working with Git on a team of developers:

Create a branch for a new change
Make the change
Merge the branch back into main (or whatever branch your team dubs the "default" branch)
Remove the branch
Repeat

* we can delete branch with ```git branch -d branch_name```
#### fast-forward merge:
when to be merge branch has all the commit those are also present in the branch in where we are merging, then fast-forward merge happens and in this case no merge commit created. 
```bash
      C     delete_vscode
     /
A - B       main

git merge delete_vscode

            delete_vscode
A - B - C   main
```

### Rebase:
A - B - C    main
   \
    D - E    feature_branch

now if we want to bring the change of to main branch to the feature_branch we can do merge but there will be a merege commit created, to avoid that and to get a linear commit history we will do rebase feature_brach. 
	Rebase avoids a merge commit by replaying the commits from feature_branch on top of main. After a rebase, the history will look like this:
A - B - C         main
         \
          D - E   feature_branch

to create a new branch from a specified commit we will do ```git switch -c update_dune COMMITHASHi```

to use **rebase** to bring the change of main branch to the current_branch(in this case feature branch) we will run ```git rebase main``` while on feature_branch.
This will do the following:

Checkout the latest commit on main
Replay one commit at a time from feature_branch onto main
Update the feature branch to point to the last replayed commit
The rebase doesn't affect main while feature_branch has all of the changes from main

#### when to rebase?
git rebase and git merge are different tools.

An advantage of merge is that it preserves the true history of the project. It shows when branches were merged and where. One disadvantage is that it can create a lot of merge commits, which can make the history harder to read and understand.

A linear history is generally easier to read, understand, and work with. Some teams enforce the usage of one or the other on their main branch, but generally speaking, you'll be able to do whatever you want with your own branches.

You should never rebase a public branch (like main) onto anything else. Other developers have it checked out, and if you change its history, you'll cause a lot of problems for them.

However, with your own branch, you can rebase onto other branches (including a public branch like main) as much as you want.

### Reset:
The git reset command can be used to undo the last commit(s) or any changes in the index(staged but not commited changes) and the worktree(unstaged and not commited changes)
#### soft reset:
```git reset --soft COMMITHASH```
The --soft option is useful if you just want to go back to a previous commit, but keep all of your changes. Committed changes will be uncommitted and staged, while uncommitted changes will remain staged or unstaged as before.

#### hard reset:
This is useful if you just want to go back to a previous commit and discard all the changes.
```bash
git reset --hard COMMITHASH
```
 It's a powerful tool, but it's also a dangerous one. Because, unlike --soft it will delete all after the COMMITHASH you reseted.


## Remote:
```git remote add <remote_name> <url>```
### fetch:
```git fetch```, This downloads copies of all the contents of the .git/objects directory (and other book-keeping information) from the remote repository into your current one.
Just because we fetched all of the metadata from the remote repo doesn't mean we have all of the files.

* git log can also dispaly commits from remote repo's specific branch ```git log remote_name/branch_name```

### merging remote branch:
Just as we merged branches within a single local repo, we can also merge branches between local and remote repos.```git merge remote_name/branch_name"

### push:
```git push remote_name branch_name```
we can also push our local branch as different branch name to the remote with ```git push remote_name <localbranch>:<remotebranch>```
we can delete a remote branch by pushing a empty branchto it.
```git push remote_name :<remotebranch>```

### pull:
```git pull [<remote>/<branch>]```. The syntax [...] means that the bracketed remote and branch are optional. If you execute git pull without anything specified it will pull your current branch from the remote repo.

tips: If you get a "divergent branches" error, run git config pull.rebase false to make sure git will merge on a pull.

#### pull request:
On GitHub, a pull request is a way to propose some changes. It's very common to use pull requests if you want to make changes to an open source project, or if you're working on a team.

Pull requests allow team members to see what changes are being proposed and to discuss them before they are merged into the main codebase.

## gitignore
if you put ```node_modules``` for example in **.gitignore** then This will ignore every path containing node_modules as a "section" (directory name or file name). It ignores:

node_modules/code.js
src/node_modules/code.js
src/node_modules
It does not ignore:

src/node_modules_2/code.js
env/node_modules_3

### nested gitignore:
Your .gitignore file does not necessarily need to be at the root of your project.

It's fairly common to have multiple .gitignore files in different directories throughout a project. A nested .gitignore file only applies to the directory it's in and its subdirectories.

### patterns in .gitignore
It would be rough if .gitignore files only accepted exact filepath section names. Luckily, they don't!

#### wildcards *:
The * character matches any number of characters except for a slash (/). For example, to ignore all .txt files, you could use the following pattern:
```bash
*.txt
```
#### Rooted patterns
Patterns starting with a / are anchored to the directory containing the .gitignore file. For example, this would ignore a main.py in the root directory, but not in any subdirectories:
```bash
/main.py
```

#### Negation:
You can negate a pattern by prefixing it with an exclamation mark (!). For example, to ignore all .txt files except for important.txt, you could use the following pattern:
```bash
*.txt
!important.txt
```

#### comments:
You can add comments to your .gitignore file by starting a line with a #. For example:
```bash
# Ignore all .txt files
*.txt
```
