# Demo using BFG tools to remove credential from git history

## Prerequisite
Please read "Your current files are sacred..." before using `bfg` to remove your files.

https://rtyley.github.io/bfg-repo-cleaner/
### TLDR
Update your latest commit to desired state before using `bfg`. Removing any files you want bfg remove it for you first then use bfg to clean those files from other commits for you.

## Useful BFG commands
```bash
# Remove files
bfg --delete-files $FILE_NAME
# Remove folder
bfg --delete-folders $FOLDER_NAME
# Remove text
bfg --replace-text passwords.txt
# Remove files bigger than 50mb
bfg --strip-blobs-bigger-than 50M
```

## Installing BFG
### via package manager
```bash
# Macos
brew install bfg
# Windows
choco install bfg-repo-cleaner
```
### official bfg doc
https://github.com/rtyley/bfg-repo-cleaner/blob/master/BUILD.md

## Instructions to follow
1. Fork https://github.com/trairatp-sk/demo-remove-credential-using-bfg then clone to your local pc
2. Using your favorite git tools to examine the repo. You will see that there are 3 problems
   1. Private key at `secrets/id_rsa` (we will remove this file)
   2. Database password inside `.env` (we will remove password from that file)
   3. `node_modules` (we will remove this folder)
3. Fix those problem then create new commit
4. To completely remove private key run the following command
    ```
    bfg --delete-files id_rsa
    ```
5. To completely remove password from `.env`. Create a file called `leaked_passwords.txt` then add leaked password to it
    ```
    # Add "sup3r-s3cr3t-p@44w0rd" to leaked_password.txt
    bfg --place-text leaked_password.txt
    ```
6. To completely remove `node_modules`. Run the following command
    ```
    bfg --delete-folders node_modules
    ```
7. Examine the history. Verify that no secrets left in local repository (It will still exists in remote branch/repo)
8. Before running the command `git reflog` and `git gc`. Try checking out to commit using `git checkout 780470fcae4bd378b1a6b57c811fd0ad3a6e5da2`
9. You will see that secret can still be access in with commit id.
10. Checkout back to `main` branch then run `git reflog` and `git gc` as instructed by `bfg`
    ```
    git reflog expire --expire=now --all && git gc --prune=now --aggressive
    ```
11. Verify that the commit `780470fcae4bd378b1a6b57c811fd0ad3a6e5da2` cannot be checkout to anymore.