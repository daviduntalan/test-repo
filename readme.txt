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


In the command 'git push origin master', origin is the alias (nickname) for your remote repository, 
and master is the name of the specific branch you are pushing to that repository.

How to update local changes back to remote repository?
------------------------------------------------------
> git add readme.txt
> git commit -m "Updated readme.txt with git fetch and pull differences"
> git remote set-url origin https://github.com/daviduntalan/test-repo.git
> git push origin master

Fetch your SSH key necessary for Creating Github SSH and GPG Keys
-----------------------------------------------------------------
> type %userprofile%\.ssh\id_rsa.pub
> copy the result and go paste it to Github > Settings > SSH and GPG Keys


To check for changes made in a remote Git repository, the most standard and safest 
method is to fetch the remote updates and check your status. Running 'git fetch' 
downloads the latest history from the remote repository without changing or overwriting 
any of your local files. 

Here are the most common and effective ways to see if the remote repository has changes:

    Method 1: The Standard Status Check (Recommended)
    -------------------------------------------------
    This method tells you exactly how many commits your local branch is behind the remote tracking branch.

        1.  Download the latest data from your remote repository:
            > git fetch

        2.  Check your local branch status compared to the remote:
            > git status 

            - If there are changes, Git will tell you something like:
            “Your branch is behind 'origin/main' by 2 commits, and can be fast-forwarded.”        
            - If there are no changes, it will say:
            “Your branch is up to date with 'origin/main'.”

    Method 2: Preview the Commits
    -------------------------------------------------
    If you want to see the specific commit messages that exist on the remote server but 
    aren't on your machine yet, run this after running 'git fetch'

        > git log HEAD..origin/main
        (Replace 'main' with the name of the branch you are tracking, such as 'master' or 'develop').

    Method 3: Preview the Exact Code Changes
    -------------------------------------------------
    If you want to view the line-by-line code differences before deciding to pull, 
    compare your current state directly to the remote tracking branch:

        > git diff HEAD origin/main
        (Replace 'main' with the name of the branch you are tracking, such as 'master' or 'develop').