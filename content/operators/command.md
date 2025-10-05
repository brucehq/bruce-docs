---
title: "Command Operator"
weight: 2
---
The Command operator is used to execute a command on the system.

## Syntax

```yaml
- cmd: <command>
  dir: <workingdir>
  setEnv: <setenv>
  onlyIf: <sub-command>
  notIf: <sub-command>
  exitIf: <sub-command>
```
* `cmd`: The command to execute. Supports templating with environment variables via `RenderEnvString`, so `{{.VAR}}` Expansions are resolved before execution.
* `dir`: Working directory. Supports templating. If not specified, the process' current working directory is used.
* `setEnv`: This sub command takes the output of the command and sets it to the provided environment variable.
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

## Examples
### Example 1
```yaml
- cmd: mkdir -p /opt/example/directory && "hello world" > /opt/example/directory/output.txt
```
In this example, the Command operator will execute the mkdir command with the arguments -p and /opt/example/directory. This will create the specified directory along with any necessary parent directories.

### Example 2

```yaml
- cmd: echo "hello world"
  setEnv: HELLO_WORLD
```
In the this example the Command operator will execute the echo command with the argument "hello world". The output of the command will be set to the HELLO_WORLD environment variable, that can be used in other operators following.

### Example 3

```yaml
- cmd: ls -l
  onlyIf: /usr/bin/ls /tmp/somefile.txt
```
In the above example the Command operator will only execute the ls command if the /tmp/somefile.txt exists.

### Example 4

```yaml
- cmd: ls -l
  notIf: /usr/bin/ls /tmp/somefile.txt
```
In the above example the Command operator will only execute the ls command if the /tmp/somefile.txt does not exist.

### Example 5

```yaml
- cmd: echo "Will not run if this file exists"
  exitIf: test -f /etc/machine-id && echo exists
```
If the `exitIf` sub-command returns any output (and a zero exit status), Bruce exits early without running further steps.

In the next section, we'll discuss the Copy operator and how to use it in your manifest files.