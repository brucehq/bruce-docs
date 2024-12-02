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

`repository url`: The URL of the Git repository to clone.
`destination`: The local file path where the repository will be cloned to.
`onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
`notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

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

