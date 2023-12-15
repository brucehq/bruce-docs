---
title: "PackageRepo Operator"
weight: 6
---
The PackageRepo operator is used to set up a package repository for supported package managers such as `apt`, `dnf`, or `yum`.

## Syntax

```yaml
repoName: <REPO_NAME>
repoLocation: <REPO_LOCATION>
repoType: <REPO_TYPE>
repoKey: <REPO_KEY>
osLimits: <OS_LIMITS>
```

* `repoName`: The name of the repository.
* `repoLocation`: The URL of the repository.
* `repoType`: The type of package manager used for the repository (apt, dnf, or yum).
* `repoKey`: The URL of the GPG key used to sign the repository packages.
* `osLimits`: A list of operating systems that the operator should run on.

## Example:

```yaml
- repoName: docker
  repoLocation: https://download.docker.com/linux/ubuntu
  repoType: apt
  repoKey: https://download.docker.com/linux/ubuntu/gpg
  osLimits: ubuntu|debian
```

In this example, the PackageRepo operator sets up the Docker repository for Ubuntu and Debian systems using the apt package manager. The GPG key used to sign the packages is also specified.

In the next section, we'll discuss the Packages operator and how to use it in your manifest files.