USAGE
-----
```
filter-rsa-private-keys  [<git-filter-branch-options>] <rev-list-options>
```

INTRO
-----
```filter-rsa-private-keys``` filters out RSA (SSH) KEYS from a git repo.  It uses a very destructive tool
(```git filter-branch```) which generally should never be used, as it rewrites commit history.
```filter-rsa-private-keys``` runs through a given range of commits, filter-branching them looking for RSA private keys
and removing them, leaving behind only the header and footer text BEGIN RSA PRIVATE KEY/END RSA PRIVATE KEY.

The tool only scans the commits/branches you tell it too. See ```git filter-branch``` documentation about
```<rev-list-options>```

COMPLEXITY: High
DANGER LEVEL: High

PREPARATION
-----------
Set working directory to the top-level directory of the git repo you want to filter.

See ```man git-filter-branch``` for the possible options and use of <rev-list-options>.
This tool primarily depends on ```--tree-filter```.  If you don't know what that is, you
should NOT be reading this or using this script.

BUGS
----
- ```filter-rsa-private-keys``` relies on ```sed``` to modify the affected files in place. The ```sed``` command options
used works on Mac.  Other versions of UNIX may have a slightly different command line syntax. In particular,
the command line options for sed -i work a bit differently, so get that straight before you run this script.

- ```filter-rsa-private-keys``` assumes that the text ```-----BEGIN RSA PRIVATE KEY-----``` and ```-----END RSA PRIVATE KEY-----```
always come in pairs and always wrap an RSA key.  It will not find keys stored in any other way, and no
validation is done on that assumption: all lines between are simply deleted. It does not recognize
keys in PPK format. It does not recognize other kinds of private data or key formats.

- Keys found in file names with white-space in the names cause the operation to fail.

- Garbage collection on the git repo is not run. You have to take care of that yourself. See
```git filter-branch``` documentation and ```git gc``` documentation for more information.

- If you need to update a repo in a git server (such as GitHub), you will need to be able to forcibly
update the branch you are filtering, otherwise you won't be able to push the updated repo. Also, you may
need to check with the server administrator to verify that garbage collection will be run on your repo to
remove the unwanted history after you push your changes.
