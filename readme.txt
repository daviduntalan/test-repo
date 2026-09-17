hello, world! from david

What's the difference between Git Fetch and Git Pull?
-----------------------------------------------------
The primary difference is that 'git fetch' only downloads remote changes without
modifying your local working files, whereas 'git pull' downloads those changes and
immediately merges them into your current local branch.

In short, git pull is a shortcut that performs a 'git fetch' followed by a 'git merge' (or
'git rebase', depending on your configuration).


Direct Comparison

Feature         git fetch                           git pull 
----------------------------------------------------------------------------------------
What it does    Downloads new data from the         Downloads new data AND integrates it
                remote repository.                  into your current branch.
----------------------------------------------------------------------------------------
Modifies local  No. Your working directory is       Yes. It updates your local files.
files?          untouched.
----------------------------------------------------------------------------------------                
Risk of merge   None. Safe to run at any time.      High. Can trigger immediate merge
conflicts                                           conflicts.
----------------------------------------------------------------------------------------                
Use Case        Reviewing what others did before    Quick syncing when you know it is 
                changing your code.                 safe to merge. 
----------------------------------------------------------------------------------------                


How They Work Internally?
-------------------------

1. Git Fetch (The "Safe" Step)

When you run 'git fetch', Git reaches out to the remote repository (like GitHub or GitLab) and 
downloads any new commits, branches, or tags. However, it keeps these changes isolated in 
remote-tracking branches (e.g., origin/main). Your local branch (e.g., main) stays exactly where it was.

Because it doesn't touch your local files, you can use it to safely peek at what your team has done 
using commands like:

> git log HEAD..origin/main (To see new commit messages)
> git diff HEAD origin/main (To see the exact line changes)


2. Git Pull (The "All-in-One" Step)

When you run 'git pull', Git executes 'git fetch' behind the scenes. Once the changes 
are downloaded, it immediately tries to combine them with your local files.

Depending on your settings, it will handle the integration in one of two ways:

> git pull --ff (Default Merge): Combines histories and creates a "merge commit" if 
        your local path and the remote path have diverged (nagkahiwa-hiwalay).
> git pull --rebase: Temporarily removes your local commits, applies the remote updates, 
        and then replays your local changes right on top for a cleaner, linear history.