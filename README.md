# Complete DevOps Assignment: Git & GitHub Workflow

This repository documents a comprehensive series of Git and GitHub operations, demonstrating proficiency in version control, branch management, conflict resolution, and open-source contribution workflows.

## Question 1: Local Repository Initialization and Staging Operations

This section demonstrates the foundational Git workflow, including repository initialization, branch renaming to `main`, and the first commit. It explores staging and unstaging files using different commands. The `temp.txt` file is staged and subsequently unstaged using the `git restore --staged` command. Additionally, changes are modified and unstaged using the alternative `git reset HEAD` method to ensure working directory flexibility.

### Executed Commands:

```
git init
git branch -M main
echo "Initial content" >> initial.txt
git add initial.txt
git commit -m "Initial commit to the main branch"

echo "Temporary content" >> temp.txt
git add temp.txt
git restore --staged temp.txt

echo "Modifying the temp file" >> temp.txt
git add temp.txt
git reset HEAD temp.txt

```

### Screenshots:

## Question 2: Remote Repository Synchronization

This phase connects the local environment to a remote GitHub repository. A new remote repository named `Assignment-Task-Devops` is created on GitHub and linked to the local directory using `git remote add origin`. To demonstrate bidirectional synchronization, `initial.txt` is created locally, modified directly on the GitHub remote interface, and the remote changes are successfully synchronized back to the local repository using `git pull`. Additional files (`file1.txt` and `file2.txt`) are staged, selectively unstaged, and committed.

### Executed Commands:

```
git remote add origin https://github.com/Kulvir-ss24/Assignment-Task-Devops.git
# (Editing initial.txt on GitHub UI)
git pull origin main

echo "Demo content in File1" >> file1.txt
echo "Demo content in File2" >> file2.txt
git add file1.txt file2.txt
git reset HEAD file2.txt
git commit file1.txt -m "Commit file1 to remote"
git push origin main

```

### Screenshots:

## Question 3: Branching and Basic Pull Requests

Branching allows for isolated development. A new branch `g1` is created directly via the GitHub UI and fetched into the local environment. Local changes (`g1.txt`) are committed and pushed to the remote `g1` branch. A Pull Request is opened to merge `g1` into `main`. Upon successful review and merging on GitHub, the local `main` branch is updated via `git pull` to maintain parity with the remote repository.

### Executed Commands:

```
# (Created branch 'g1' via GitHub UI)
git fetch origin g1
git checkout g1
echo "Creating new file in g1 branch" >> g1.txt
git add g1.txt
git commit -m "Pushing g1.txt to branch g1"
git push origin g1

# (Pull Request opened and merged via GitHub UI)
git checkout main
git pull origin main

```

### Screenshots:

## Question 4: Advanced Tracking, Interactive Staging, and Resets

This section covers complex state management. Nested branches (`b1`, `b2`, `b3`) are sequentially created and updated. The `git add -p` command is utilized for interactive staging, allowing granular control over which code hunks are included in the commit. Commits are verified using `git diff --staged` and checked via formatted commit logs. Destructive and non-destructive rollbacks are performed using `git reset --hard` to completely erase commits, and `git reset --soft` to undo a commit while safely retaining the modifications in the staging area. The repository is then fully updated utilizing `git fetch` and `git merge`, and untracked files are effectively managed.

### Executed Commands:

```
git branch b1 && git checkout b1
git commit initial.txt -m "Updating initial.txt in b1"
git branch b2 && git checkout b2
echo "This is a demo-line for the new-file added in b2" >> b2_file.txt
git commit b2_file.txt -m "Updating b2_file.txt in b2"
git branch b3 && git checkout b3
echo "This is a second-line added in b3" >> b2_file.txt
echo "This is a second-line for demo purpose added in b3" >> file1.txt

git add b2_file.txt file1.txt
git reset --mixed HEAD
git add -p b2_file.txt file1.txt
git diff --staged
git commit -m "Selectively commit changes to b2_file and file1"
git log --oneline -n 5

git diff main g1
git ls-files
echo "Just testing untracked files" > untracked_file.txt
rm untracked_file.txt

# Reset Operations
echo "Last two lines will be deleted by hard reset.." >> initial.txt
git commit initial.txt -m "Performing a hard reset"
git reset --hard HEAD~1

echo "This is the information regarding Github! Updating changes.." >> initial.txt
git add initial.txt
git commit -m "Updation of initial.txt file"
git reset --soft HEAD~1

# Interactive staging
git add -p initial.txt
git commit -m "Commit partial <-p> changes using interactive staging ...."

git fetch origin
git merge origin/main

```

