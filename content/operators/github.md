---
title: "Github Operator"
weight: 12
---
# WIP - Not complete

The Github operator is used to download a Github release.  Please note this is a work in progress and currently not usable.

## Syntax

```yaml
- github:
  owner: <OWNER>
  repo: <REPO>
  tag: <TAG>
  asset: <ASSET>
  destination: <DESTINATION>
  token: <TOKEN>
  onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
  notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

`owner`: The owner of the Github repository.
`repo`: The name of the Github repository.
`tag`: The specific release tag to download.
`asset`: The filename of the asset to download from the release.
`destination`: The local file path where the asset will be saved.
`token`: (Optional) Your Github personal access token. This is required if you're downloading from a private repository or have exceeded the API rate limit.
`onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
`notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Example:

```yaml
github:
  owner: example
  repo: example-repo
  tag: v1.0.0
  asset: example-bin.tar.gz
  destination: /opt/example/bin/example-bin.tar.gz
  token: your_github_personal_access_token
```

In this example, the Github operator will download the example-bin.tar.gz asset from the release tagged v1.0.0 of the example/example-repo Github repository. The downloaded file will be saved to /opt/example/bin/example-bin.tar.gz.

## Example 2:

```yaml
github:
  owner: example
  repo: example-repo
  tag: v1.0.0
  asset: example-bin.tar.gz
  destination: /opt/example/bin/example-bin.tar.gz
  token: your_github_personal_access_token
  onlyIf: which tar
```

In the above example the Github operator will only execute the tar command if the /usr/bin/tar exists.

## Example 3:

```yaml
github:
  owner: example
  repo: example-repo
  tag: v1.0.0
  asset: example-bin.tar.gz
  destination: /opt/example/bin/example-bin.tar.gz
  token: your_github_personal_access_token
  notIf: ls example-repo/
```

In the above example the Github operator will only execute the tar command if the example-repo/ does not exist.


In the next section, we'll discuss the PackageRepo operator and how to use it in your manifest files.