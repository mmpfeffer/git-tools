# rsync_codecommit

Recursively (and destructively) download (a portion of the) files from an AWS CodeCommit repository.

# Usage
```
rsync_codecommit [-h]      --repository-name REPOSITORY_NAME
                           --download-destination-path PATH
                           [--region REGION] [--profile AWS_PROFILE]
                           [--branch BRANCH | --commit-id COMMIT_ID]
                           [--source-folder-path PATH]
                           [--merge] [--force] [--verbose] [--debug]

```

## Defaults

- Default source-folder-path is the root directory folder in the repository (i.e. '/').
- Default commit to download is the current default branch.

## Flags

```
--merge:   Replace and add files from CodeCommit, but do not delete local files or directories under
           the download destination path.  The default is to ensure that the contents of the download
           directory reflect precisely the contents of the repository (subfolder) in CodeCommit.

--force:   Even if there has been no change, perform the download operation.

--verbose: Print a running log of activity.
--debug:   Print voluminous output of file transfers and other activities.

```

AWS Credentials and Region will be taken from environment variables such as AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY as per their normal usage, from ${HOME}/.aws/credentials file (for which the --profile option is provided), or in the case of execution from within an AWS service with an attached IAM Role (such as EC2, Lambda, EKS or ECS), through temporary credentials generated when the program is executed.

As a preventive measure, neither the root directory (e.g. '/') nor the current working directory (e.g. '.') may be specified in `--download-destination-path`.

Unless `--merge` is specified, all files and folders in the `--download-destination-path` will be erased prior to the download.

# Summary

The selected path is downloaded to the destination directory, which is created if it does not exist. Once downloading is complete,
a record of the activity is printed (and placed in file `.commit_info` in the destination directory) as follows:

Unless `--merge` is specified, this is the format:
```
{
    "commitId": "88ee5b99cec034638c7f0c7f888b3d5fcEXAMPLE",
    "repositoryName": "myRepoEXAMPLE",
    "sourceFolderPath": "myfolder/EXAMPLE",
    "md5Sum": "799b7215daf5f7168acb08b55EXAMPLE"
}
```

When `--merge` is specified, the record format is as follows:
```
{
    "commitId": "88ee5b99cec034638c7f0c7f888b3d5fcEXAMPLE",
    "repositoryName": "myRepoEXAMPLE",
    "sourceFolderPath": "myfolder/EXAMPLE",
    "flags": [
        "merged"
    ],
    "md5Sum": "799b7215daf5f7168acb08b55EXAMPLE"
}
```

The record file is used on subsequent invocations to check first if there is any change to the parameters and/or the locally stored files.
If the result of a download would not change the files in the destination download directory, the download is skipped silently.

# Requirements

This tool requires Python3 with the following non-standard python libraries:
- boto3

# Examples

Example 1: Download the contents of the `/joe` folder from the CodeCommit repository `customisation`
in the Ireland region (`eu-west-1`) into the local `/opt/myfiles` folder, _clearing_ all contents previously found in
that local folder:

`rsync_codecommit --repository-name customisation --source-folder-path joe --region eu-west-1 -l /opt/myfiles`

Example 2: Download and merge the contents of the `/joe` folder from the `staging` branch of the
CodeCommit repository `customisation` in the Ireland region (`eu-west-1`) into the local `/opt/myfiles` folder,
_preserving_ all contents previously found in that local folder:

`rsync_codecommit --repository-name customisation --source-folder-path joe --region eu-west-1 -b staging -l /opt/myfiles --merge`



# Bugs

When preparing to download, except in the --merge case, the directory is first erased and then the download takes place. This could lead to
files being wiped out if there is any issue with the download.
