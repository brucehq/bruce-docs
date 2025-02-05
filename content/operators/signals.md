---
title: "Signals Operator"
weight: 14
---
The Signals operator is used to send signals to a process, typically to reload configuration files or gracefully stop the process.

## Syntax

```yaml
pidFile: <PID_FILE>
signal: <SIGNAL>
onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

* `pidFile`: The path to the process ID (PID) file for the process you want to send a signal to.
* `signal`: The signal to send to the process. Currently supports: SIGHUP, SIGINT.
* `onlyIf`: [See detailed docs here](sub-commands)
* `notIf`: [See detailed docs here](sub-commands)
* `exitIf`: [See detailed docs here](sub-commands)

## Example:

```yaml
pidFile: /var/run/nginx.pid
signal: SIGHUP
```

In this example, the Signals operator sends a SIGHUP signal to the process with the PID specified in the /var/run/nginx.pid file. This is often used to reload the Nginx configuration without stopping the process.

## Example 2:

```yaml
pidFile: /var/run/nginx.pid
signal: SIGINT
onlyIf: ls /tmp/output.txt
```

In this example, the Signals operator sends a SIGINT signal to the process with the PID specified in the /var/run/nginx.pid file. This is often used to gracefully stop the Nginx process, but it only executes if the /tmp/output.txt file exists.

## Example 3:

```yaml
pidFile: /var/run/nginx.pid
signal: SIGINT
notIf: ls /etc/systemd/system/nginx.service
```

In this example, the Signals operator sends a SIGINT signal to the process with the PID specified in the /var/run/nginx.pid file. This is often used to gracefully stop the Nginx process, but it only executes if the /etc/systemd/system/nginx.service file does not exist.

In the next section, we'll discuss the Templates operator and how to use it in your manifest files.