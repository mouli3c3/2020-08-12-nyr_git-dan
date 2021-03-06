# 2020-08-12 NYR Git Workshop

These are the commands and notes that were covered during the workshop.

## Local

- `git init`: create git repository (repo) in current folder
    - only do this once per repo
- `git status`: tells you your current git status
- `git add <FILE>`: puts <FILE> into the staging area
- `git commit`: open your default editor to type a commit message and commit changes
    - `git commit -m "MESSAGE"`: write a one line message and commit in 1 step
- `git log`: show you the history of the commits
    - `git log --oneline`: shows the 1 line version of the log
- `git diff`: shows you the difference between current state and last commit
    - git diff --staged`: shows you the diff in the staging area
- `git checkout <HASH> <FILE>`: reverts <FILE> back to the state in <HASH>
    - `git checkout HEAD~<NUM> <FILE>`: reverts <FILE> back to state in HEAD~<NUM>
    - `git checkout <HASH>`: moves HEAD to <HASH> (moves entire state/folder/snapshot)
        - `git checkout master`: goes back to master from detached HEAD state
- `HEAD`: tells you where you are currently looking
- `git restore <FILE>`: throws away changes from <FILE>
    - Can also use this to unstage from staging area
    - Older versions of git use `git reset`
- `.gitignore`: special file git uses to ignore files/folders
    - `git add -f <FILE>` force add a file that is ignored

## Remote

- `git remote add <NAME> <URL>`: adds the reference <NAME> to the <URL>
    - `git remote add origin <SSH URL>`
- `git push <WHERE> <WHAT>`: pushes <WHAT> to <WHERE>
    - `git push origin master`
    - do this once for rstudio: `git push -u origin master`

- `git log --oneline`: will now show references to the remote, e.g., `origin/master`)
    - `git log --oneline --graph --all`: shows your the entire history and makes it pretty

## Conflicts

- You can have multiple people (yourself included) work on the same file and at the same place
- Git will either automatically resolve the differences or show you a conflict.

- You won't know there will be a conflict, until you run `git pull` when the remote and your local computer is out of sync
    - It will either auto merge the changes
    - Or show you which files have a conflict.
        - You open the file and manually look for the `>>>`, `===`, and `<<<` and fix the file until you are satisfied.
        - You can then `git add` and `git commit` your changes and re `git push`

## Branches

- `git branch <NAME>`: creates a new branch, <NAME> where HEAD is
    - `git checkout -b <NAME>`: got create and move to branch in 1 step
    - `git switch -c <NAME>`: newer git version to do the same task
- `git checkout <BRANCH>`: move to branch <BRANCH>
    - `git switch <BRANCH>`: newer way

## Pull Requests (Online Merge)

- `git log --oneline --graph --all`: show everything in history
- `git fetch --prune`: removes the references from deleted branches in the remote
- PRs don't need to be re-created after each branch update/push, the PR will auto update itself

## Branch conflicts

- happens when branches do work in the same place and the conflict happens when you try to merge all the branches
- `git rebase <BRANCH>`: rebases agaist a branch to rewind and play back commits
    - Usually this is `git rebase master`
    - See 3.8.4: https://chendaniely.github.io/training_ds_r/help-faq.html

## Some additional notes and links

- Software Carpentry notes on basic git: https://swcarpentry.github.io/git-novice/
    - The setting up git has the commands to setup your name/email/editor: https://swcarpentry.github.io/git-novice/02-setup/index.html

- Git workflow notes and commands (to paste on your wall)
    - https://chendaniely.github.io/training_ds_r/help-faq.html

- Atlassian page on git workflows: https://www.atlassian.com/git/tutorials/comparing-workflows
    - The one we covered today was mainly the "Feature Branch Workflow": https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow

- The atlassian page has more infor about "git flow", but this is also another top Google hit that I liked:
  - https://nvie.com/posts/a-successful-git-branching-model/

- Getting your (bash) terminal to show current path and other things:
    - Use this to create your PS1 variable: http://bashrcgenerator.com/

- Show git branch in terminal:
    - In addition you can write a function and put that in your PS1 to also show git branch
    - https://gist.github.com/joseluisq/1e96c54fa4e1e5647940

- https://chendaniely.github.io/training_ds_r/help-faq.html (has the checklist)
- https://happygitwithr.com/ (more rstudio specific workflows)
- https://swcarpentry.github.io/git-novice/
- https://www.youtube.com/watch?v=uvWhSYBkZJ0
- Setting up ssh links: https://bi-sdal.github.io/training/ssh-keys.html

## Final exercise

1. (M) will add (C) as a collaborator
2. (C) accept the invitation (email)
3. (C) `clone` the repo to their computer
    - make sure it's not nested
4. (M)/(C) make a new branch, edit the script.R file, add, commit, push to remote
  - `git checkout -b my_colab_update`
  - edit file
  - `git add .`
  - `git commit -m ""`
  - `git push origin my_colab_update`

5. (M) (C): create a PR to the repo
6. (M) accept each one separately
    - (M) accept theirs first

Probably a conflict with (C)

7. (C): fix conflicts
  - `git checkout master`,
  - `git pull origin master`,
  - `git checkout your_branch`,
  - `git rebase master`
  - fix conflicts
  - re-push branch to update PR

8. (M) should be able to merge
