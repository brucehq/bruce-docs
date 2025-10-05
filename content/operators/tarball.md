---
title: "Tarball Operator"
weight: 11
---
The Tarball operator is used to download and extract a tarball archive to a specified directory.

Templating: `tarball` (source), `dest`, and conditionals support environment templating via `RenderEnvString()`.

## Syntax

```yaml
- tarball: <TARBALL>
  dest: <DESTINATION>
  force: True|False
  stripRoot: True|False
```
* `tarball`: The location of the tarball archive to be downloaded.
* `dest`: The directory where the tarball should be extracted.
* `force`: A boolean value that determines if the destination directory should be overwritten if it already exists.
* `stripRoot`: A boolean value that determines if only the files inside the the first directory should be extracted.
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

## Example 1:

```yaml
- tarball: https://go.dev/dl/go1.19.4.linux-amd64.tar.gz
  dest: /tmp/go
  force: true # force will overwrite if destination exists or skip with info message if false
  stripRoot: true # will strip the first directory from every path, useful if the tarball contains an initial directory
 ```
In this example, the Tarball operator will download the tarball archive from the specified URL and extract it to the `/tmp/go` directory.  The `force` and `stripRoot` options are set to `true` and `true` respectively.  The `force` option will overwrite the destination directory if it already exists.  The `stripRoot` option will strip the first directory from every path, which is useful if the tarball contains an initial directory.  So what makes this useful is it allows you to download golang and extract it over a previous version of golang without having to worry about the directory structure.  Please do keep in mind though that you may actually not want to do this as new versions may require cleaning up some of the files that were previously installed.  However if you did already "create" an empty directory then this makes it easy to just extract into the existing directory.

## Example 2:
```yaml
- tarball: https://go.dev/dl/go1.19.4.linux-amd64.tar.gz
  dest: /tmp/go
  force: true # force will overwrite if destination exists or skip with info message if false
  stripRoot: true # will strip the first directory from every path, useful if the tarball contains an initial directory
  onlyIf: /usr/bin/ls /tmp/go
```

In this example the tarball operator will only execute the tarball command if the /tmp/go exists.

## Example 3:
```yaml
- tarball: https://go.dev/dl/go1.19.4.linux-amd64.tar.gz
  dest: /tmp/go
  force: true # force will overwrite if destination exists or skip with info message if false
  stripRoot: true # will strip the first directory from every path, useful if the tarball contains an initial directory
  notIf: /usr/bin/ls /tmp/go
```

In this example the tarball operator will only execute the tarball command if the /tmp/go does not exist.
