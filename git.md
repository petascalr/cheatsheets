# Git cheatsheet

### I collected these git commands from various sources like Stackoverflow, programming blogs, or simply the git documentation.


1. Initial git configuration.
   
        git config --list
        git config --global user.name "Liviu Gheorghisan"
        git config --global user.email "abc@def.com"
        git config --global core.editor vim
        git config --global merge.tool p4merge
        git config --global diff.tool p4merge

1. Squash last X commits into one.

        git rebase -i HEAD~X

1. See what remote branch my local branch is tracking.

        git branch -vv

1. Pull changes from a remote branch into my local branch, and rebase my changes on top of the remote changes.

        git pull --rebase --autostash origin master

1. Merge another branch into current branch.

        git merge -m "git merge message" feature/branch-X

1. Enable auto-stash (git stashes local changes before rebase, and then pops the stash).

        git config --global rebase.autoStash true

1. Change author of old commits.

        git filter-branch --env-filter '
            WRONG_EMAIL="wrong@example.com"
            NEW_NAME="New Name Value"
            NEW_EMAIL="correct@example.com"

            if [ "$GIT_COMMITTER_EMAIL" = "$WRONG_EMAIL" ]
            then
                export GIT_COMMITTER_NAME="$NEW_NAME"
                export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
            fi
            if [ "$GIT_AUTHOR_EMAIL" = "$WRONG_EMAIL" ]
            then
                export GIT_AUTHOR_NAME="$NEW_NAME"
                export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
            fi' 
            --tag-name-filter cat -- --branches --tags

1. Get the number of commits made by each author on all branches, in ascending order (not including merge commits).

        git shortlog -s -n --all --no-merges --since="1 Jan, 2019"

1. Get number of files changed/added/deleted per author.

        git log --shortstat --author="Anna Povzner" | grep -E "fil(e|es) changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "files changed: ", files, "lines inserted: ", inserted, "lines deleted: ", deleted }'


1. Create git patches (with git metadata in them) out of the last 3 commits.

        git format-patch -3

1. Delete merged branches.
   
        git branch --merged | egrep -v "(*|master|dev)" | xargs git branch -d

1. Diff file between 2 branches

        git diff mybranch master -- MyClass.java
        git diff mybranch..master -- MyClass.java

        # diff between current branch and master
        git diff master 

