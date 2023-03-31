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
```

`owner`: The owner of the Github repository.
`repo`: The name of the Github repository.
`tag`: The specific release tag to download.
`asset`: The filename of the asset to download from the release.
`destination`: The local file path where the asset will be saved.
`token`: (Optional) Your Github personal access token. This is required if you're downloading from a private repository or have exceeded the API rate limit.

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

In the next section, we'll discuss the PackageRepo operator and how to use it in your manifest files.