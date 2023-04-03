---
title: "Recursive Copy Operator"
weight: 11
---
The Recursive Copy operator is used similarly to the copy operator but is intended to copy files recursively from a target location to location on the local machine.  The only current retrieval method supported is http / https.  Please note that this may change soon.

## Syntax

```yaml
- copyRecursive: <SOURCE>
  dest: <DESTINATION>
  ignoreFiles: <IGNORED_FILES>
  flatCopy: <IGNORED_FILES>
  maxDepth: <IGNORED_FILES>
```

* `copy`: The source directory/file to be copied.  Must currently be an http / https url.
* `dest`: The destination path where the file or directory should be copied to.
* `ignoreFiles`: This is a list of files that should not be copied from the source location.
* `flatCopy`: This is a boolean value that determines if the files should be copied to the destination directory or if the directory structure should be preserved.
* `maxDepth`: This is an integer value that determines the maximum depth of the directory structure that should be copied. If set to 0 or left unset it will copy the entire directory structure.

## Example:
```yaml
- copyRecursive: https://the-eye.eu/public/AI/models/GPT-NeoX-20B/slim_weights/
  dest: /mnt/d/Projects/configset/test
  ignoreFiles: 
  - index.html
  flatCopy: true
  maxDepth: 1
```

In this example, the Copy operator will read the remote slim_weights directory and copy all of the files to the local directory `/mnt/d/Projects/configset/test`.  The files will be copied to the destination directory and not preserve the directory structure.  The index.html file will not be copied.  And it will only copy the first level of the directory structure (maxDepth = 1).




