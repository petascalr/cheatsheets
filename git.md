# Git cheatsheet

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
