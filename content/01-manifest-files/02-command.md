---
title: "Command Operator"
weight: 2
---
The Command operator is used to execute a command on the system.

## Syntax

```yaml
cmd: <COMMAND>
```

* `cmd`: The command to execute, the arguments to pass to the command, and any other options that should be used.

```yaml
cmd: mkdir -p /opt/example/directory && "hello world" > /opt/example/directory/output.txt
```

In this example, the Command operator will execute the mkdir command with the arguments -p and /opt/example/directory. This will create the specified directory along with any necessary parent directories.

In the next section, we'll discuss the Copy operator and how to use it in your manifest files.