### Screenshots:







!\[Git Diff\](GIT--diff --staged--commit(B3)*4.png)
!\[Check Logs\](Checking* GIT_Status_Log_4.png)




## Question 5: Merge Conflicts and Branch Cleanup

Intentional conflicting modifications are made to `initial.txt` across branches `b2` and `b3`. A merge conflict is triggered when attempting to merge `b3` into `b2`, which is successfully resolved manually in the terminal. The resolved changes cascade upward as `b2` is merged into `b1`, and `b1` is finally merged into `main`. With development complete, repository hygiene is maintained by deleting the local branches `b1`, `b2`, and `b3`, alongside the removal of the remote `g1` branch.

### Executed Commands:

```
git checkout b3
# (Modify initial.txt)
git commit initial.txt -m "Modified file on branch b3"

git checkout b2
# (Modify initial.txt on the same line)
git commit initial.txt -m "Modified file on branch b2"

git merge b3
# (Conflict occurs, resolved manually in editor)
git add initial.txt
git commit -m "Resolve merge conflict between b3 and b2 manually"

git checkout b1
git merge b2
git checkout main
git merge b1

git branch -d b1
git branch -d b2
git branch -d b3
git push origin --delete g1

```

### Screenshots:

## Question 6: Forking Workflow and Cross-Repository Pull Requests

This task demonstrates an open-source contribution model. A new GitHub organization, `Kulvir-DevOps-Labs`, is created and configured under the free tier. The original `Assignment-Task-Devops` repository is then forked into this new organization. The forked repository is cloned locally, and new commits (`forked.txt`) are pushed directly to the fork's main branch. Synchronization checks ensure the fork is properly aligned with upstream changes. A cross-repository Pull Request is successfully opened, proposing changes from the forked repository to the original project. The PR is reviewed, confirmed, and successfully merged on GitHub. The merge is verified by checking the file structure and fetching the latest commit logs locally in both the forked and original repositories.

### Executed Commands:

```
# (Created Org, Verified Email, Forked Repo via GitHub UI)
git clone https://github.com/Kulvir-DevOps-Labs/Assignment-Task-Devops-Forked.git
cd Assignment-Task-Devops-Forked
echo "we had created this file under forked repository" >> forked.txt
git add forked.txt
git commit -m "Making some changes in forked repository"
git push origin main

# (Cross-repository PR opened and merged via GitHub UI)

# Verifying in Forked Repo:
git pull origin main
git log --oneline -n 6

# Verifying in Original Repo:
cd ../Assignment-Task-Devops
git pull origin main
git log --oneline -n 6

```

### Screenshots:

## Question 7: File Removal and Targeted Reversion

The final step demonstrates targeted commit reversion and file deletion using `git rm`. First, the `readme.md` file is created and added, while the `temp.txt` file is permanently removed from tracking via `git rm temp.txt`. These operations are combined into a single commit demonstrating the `rm` command. The commit history is then audited via `git log`, and the specific commit ID is used to safely execute `git revert <commit-id>`. This targeted reversion cleanly restores the working directory state—removing the new `readme.md` and bringing back the deleted `temp.txt`—without destructively rewriting the repository history.

### Executed Commands:

```
echo "Devops Assignment" >> readme.md
git rm temp.txt
git add readme.md
git commit -m "Demonstration of 'rm' command"

git log
# (Copied commit ID fac5f3d64c31d77ebc8e1de2391e6e0375f55cf2)

git revert fac5f3d64c31d77ebc8e1de2391e6e0375f55cf2
ls -alht

```

### Screenshots:


!\[Revert Commit\](Reverting_To previous_Commit_7.png)