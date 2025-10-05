---
title: "Cron Operator"
weight: 4
---
The Cron operator is used to manage and set up cron jobs on the system.

Note: This operator is currently supported on Linux only and writes entries under `/etc/cron.d/<name>`.

## Syntax

```yaml
- cron: <NAME> 
  schedule: <SCHEDULE>
  username: <USER>
  cmd: <COMMAND>
  onlyIf: <sub-command>
  notIf: <sub-command>
  exitIf: <sub-command>
```

* `cron`: The name of the cron job; sanitized to alphanumeric for file naming.
* `schedule`: The standard crontab schedule expression.
* `username`: The user to run the cron job as (defaults to current user if omitted).
* `cmd`: The command to execute.
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

Templating: `cmd`, `username`, and conditionals support environment templating via `RenderEnvString()`.

## Example:

```yaml
- cron: foo
  schedule: "*/5 * * * *"
  username: dave
  cmd: echo "hello world" > /tmp/output.txt
```

In this example, the Cron operator will create a cron job named `foo` that runs every 5 minutes and executes `echo "hello world" > /tmp/output.txt` as user `dave`.

### Example 2

```yaml
- cron: foo
  schedule: "*/5 * * * *"
  username: dave
  cmd: echo "hello world" > /tmp/output.txt
  onlyIf: /usr/bin/ls /tmp/output.txt
```

In the above example the Cron operator will only execute the cron job if the /tmp/output.txt exists.

### Example 3

```yaml
- cron: foo
  schedule: "*/5 * * * *"
  username: dave
  cmd: echo "hello world" > /tmp/output.txt
  notIf: /usr/bin/ls /tmp/output.txt
```

In the above example the Cron operator will only execute the cron job if the /tmp/output.txt does not exist.

In the next section, we'll discuss the Git operator and how to use it in your manifest files.