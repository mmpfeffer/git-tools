# Git-Sync: Simple mirroring between two (or more) git remotes.

## Synopsis
```
git-sync DIR [-s SOURCE_REMOTE] [-d DEST_REMOTE]
DIR: directory holding git repo(s) to sync. Default is current directory.
-s SOURCE_REMOTE: remote to sync from. default to 'origin'
§-d DEST_REMOTE: remote to sync to. defaults to 'mirror'
```

## Introduction
Find local git mirrors and sync their origin to a mirror.

### ENVIRONMENT
SOURCE_REMOTE and DEST_REMOTE can be given via env. -s and -d take precedence.

### SETUP
Underneath the DIR clone and configure any number of folders and repos
e.g.
```
        cd ./somefolder/anotherfolder
        git clone --mirror <SOURCE_REPO_URL>
        git remote add 'mirror' <DEST_REPO_URL>
```

### REQUIREMENTS:
Credentials for 'origin' and 'mirror' remotes must be configured.

### LIMITATIONS:
Local git repos in subdirectories of PATH must be named with .git suffix (e.g. myrepo.git)

If the result of 'git clone' results in a directory named differently, change the directory
name to end with git.

Git submodules the submodules must be mirrored independently.

### INSTALLATION:
Copy git-sync and place in /usr/local/bin as executable file.

### INSTALLATION REQUIREMENTS:
LINUX or other UNIX flavor + git

### BUGS:
email:mmpfeffer@gmail.com
