# Complete DevOps Assignment: Git & GitHub Workflow

This repository documents a comprehensive series of Git and GitHub operations, demonstrating proficiency in version control, branch management, conflict resolution, and open-source contribution workflows.

---

## Question 1: Local Repository Initialization and Staging Operations

This section demonstrates the foundational Git workflow, including repository initialization, branch renaming to `main`, and the first commit. 

It explores staging and unstaging files using different commands. The `temp.txt` file is staged and subsequently unstaged using the `git restore --staged` command. Additionally, changes are modified and unstaged using the alternative `git reset HEAD` method to ensure working directory flexibility.

### Executed Commands:
```bash
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
* ![Initial Commit](<Screenshots/Initialize-a-Local-Git-Repository/Initial_commit_1.png>)
* ![Restore Staged](<Screenshots/Initialize-a-Local-Git-Repository/Stage_unstage_(Git-restore)_1.png>)
* ![Reset Head](<Screenshots/Initialize-a-Local-Git-Repository/Modify_stage_unstage_(Git-reset)_1.png>)

---

## Question 2: Remote Repository Synchronization

This phase connects the local environment to a remote GitHub repository. A new remote repository named `Assignment-Task-Devops` is created on GitHub and linked to the local directory using `git remote add origin`. 

To demonstrate bidirectional synchronization, `initial.txt` is created locally, modified directly on the GitHub remote interface, and the remote changes are successfully synchronized back to the local repository using `git pull`. Additional files (`file1.txt` and `file2.txt`) are staged, selectively unstaged, and committed.

### Executed Commands:
```bash
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
* ![Create Repo](<Screenshots/Remote-Repository-Operations/Creating_new_repo_2.png>)
* ![Link Remote](<Screenshots/Remote-Repository-Operations/Linking_repo(remote-to-local)_2.png>)
* ![Before Expand](<Screenshots/Remote-Repository-Operations/Before_Expanding_(initial.txt)_2.png>)
* ![Expand GitHub](<Screenshots/Remote-Repository-Operations/Expand_(initial.txt)_remote_GitHub_2.png>)
* ![Pull Changes](<Screenshots/Remote-Repository-Operations/Pulling_changes(remote_repo)_2.png>)
* ![Stage Unstage](<Screenshots/Remote-Repository-Operations/git_stage_unstage_commit_2.png>)

---

## Question 3: Branching and Basic Pull Requests

Branching allows for isolated development. A new branch `g1` is created directly via the GitHub UI and fetched into the local environment. 

Local changes (`g1.txt`) are committed and pushed to the remote `g1` branch. A Pull Request is opened to merge `g1` into `main`. Upon successful review and merging on GitHub, the local `main` branch is updated via `git pull` to maintain parity with the remote repository.

### Executed Commands:
```bash
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
* ![Create Branch G1](<Screenshots/Branching-and-Pull-Request/Creating_new_branch(G1)_3.png>)
* ![Fetch G1](<Screenshots/Branching-and-Pull-Request/Fetch_G1_branch_(git-checkout)_3.png>)
* ![Push G1](<Screenshots/Branching-and-Pull-Request/Push_(g1.txt)_remote_branch_G1_3.png>)
* ![Compare PR](<Screenshots/Branching-and-Pull-Request/Comparing_pull_request_3.png>)
* ![Create PR](<Screenshots/Branching-and-Pull-Request/Creating_pull_request_3.png>)
* ![Merge PR](<Screenshots/Branching-and-Pull-Request/Merge_pull_request_3.png>)
* ![Merged Branch](<Screenshots/Branching-and-Pull-Request/Merged_branch_(g1-to-main)_3.png>)
* ![Sync Merged Changes](<Screenshots/Branching-and-Pull-Request/Sync_Merged_Changes_local_3.png>)

---

## Question 4: Advanced Tracking, Interactive Staging, and Resets

This section covers complex state management. Nested branches (`b1`, `b2`, `b3`) are sequentially created and updated. The `git add -p` command is utilized for interactive staging, allowing granular control over which code hunks are included in the commit. 

Commits are verified using `git diff --staged` and checked via formatted commit logs. Destructive and non-destructive rollbacks are performed using `git reset --hard` to completely erase commits, and `git reset --soft` to undo a commit while safely retaining the modifications in the staging area. The repository is then fully updated utilizing `git fetch` and `git merge`, and untracked files are effectively managed.

### Executed Commands:
```bash
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
* ![Branch B1](<Screenshots/Local-Git-Operations/Creating_branch(B1)_updating_4.png>)
* ![Branch B2](<Screenshots/Local-Git-Operations/Creating_branch(B2_in_B1)_updating_4.png>)
* ![Branch B3](<Screenshots/Local-Git-Operations/Creating_branch(B3_in_B2)_updating_4.png>)
* ![Unstage B3](<Screenshots/Local-Git-Operations/Unstaging_Changes_branch(B3)_4.png>)
* ![Interactive Staging 1](<Screenshots/Local-Git-Operations/Interactive_Staging(B3)_4.png>)
* ![Interactive Staging 2](<Screenshots/Local-Git-Operations/Interactive_Staging_4.png>)
* ![Git Diff](<Screenshots/Local-Git-Operations/GIT--diff --staged--commit(B3)_4.png>)
* ![Check Logs](<Screenshots/Local-Git-Operations/Checking_ GIT_Status_Log_4.png>)
* ![Track Untrack](<Screenshots/Local-Git-Operations/List_Changes_Track_Untrack_4.png>)
* ![Hard Reset](<Screenshots/Local-Git-Operations/Reset_Operation_HARD_4.png>)
* ![Soft Reset](<Screenshots/Local-Git-Operations/Reset_Operation_SOFT_4.png>)
* ![Update Files](<Screenshots/Local-Git-Operations/Getting_Updated_Files_4.png>)

