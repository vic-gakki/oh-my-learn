# Pro Git
> this is a summary after reading [pro-git e-book](https://git-scm.com/book/en/v2)

### Getting Started
#### Version Control History
- local version control
- centralised version control
  > a server stores history changes and ecah client checkout current snapshot not all history
- distributed version control
  > ecah client mirror the repo. Thus if the server break down, it can resotre by copying from a client 

#### What is Git
- snapshots, not differences
> the way of thinking of data: other systems think of data as a set of files and the **changes** made to each file over time. this is commonly describled as delta-based version control. While git thinks of data like a series of **snapshots** of a miniature filesystem. [^1]

[^1]: git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficent, if files have not changed, git doesn't store the file again, just a link to the previous identical file it has already stored.

- nearly every operation are local
- git has integrity 
  > everything in git is checksummed before it is stored and is then referred to by that checksum. this means it's impossible to change the contents of any file or directory without git knowing about it.
- git generally only adds data

#### Git Setup
- git config
  - --system: applies to every user on the system and all their repositories.
  - --global: applies to all your repositories.
  - --local: appliyes to the repository you are currently working and is default but you need to be located somewhere in a git repository for this work properly.
- git confit --list --show-origin: to show all config and where they are coming from.

### Git Basics
#### Recording Changes
- git diff: to see changes between working directory and the index
  - --staged: changes between the index and last commit
- git rm: to remote file from index and also working directory. 
  - -f: By default, the file being removed must be identical to the tip of the branch, and no updates to the contents can be staged in the index.
  - --cached: the staged content has to match either the tip of the branch or the file on disk, allowing the file being removed from just the index.
- git mv: to rename files
  > equivalent to mv file.old file.new + git rm file.old + git add file.new

#### View Commit History
- git log
  - -p | --patch: to show the difference introduced in each commit
  - --stat: to see some abbreviated stats for each commit
  - --pretty: accepts a value to change the format of output and has presets like oneline, short, full, fuller. Especially, the option value **format** allows you to custom your own style
    | name | desc |
    | ----- | ----- |
    | %H | commit hash |
    | %h | abbreviated commit hash |
    | %T | tree hash |
    | %t | abbreviated tree hash |
    | %P | parent hash |
    | %p | abbreviated parent hash |    
    | %[a or c]n | anthor or commiter name |
    | %[a or c]e | anthor or commiter email |
    | %[a or c]d | anthor or commiter date |
    | %[a or c]r | anthor or commiter date, relative |
    | %s | subject, commit message |
  - --graph: to show a nice ASCII graph
  - -S: filter commits that changed the number of occurences of the value string
  - -\<n>: show only last n commits
  - --since, --after
  - --until, --before
  - --author
  - --committer
  - --grep: show only commits with a commit message containing the string

#### Undo Things
- git commit --amend: when you forget to add some files or change the commit message
  > improved commit will replace the previous commit, but do remember only amend commit that are still local and have not been pushed somewhere.

##### Unstage a staged file
- git reset HEAD \<file>
- git restore --staged \<file>
  
##### Unmodify a modified file
- git checkout -- \<file>
- git restore \<file>

#### Work With Remote
- git remote: list shortnames of each remote
  - -v: shows urls for the shortname to be used when reading and writing to that remote
- git remote add \<name> \<url>: add remote repository
- git fetch \<remote>: fetch all data from that remote that you don't have yet. After doing this, you have references to all the branches from that remote
- git pull: if the current branch is set up to track a remote branch, then this command will automatically fetch and merge that remote branch to your current branch
- git push \<remote> \<branch>
- git remote show \<remote>: to see more information about that remote
- git remote rename oldName newName
- git remote remove \<remote>

#### Tagging
> git supports two kinds of tags: **lightweight** and **annotated**
> lightweight: is very much like a branch that doesn't change - it's just a pointer to a specific commit
> annotated: store full objects in the git database. they are checksummed, containing tagger name, email, date and messeage
- git tag
  - -l "search wildcard pattern": to list filterd tags
- git tag tagName [commit]: to create a tag
  - -a [-m ""]: to create an annotated tag
- git show tagName: to show tag information
- git push origin tagname: By default, git push doesn't transfer tags to the server. to explicitly push tag using this command
  > if you have lots of tags to push up at once, use **git push --tags**
- git tag -d tagName: to delete a local tag
- git push origin --delete tagName: to delete a remote tag
- git checkout tagName: to view the version of files that tag is pointing to and will make git in **detached HEAD** [^2] state.
  [^2]: In detached HEAD state, if you create a commit, the tag will stay the same, but your new commit won't belong to any branch and will be unreachable, except by the exact commit hash

#### Alias
- git config --global alias.xx "subcomand"


### Git Branching
> A branch in git is a lightweight movable pointer to one of the commit.
> Create a new branch is simply add a movable pointer to the current commit. Thus, how does git know which branch you are currently on? **It keeps a spcial pointer called `HEAD` pointing to the current branch. you can use `git log --decorate` to show branch pointer
- git branch branchName: to create a new branch
- git checkout branchName: to switch to an existing branch
> to create a branch and switch to it at the same time, using `git checkout -b branchName`. [^3]

[^3]: From Git version 2.23 onwards you can use `git switch` instead of `git checkout` to do following things: 1. switch to an exsiting branch: `git switch branchName`. 2. create a branch and switch to it: `git switch -c branchName`. 3. return to your previously checked out branch: `git switch -`

#### Merge Branch
- git merge branchName
  - fast forward mode
  - three-way merge: using two snapshots and the common ancestor of the two, and create a new snapshot resulted from the three-way merge and automatically creates a new commit message. this commit has **more than one parent**. if conflicts occur, you can do the following:
    - git status to see conflict files
    - mannually fix the conflict
    - git add to stage file
    - git commit, message box will open with default conflict-handling message, you can modify it with more detail

#### Branch Management
- git branch
  - `-v`: to see last commit on each branch
  - `--merged`: to see branch that have been merged into current branch, `--no-merged` vice virsa

#### Remote Branch
##### Remote-Tracking Branch
>It's a reference to the state of remote branch. It's local reference but can't move. Git move it for you whenever you do any network communication.
##### Tracking Branch
> checkout a local branch from a remote tracking branch automatically creates what is called a 'tracking branch' (and the branch it tracks is called upstream branch). **Tracking branch is a local branch which has a direct relationship to a remote branch**. If you type `git pull` on the tracking branch, Git automatically knows which server to fetch from and which branch to merge in.
- git checkout -b localBranch remote/branch: checkout a tracking branch which tracks the remote branch 
- git checkout --track remote/branch: shorthand for the above
- git checkout branch: shorthand for the above when 1. branch doesn't exist. 2. exactly matches a name on only one remote.
- git branch -u(--set-upstream-to) remtoe/branch: to explicitly set upstream branch
- git branch -vv: to see what tracking branches you have set up.

#### Rebasing
> This operation works by going to the common ancestor of the two branches, getting the diff introduced by each commit of the branch you're on, saving those diffs to temporary files, resetting the current branch to the same commit you are rebasing onto, and finally applying each change in turn.

- git rebase baseBranch topicBranch

### Git on the Server   
> a bare repository: a git repo that has no working directory. It's the contents of your project's `.git` directory and nothing else.
- four protocols
  - local
  - http
  - secure shell(SSH)
  - git

#### Create bare repository
- git clone --bare \<your repo> \<bare repo>: to export an existing repo inot a new bare repo. By convention, bare repo directory names end with the suffix `.git`

#### Putting the bare repo on a server