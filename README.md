********** Git for professionals ************

// The perfect commit

a. Add the 'right' changes

    a --> b --> c    a --> b --> c    
    |_____|_____|    |_____|     |
          |             |     commit_2           
        commit_1    commit_1
    
    Keep a & b in one commit and c in different commit 
    
    Do not cram all the files in one commit

    We can be selective about staging. 
    We can decide which files will go to which commit.
    
    Eg. We can do half files to b to commit_1 (a + 1/2b)
    and other half to commit_2 (1/2b + c) 

    Golden rule: Only combine files of the same topic to one commit.

    *To decide what changes to include and what not to, we need to go to the patch level:*
    git add -p file_name  *(Here git will ask, We have to use 'y' for add and 'n' for leave)*

b. Compose a 'good' commit message

    Subject: Concise summary of what happened (< 80 Characters)
    Body = more detailed explanation
    - Difference from before
    - Reason for changes 
    - Anything to watchout for


********** Branching Strategies ************

a. Have a written agreed upon convention
b. Integrating and structuring releases:
    b1. Mainline Development ("Always be Integerating")
    b2. State, release and Feature Branches 


// Mainline Development (Always be integrating)
    - few branches 
    - relatively small commits
    - high quality testing and QA standards 

    commit_1 ----> commit_2 ----> commit_3 ---> main_branch

// State, release and Feature Branches
    - different branch types 
    - fulfill different type of jobs
        
        (feature branch)
        c ---> c ---> c     c ---> c ---> c
      c/               \ c /               \c (develop branch)
    c/                                      \c (main branch)

// Long running Branches 
   - exist through the complete lifetime of the project
   - often, they mirror "stages" in your dev life cycle
   - c'mon convention: no direct commits 
     i.e. only through merge/rebase
   - eg. develop branch & main branch

// Short-lived branches 
    - for new features, bug fixes, refactoring, experiments
    - will be deleted after integration (merge/rebase)
    - eg. feature branch 

********* Two Branching Strategies *********
a. Github Flow
b. GitFlow

// GitHub Flow

    - very simple, very lean: only one long running
    - branches: main + feature
        
        (feature branch)
        c ---> c ---> c    c (bugfix branch)
       /               \  / \   
      c                 c    c (main branch) 

// Git Flow

    - more structure, more rules
    - long-running: "main" + "develop"
    - short-lived: feature, releases, hotfixes 

        (feature branch)
        c --> c --> c   (release branch)
       /            \   c --> c
      /              \ /       \
     c                c         \   (develop branch)
    /                            \  
   c                              c (main branch)


********* Pull Requests ************

- Communicating about and reviewing of code
- feedback before merger
- Contributing code to other repositories

Fork: Is a personal copy of git repository

Fork it --> Change it --> Raise a Pull request 

Note: Pull requests are always based on branches and not individual commits


********* Merge Conflicts ************
 
 How and when?

 When integrating commits from Different sources
 
 *When git_merge/git_rebase/git_pull/git_cherry_pick/git_stash apply:* 
- mostly git figures out automatically
- But sometimes changes are contradictory

*To undo a conflict and start over:*
git merge --abort
git rebase --abort

*To resolve a conflict:*
- clean up the file
- talk to fellow coder

********* Merge V/s Re-base ************
        
// Merge:         

        (last commit on branch A)    
(c'mon ancestor) c1-------------branch A 
                  \
                   \
                    c2 --- c3 ----- branch B
                (last commit on branch B)

Git looks for the above mentioned three commits in parenthesis
and end points of each branch

// Fast forward merge 

                        Branch_A
c1 -----> c2 -----> c3 
                        Branch_B

All commits are added with a c'mon ancestor commits 

// The merge commit 
              
              (merge commit)
c1 -----> c3 -----> c5 ---- branch A
  \                /
    c2 <-------- c4 ------- branch B

- gets created automatically by git not by a developer 
- purpose is to connect two branched like a knot

// Rebase 

c1 ---> c2 ---> c4 ---> c3  

c2, c4 - Branch-B
c3 - Branch-A

*Branching branch b:*
git rebase branch-B

This is what happens:

a. Git removes all commmits of branch A to ancestor commit (Parked Somewhere).
b. It applies commits of Branch B making both Branches look the same temporarily.
c. Then rewriting commit history parked commits of branch A are commited on top of commits of branch B.
   
All this makes it look like it all happened sequentialy

Warning: Do NOT use rebase on commits pushed/shared on a remote repository
Instead use it for cleaning up your local commits on a remote repository


****************** Branching in detail ********************************

*The HEAD branch:* The currently 'active' or 'checked out' branch
(There can only be one HEAD branch)

Local & Remote Branches: 95% times "working" with branches means local branches. That we are workig in a local git repository.

*#1 To create a new Branch:*
git branch <new_branch_name>   *(Git here assumes that we are going to start a new branch based on the currently checkout revision)*

*#2 To start a new_branch at a specific  revision:*
git branch <new_branch_name> revision_hash

*#3 To switch a branch:*
git checkout <branch_name> | git switch <branch_name> 

*#4 To rename a current 'local' branch:*
git branch -m <new_name>

*#5 To rename a different 'local' branch other than the current branch:*
git branch -m <old_branch_name> <new_branch_name> 

*#6 Renaming 'remote' branch:*
*Step 1: Delete current/old branch*
git push origin --delete <old_name>

*Step 2: Push the new local branch with the correct name:*
git push -u origin <new_name>

*#7 Pushing Branches: Uploading a local branch for the first time:*
git push -u origin <local_branch>   

Note: '-u' is upstream tells git to establish a tracking connection
to make pushing and puling later on easier

*#8 Tracking Branches:* 
Connecting branches with each other. Local and remote branches are independent to each other
but in real situations do share a relationship (like a counterpart).

c1 <--- c2 <------------------ c5---- Local branch 'develop' ---
         \
          c3 <--- c4 ---------------- remote branch 'origin/develop'

*Connecting branches with one another to track a remote branch to a local branch:*
git branch --track <new branch> origin/base<base-branch>
*or*
git checkout --track origin/<base_branch>

*#9 Deleting a branch in local repository:*
git branch -d <branch-name>     // You cant delete a current head (active) branch 

*To switch a branch use:*
git branch <branch_name>        // Then you can use #9 to delete the branch

*To delete a remote branch:*
git push origin --delete <branch_name> 

*Merging Branches: Integerating changes from another branch into your current local HEAD branch:*

*Step 1: Checkout the branch that should recieve the changes:*
git switch <branch_name>

*Step 2: Execute the merge command with the name of the branch that contains the desired changes:*
git merge <branch_name>

*#10 Rebasing: Alternative way to integrate changes from another branch into your current local head*
*Merge V/s Rebase*

*Merge Commit:*
                      Merge commit
                           |
c1<---------c3<-----------c5----Branch_A (Head)
\                        /
 \                      /
  c2 ------------------c4---------Branch_B

*Git Rebase:*                  
                                Branch-A (Head)
                                     |
c1----------c2----------c4----------c3
                        |
                     Branch-B

*Step 1: Checkout the branch that should recieve the changes:*
git switch <branch_name>

*Step 2: Execute the "rebase" command with the name of the branch that contains the desired changes:*
git rebase <branch_name>

*#11 Comparing Branches: Checking the commits that are in Branch-B but not in Branch-A:*
git log main..<Branch-Name>     // Eg. git log main..<feature/uploader>

*To see diff between local and main branch:*
git log origin/main..main






















 


















