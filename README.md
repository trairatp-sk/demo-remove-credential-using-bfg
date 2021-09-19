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
brew install
# Windows
choco install
```
### official doc
https://github.com/rtyley/bfg-repo-cleaner/blob/master/BUILD.md
