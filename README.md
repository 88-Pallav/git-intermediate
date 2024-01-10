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

    To decide what to include and what not to we need to go to the patch level:

    git add -p file_name
    (Here git will ask, We have to use 'y' for add and 'n' for leave)

b. Compose a 'good' commit message

    Subject: Cncise summary of what happened (< 80 Characters)
    Body = more detailed explanation
    - difference from before
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
    - different brach types 
    - fulfill different type of jobs
        
        (feature branch)
        c ---> c ---> c     c ---> c ---> c
      c/               \ c /               \c (develop branch)
    c/                                       \c (main branch)

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

***** Two Branching Strategies *********
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
 When git merge/git rebase/git pull/
      git cherry-pick/ git stash apply 

- mostly git figuers out automatically
- But sometimes changes are contradictory

To undo a conflict and start over:
git merge --abort
git rebase --abort

To resolve a conflict:
- clean up the file
- talk to fellow coder

********* Merge V/s Rebase ************
        
// Merge:         

        (last commit on branch A)    
(c'mon ancestor) c1-------------branch A 
                  \
                   \
                    c2 --- c3 ----- branch B
                (last commit on branch B)

Git looks for the above mentioned three commits in parenthesi
and end points of each branch

// Fast forward merge 

                        Branch_A
c1 -----> c2 -----> c3 
                        Branch_B

All commits are added witha c'mon ancestor commits 

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

Braanching branch b:
git rebase branch-B

This is what happens:
a. Git removes all commmits of branch A to ancestor commit (Parked Somewhere) 
b. It applies commits of Branch B making both Branches look the same temporarily 
c. Then rewriting commit history parked commits of branch A are commited on top of commits of branch B.
   
All this makes it look like a it all happened sequentialy

Warning: Do NOT use rebase on commits pushed/shared on a remote repository
Instead use it for cleaning up your local commits on a remote repository










