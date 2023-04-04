---
title: "Recursive Copy Operator"
weight: 11
---
The Recursive Copy operator is used similarly to the copy operator but is intended to copy files recursively from a target location to location on the local machine.  The current supported source schemes (copyRecursive) include http and https as well as S3, please note that you must have your AWS environment already configured as the cfs application will make use of your environment keys / roles to make the copies should you decide to use S3.

## Syntax

```yaml
- copyRecursive: <SOURCE>
  dest: <DESTINATION>
  ignoreFiles: <IGNORED_FILES>
  flatCopy: <IGNORED_FILES>
  maxDepth: <IGNORED_FILES>
	maxConcurrent: <MAX_CONCURRENT>
```

* `copy`: The source directory/file to be copied.  Must currently be an http / https url.
* `dest`: The destination path where the file or directory should be copied to.
* `ignoreFiles`: This is a list of files that should not be copied from the source location.
* `flatCopy`: This is a boolean value that determines if the files should be copied to the destination directory or if the directory structure should be preserved.
* `maxDepth`: This is an integer value that determines the maximum depth of the directory structure that should be copied. If set to 0 or left unset it will copy the entire directory structure.
* `maxConcurrent`: This is an integer value that determines the maximum number of concurrent file copies that should be performed.  If set to 0 or left unset it will use the default value of 5.

Please do be careful with setting the maxConcurrency value too high as you may run into issues with the remote server throttling your requests.

## Example 1:
```yaml
- copyRecursive: https://the-eye.eu/public/AI/models/GPT-NeoX-20B/slim_weights/
  dest: /mnt/d/Projects/configset/test
  ignoreFiles: 
  - index.html
  flatCopy: true
  maxDepth: 5
  maxConcurrent: 10
```

In this example, the Copy operator will read the remote slim_weights directory and copy all of the files to the local directory `/mnt/d/Projects/configset/test`.  The files will be copied to the destination directory and not preserve the directory structure.  The index.html file will not be copied.  And it will only copy up to the fith level of the directory structure (maxDepth = 5).

## Example 2:
```yaml
steps:
- copyRecursive: s3://somebucket/
  dest: /tmp/test/
  ignoreFiles: 
  - index.html
  flatCopy: false
  maxDepth: 2
  maxConcurrent: 10
```

In this example, the Copy operator will read and S3 bucket (somebucket) and copy all of the files to the local directory `/tmp/test/`.  The files will be copied to the destination directory and preserve the directory structure.  The index.html file will not be copied.  And it will only copy up to the third level of the directory structure (maxDepth = 2).
