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






    






