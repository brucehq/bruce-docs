---
title: "Copy Operator"
weight: 3
---
The Copy operator is used to create a copy of a file or directory on the system.

## Syntax

```yaml
- copy: <SOURCE>
  dest: <DESTINATION>
  perm: <PERMISSION>
```

* `copy`: The item to be copied at the source location.
* `dest`: The destination path where the file or directory should be copied.
* `perm`: The permissions to use in octal values for the copied file or directory.

## Example:
```yaml
- copy: s3://somebucket/somefile.bin
  dest: /usr/bin/somefile
  perm: 0775
```

In this example, the Copy operator will copy the file that lives under the s3 bucket (somebucket) to a local directory `/usr/bin/somefile` and the file permissions will be set to 0775.  The copy operator currently supports several retrieval methods such as s3, http, and local file which starts with ./ or /.  For more information on this see the supported retrieval methods.

In the next section, we'll discuss the Cron operator and how to use it in your manifest files.