---

## Question 5: Merge Conflicts and Branch Cleanup

Intentional conflicting modifications are made to `initial.txt` across branches `b2` and `b3`. A merge conflict is triggered when attempting to merge `b3` into `b2`, which is successfully resolved manually in the terminal. 

The resolved changes cascade upward as `b2` is merged into `b1`, and `b1` is finally merged into `main`. With development complete, repository hygiene is maintained by deleting the local branches `b1`, `b2`, and `b3`, alongside the removal of the remote `g1` branch.

### Executed Commands:
```bash
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
* ![Modify B2 B3](<Screenshots/Branch-Merging-and-Cleanup/Modify_Files_branch_B2_B3_5.png>)
* ![Resolve Conflict](<Screenshots/Branch-Merging-and-Cleanup/Resolve_Conflict_Merging_B3_with_B2_5.png>)
* ![Finish Merging](<Screenshots/Branch-Merging-and-Cleanup/Finish_Merging_Down_To_Main_5.png>)
* ![Delete Local](<Screenshots/Branch-Merging-and-Cleanup/Deleting_Local_Branches_(b1_b2_b3)_5.png>)
* ![Delete Remote](<Screenshots/Branch-Merging-and-Cleanup/Deleting_Remote_Branch_g1_5.png>)

---

## Question 6: Forking Workflow and Cross-Repository Pull Requests

This task demonstrates an open-source contribution model. A new GitHub organization, `Kulvir-DevOps-Labs`, is created and configured under the free tier. The original `Assignment-Task-Devops` repository is then forked into this new organization. 

The forked repository is cloned locally, and new commits (`forked.txt`) are pushed directly to the fork's main branch. Synchronization checks ensure the fork is properly aligned with upstream changes. A cross-repository Pull Request is successfully opened, proposing changes from the forked repository to the original project. The PR is reviewed, confirmed, and successfully merged on GitHub. The merge is verified by checking the file structure and fetching the latest commit logs locally in both the forked and original repositories.

### Executed Commands:
```bash
# (Created Org, Verified Email, Forked Repo via GitHub UI)
git clone https://github.com/Kulvir-DevOps-Labs/Assignment-Task-Devops-Forked.git
cd Assignment-Task-Devops-Forked

# (Make changes)
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
* ![New Org](<Screenshots/Fork-Operations/Click_To_New_Organization_6.jpg>)
* ![Free Plan](<Screenshots/Fork-Operations/Click_On_Free_Plan_6.png>)
* ![Setup Org](<Screenshots/Fork-Operations/Setup_Your_Organization_6.png>)
* ![Verify Email](<Screenshots/Fork-Operations/Verfify_Email_(Confirm-Access)_6.png>)
* ![Complete Setup](<Screenshots/Fork-Operations/Click_Complete_Setup_6.png>)
* ![Org Created](<Screenshots/Fork-Operations/Organization_Created_Successfuly_6.png>)
* ![Create Fork](<Screenshots/Fork-Operations/Click_Create_New_Fork_6.png>)
* ![Configure Fork](<Screenshots/Fork-Operations/Create_Fork_Copy_Of_Existing_Repo_6.png>)
* ![Repo Forked](<Screenshots/Fork-Operations/Repo_Forked_Successfully_6.png>)
* ![Clone Fork](<Screenshots/Fork-Operations/Cloning_Forked_Repo_Locally_6.png>)
* ![Make Fork Changes](<Screenshots/Fork-Operations/Making_Changes_Forked_Repo_6.png>)
* ![Sync Fork](<Screenshots/Fork-Operations/Click_On_Sync_Fork_6.png>)
* ![Contribute](<Screenshots/Fork-Operations/Click_Contribute_Open_PR_6.png>)
* ![Create PR](<Screenshots/Fork-Operations/Create_Pull_Request_6.png>)
* ![Verify PR](<Screenshots/Fork-Operations/Merging_PR_For_Verifying_Changes_6.png>)
* ![Confirm Merge](<Screenshots/Fork-Operations/Confirm_Merging_Operation_6.png>)
* ![Merged Success](<Screenshots/Fork-Operations/Merged_Successfully_6.png>)
* ![Original Repo Check](<Screenshots/Fork-Operations/After_Merge_Operation_(Check_In_Original_Repo)_6.png>)
* ![Forked Logs](<Screenshots/Fork-Operations/Pulling_Verifying_Status_Logs_Forked_Repo_6.png>)
* ![Original Logs](<Screenshots/Fork-Operations/Pulling_Verifying_Status_Logs_Original(main)_Repo_6.png>)

---

## Question 7: File Removal and Targeted Reversion

The final step demonstrates targeted commit reversion and file deletion using `git rm`. First, the `readme.md` file is created and added, while the `temp.txt` file is permanently removed from tracking via `git rm temp.txt`. These operations are combined into a single commit. 

The commit history is then audited via `git log`, and the specific commit ID is used to safely execute `git revert <commit-id>`. This targeted reversion cleanly restores the working directory state—removing the new `readme.md` and bringing back the deleted `temp.txt`—without destructively rewriting the repository history.

### Executed Commands:
```bash
echo "Devops Assignment" >> readme.md
git rm temp.txt
git add readme.md
git commit -m "Demonstration of 'rm' command"

git log
# (Copied the relevant commit ID for the action)

git revert fac5f3d64c31d77ebc8e1de2391e6e0375f55cf2
ls -alht
```

### Screenshots:
* ![Remove and Add](<Screenshots/Verifying-Status-Revert-Operations/Removing_and_adding_new_file_7.png>)
* ![Revert Commit](<Screenshots/Verifying-Status-Revert-Operations/Reverting_To previous_Commit_7.png>)