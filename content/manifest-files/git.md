---
title: "Git Operator"
weight: 5
---
The Git operator provides a means to clone a Git repository to a specific location on the system, without the need to have git pre-installed on the system.  Please note that even though you may not have git installed this offers some basic functionality in order to clone a repository.  If you need more advanced functionality, you should install git on the system and use the `git` command directly.  The Git operator is also not intended to be used to manage a Git repository, but rather to clone a repository to a specific location on the system.

## Syntax

```yaml
- gitRepo: <repository url>
  dest: <destination>
  osLimits: <os limits>
```

`repository url`: The URL of the Git repository to clone.
`destination`: The local file path where the repository will be cloned to.
`osLimits`: (Optional) A list of operating systems that the Git repository is allowed to operate on.  If this is not specified, the repository will be cloned to all operating systems.

## Example:

```yaml
- gitRepo: https://github.com/mallorbc/Finetune_LLMs.git
  dest: ~/ai
  osLimits: ubuntu
```

In this example, the Git operator clones the repository for Fine Tuning LLM to the User's home directory into an aidirectory on Ubuntu systems.