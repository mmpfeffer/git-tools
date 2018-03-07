# Git-Sync: Effective mirroring between git remotes.

## Synopsis
```
git-sync DIR [-s SOURCE_REMOTE] [-d DEST_REMOTE]

DIR: directory holding git repo(s) to sync. Default is current directory.
-s SOURCE_REMOTE: remote to sync from. default to 'origin'
-d DEST_REMOTE: remote to sync to. defaults to 'mirror'
```

## Introduction
Sync between git remotes.

### ENVIRONMENT
SOURCE_REMOTE and DEST_REMOTE can be given via env. -s and -d take precedence.

### SETUP
Choose a directory, clone and configure any number of folders and repos. For example:
```
mkdir /opt/mirrors/{project1,project2}
cd /opt/mirrors/project1
git clone --mirror <PROJECT1_REPO_URL>
git remote add 'mirror' <PROJECT1_MIRROR_URL>
cd /opt/mirror/project2
git clone --mirror <PROJECT2_REPO_URL>
git remote add 'mirror' <PROJECT2_MIRROR_URL>
cd /opt/mirrors
git-sync
```

### REQUIREMENTS:
Credentials and target repos for remotes must be pre-configured.

### LIMITATIONS:
Local git repos in subdirectories of DIR must be named with .git suffix (e.g. myrepo.git)
If the result of 'git clone' results in a directory named differently, change the directory
name to end with git.
Git submodules the submodules must be mirrored independently.

### INSTALLATION:
Copy git-sync and place in /usr/local/bin as executable file.

### INSTALLATION REQUIREMENTS:
LINUX or other UNIX flavor + git

### BUGS:
email:mmpfeffer@gmail.com
