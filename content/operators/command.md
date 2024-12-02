---
title: "Command Operator"
weight: 2
---
The Command operator is used to execute a command on the system.

## Syntax

```yaml
cmd: <command>
dir: <workingdir>
osLimits: <oslimits>
setEnv: <setenv>
onlyIf: <sub-command> (Requires version 1.2.6 or higher)
notIf: <sub-command> (Requires version 1.2.6 or higher)
```

* `cmd`: The command to execute, the arguments to pass to the command, and any other options that should be used.
* `dir`: The working directory for the command. If not specified, the working directory will be the same as the directory where the manifest file is located.
* `osLimits`: The operating system limits to apply to the command. See the [Operating System Limits](/03-capabilities/02-os-limits/) page for more information.
* `setEnv`: This sub command takes the output of the command and sets it to the provided environment variable.
* `onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
* `notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Examples
### Example 1
```yaml
cmd: mkdir -p /opt/example/directory && "hello world" > /opt/example/directory/output.txt
```
In this example, the Command operator will execute the mkdir command with the arguments -p and /opt/example/directory. This will create the specified directory along with any necessary parent directories.

### Example 2

```yaml
cmd: echo "hello world"
setEnv: HELLO_WORLD
```
In the this example the Command operator will execute the echo command with the argument "hello world". The output of the command will be set to the HELLO_WORLD environment variable, that can be used in other operators following.

### Example 3

```yaml
cmd: ls -l
onlyIf: /usr/bin/ls /tmp/somefile.txt
```
In the above example the Command operator will only execute the ls command if the /tmp/somefile.txt exists.

### Example 4

```yaml
cmd: ls -l
notIf: /usr/bin/ls /tmp/somefile.txt
```
In the above example the Command operator will only execute the ls command if the /tmp/somefile.txt does not exist.

In the next section, we'll discuss the Copy operator and how to use it in your manifest files.