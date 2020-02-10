# Git-Trim: Tree-chop a git repo

## Synopsis
```
git_trim [REF [REFSPEC]]

REF specification (as an `--until` phrase.) Default is '30 days ago'. Remove this ref and all which came before it.
BRANCH the branch to trim (default is master). The branch to rewrite.
```
See [git filter-branch](https://git-scm.com/docs/git-filter-branch) for documentation on the ```--until``` flag.

## Introduction
Trim a git branch history. This effectively converts your git repo (branch) into a tool for keeping a limited history on your
content rather than a permanent history.

### ENVIRONMENT
`GIT_TRIM_ALLOWED` - must be set and not-empty to run this tool. This is to protect against accidental runs, since
git-trim is highly destructive.

### INSTALLATION:
copy git-trim and place in /usr/local/bin as executable file.

### INSTALLATION REQUIREMENTS:
LINUX or other UNIX flavor + git

### PROCESS:
Remove all commits prior to and including the selected (30 days ago) commit on the branch using commit rewrites.

### WARNING:
- This rewrites COMMIT HISTORY on your repo's branch. Do not use this unless you know what
  you are doing.

- This doesn't do something normal! Don't use it unless you really know Git well...
- This doesn't run garbage collection. Your repo probably won't shrink without some
  additonal garbage collection (e.g. See [git filter-branch](https://git-scm.com/docs/git-gc) and
  [git filter-branch](https://git-scm.com/docs/git-filter-branch) documentation.

- NOTE: If there are other branches, their history will remain untouched.
        For this reason it may be best to use this on a repo that only has a single branch
        - unless you *really* know what you are doing.

### BUGS:
email:mmpfeffer@gmail.com
