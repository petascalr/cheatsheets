# Git cheatsheet

### I collected these git commands from various sources like Stackoverflow, programming blogs, or simply the git documentation.


1. Initial git configuration.
   
        git config --list
        git config --global user.name "Liviu Gheorghisan"
        git config --global user.email "abc@def.com"

2. Squash last X commits into one.

        git rebase -i HEAD~X

3. Merge another branch into current branch.

        git merge -m "git merge message" feature/branch-X

4. Enable auto-stash (git stashes local changes before rebase, and then pops the stash).

        git config --global rebase.autoStash true

5. Change author of old commits.

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

6. Get the number of commits made by each author on all branches, in ascending order (not including merge commits).

        git shortlog -s -n --all --no-merges --since="1 Jan, 2019"

7. Get number of files changed/added/deleted per author.

        git log --shortstat --author="Anna Povzner" | grep -E "fil(e|es) changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "files changed: ", files, "lines inserted: ", inserted, "lines deleted: ", deleted }'

