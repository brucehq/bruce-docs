---
title: "Copy Operator"
weight: 3
---
The Copy operator is used to create a copy of a file or directory on the system.

All string fields (`copy`, `dest`, and conditionals) support environment templating via `RenderEnvString()`, so values like `s3://bucket/{{.APP_ENV}}/artifact.tgz` are rendered using current environment variables.

## Syntax

```yaml
- copy: <SOURCE>
  dest: <DESTINATION>
```

* `copy`: The item to be copied at the source location.
* `dest`: The destination path where the file or directory should be copied.
* `key`: Optional key/credential used by the loader for remote sources (e.g., S3 or authenticated endpoints).
* `perm`: The permissions to use in octal values for the copied file or directory.
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

Supported sources include:

- `s3://bucket/key`
- `http(s)://...`
- Local paths (`/path`, `./relative`)

## Example 1:
```yaml
- copy: s3://somebucket/somefile.bin
  dest: /usr/bin/somefile
  perm: 0775
```

In this example, the Copy operator will copy the file that lives under the s3 bucket (somebucket) to a local directory `/usr/bin/somefile` and the file permissions will be set to 0775.  The copy operator currently supports several retrieval methods such as s3, http, and local file which starts with ./ or /.  For more information on this see the supported retrieval methods.

## Example 2:

```yaml
- copy: s3://somebucket/somefile.bin
  dest: /usr/bin/somefile
  perm: 0775
  onlyIf: /usr/bin/ls /usr/bin/somefile
```

In the above example the Copy operator will only execute the copy command if the /usr/bin/somefile exists.

## Example 3:

```yaml
- copy: s3://somebucket/somefile.bin
  dest: /usr/bin/somefile
  perm: 0775
  notIf: /usr/bin/ls /usr/bin/somefile
```

In the above example the Copy operator will only execute the copy command if the /usr/bin/somefile does not exist.

In the next section, we'll discuss the Cron operator and how to use it in your manifest files.