### Summary: Split out folders from a git repo into separate repos

### Synopsis
```
gitsplit <topdir> <dest>

top-dir: the directory to split out
dest: the git working directory to place split out git repos
```

### Description

Each source directory directly under `<top-dir>`is copied
over to repo directory of the same name under `<dest>` and
a commit is made there.

The commit message includes the id and commit message of
the last commit made on the source directory.

Non-directories directly under the `<top-dir>` are ignored.

Symlinks are traversed and copied. There is (currently) no
option to just copy the symlink.

Split out destinaton repos must be non-bare so that files can be
removed and replaced there (i.e. in the working tree).

NOTE: This tool creates the destination repo if it does not exist.
Also, destination directory must not be / or a direct child of / (e.g. /myrepos).

