---
title: "Sub-commands"
weight: 3
---

Bruce supports conditional execution and other specialized actions through the use of sub-commands within operator definitions. These sub-commands modify the behavior of the main operator.

## Conditional Execution

The following sub-commands allow you to control whether an operator runs based on the output of an external command:

*   **`onlyIf`**: Executes an external command. The operator will *only* run if the command's output is a non-empty string (considered "true"). An empty string output is considered "false," and the operator will be skipped.
*   **`notIf`**: Executes an external command. The operator will *not* run if the command's output is a non-empty string (considered "true"). An empty string output is considered "false," and the operator *will* run.
*   **`exitIf`**: Executes an external command. If the command's output is a non-empty string (considered "true"), the entire Bruce run will immediately terminate. An empty string output is considered "false," and the Bruce run will continue normally.

**Important Considerations for Conditionals:**

*   **External Commands:** The commands specified in `onlyIf`, `notIf`, and `exitIf` are external programs or scripts that Bruce executes. Ensure these commands are available in the environment where Bruce runs.
*   **Output Interpretation:** Bruce interprets any non-empty string output from these commands as "true" and an empty string as "false."  The *content* of the non-empty string is not relevant; only its presence.

## Robust Examples

The following examples demonstrate correct usage of conditional sub-commands with commands that produce output:

```yaml
- copy: s3://somebucket/somefile.bin
  dest: /usr/bin/somefile
  perm: 0775
  onlyIf: /usr/bin/ls /usr/bin/somefile
  
- cmd: /my/script.sh
  onlyIf: /my/check_script.sh # Run /my/script.sh only if /my/check_script.sh outputs something

- sleep:
  seconds: 60
  notIf: ping -c 3 [google.com](https://www.google.com/search?q=google.com) # Don't sleep if [google.com](https://www.google.com/search?q=google.com) is reachable (ping returns output)

- cmd: /another/script.sh
  exitIf: grep -q "ERROR" /path/to/logfile # exit if ERROR is found in the log file.
```