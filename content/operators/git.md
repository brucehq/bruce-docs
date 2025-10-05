---
title: "Git Operator"
weight: 5
---
The Git operator provides a means to clone a Git repository to a specific location on the system, without the need to have git pre-installed on the system.  Please note that even though you may not have git installed this offers some basic functionality in order to clone a repository.  If you need more advanced functionality, you should install git on the system and use the `git` command directly.  The Git operator is also not intended to be used to manage a Git repository, but rather to clone a repository to a specific location on the system.

Templating: `gitRepo`, `dest`, `branch`, `tag`, and conditionals support environment templating via `RenderEnvString()`.

## Syntax

```yaml
- gitRepo: <repository url>
  dest: <destination>
  mode: <cloneOnly|pull|reclone>
  branch: <branch-name>
  tag: <tag-name>
  onlyIf: <sub-command>
  notIf: <sub-command>
  exitIf: <sub-command>
```

* `gitRepo`: The URL of the Git repository to clone.
* `dest`: The local path where the repository will be cloned to.
* `mode`: `cloneOnly`, `pull` (default), or `reclone`.
* `branch`: The branch to check out after cloning (optional).
* `tag`: The tag to check out after cloning (optional).
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

### Mode options:
Mode behavior:
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

