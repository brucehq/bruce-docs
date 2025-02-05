---
title: "Git Operator"
weight: 5
---
The Git operator provides a means to clone a Git repository to a specific location on the system, without the need to have git pre-installed on the system.  Please note that even though you may not have git installed this offers some basic functionality in order to clone a repository.  If you need more advanced functionality, you should install git on the system and use the `git` command directly.  The Git operator is also not intended to be used to manage a Git repository, but rather to clone a repository to a specific location on the system.

## Syntax

```yaml
- gitRepo: <repository url>
  dest: <destination>
  onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
  notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

* `repository url`: The URL of the Git repository to clone.
* `destination`: The local file path where the repository will be cloned to.
* `mode`: Can be one of the following: `cloneOnly, pull, reclone
* `branch`: The branch to checkout after cloning the repository
* `tag`: The tag to checkout after cloning the repository
* `onlyIf`: [See detailed docs here](sub-commands)
* `notIf`: [See detailed docs here](sub-commands)
* `exitIf`: [See detailed docs here](sub-commands)

### Mode options:
For the mode options please note that the following behavior will be added to the git clone operation once set:
- `cloneOnly`: This will only clone the repository and will not perform any additional operations.
- `pull`: This will clone the repository and then pull the latest changes from the repository.
- `reclone`: This will remove the existing repository and clone it again.

NOTE: Default mode is `pull` if not specified.

## Example 1:

```yaml
- gitRepo: https://github.com/mallorbc/Finetune_LLMs.git
  dest: ~/ai
```

In this example, the Git operator clones the repository for Fine Tuning LLM to the User's home directory into an aidirectory on Ubuntu systems.

## Example 2:

```yaml
- gitRepo: https://github.com/mallorbc/Finetune_LLMs.git
  dest: ~/ai
  onlyIf: which python
```

In this example, the Git operator clones the repository for Fine Tuning LLM to the User's home directory into an aidirectory on Ubuntu systems if the `python` command is installed.

## Example 3:

```yaml
- gitRepo: https://github.com/mallorbc/Finetune_LLMs.git
  dest: ~/ai
  notIf: which python3.11
```

In this example, the Git operator clones the repository for Fine Tuning LLM to the User's home directory into an aidirectory on Ubuntu systems if the `python3.11` command is not installed.

