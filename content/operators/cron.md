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
```

`name`: The name of the cron job.
`schedule`: The schedule of the cron job.
`username`: The user to run the cron job as.
`cmd`: The command to execute, the arguments to pass to the command, and any other options that should be used.

## Example:

```yaml
- cron: foo # give it a name
    schedule: "*/5 * * * *"
    username: foo
    cmd: cho "hello world" > /tmp/output.txt
```

In this example, the Cron operator will create a cron job named foo that will run every 5 minutes and execute the command `echo "hello world" > /tmp/output.txt` as the user foo.

In the next section, we'll discuss the Github operator and how to use it in your manifest files.