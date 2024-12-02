---
title: "Cron Operator"
weight: 4
---
The Cron operator is used to manage and set up cron jobs on the system.

## Syntax

```yaml
- cron: <NAME> 
  schedule: <SCHEDULE>
  username: <USER>
  cmd: <COMMAND>
  onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
  notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

`name`: The name of the cron job.
`schedule`: The schedule of the cron job.
`username`: The user to run the cron job as.
`cmd`: The command to execute, the arguments to pass to the command, and any other options that should be used.
`onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
`notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Example:

```yaml
---
- cron: foo
  schedule: "*/5 * * * *"
  username: dave
  cmd: echo "hello world" > /tmp/output.txt
```

In this example, the Cron operator will create a cron job named foo that will run every 5 minutes and execute the command `echo "hello world" > /tmp/output.txt` as the user foo.

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

In the next section, we'll discuss the Github operator and how to use it in your manifest files.