---
title: "Signals Operator"
weight: 12
---
The Signals operator is used to send signals to a process, typically to reload configuration files or gracefully stop the process.

## Syntax

```yaml
pidFile: <PID_FILE>
signal: <SIGNAL>
osLimits: <OS_LIMITS>
onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

* `pidFile`: The path to the process ID (PID) file for the process you want to send a signal to.
* `signal`: The signal to send to the process. Currently supports: SIGHUP, SIGINT.
* `osLimits`: A list of operating systems that the operator should run on.
* `onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
* `notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Example:

```yaml
pidFile: /var/run/nginx.pid
signal: SIGHUP
osLimits: all
```

In this example, the Signals operator sends a SIGHUP signal to the process with the PID specified in the /var/run/nginx.pid file. This is often used to reload the Nginx configuration without stopping the process.

## Example 2:

```yaml
pidFile: /var/run/nginx.pid
signal: SIGINT
osLimits: all
onlyIf: ls /tmp/output.txt
```

In this example, the Signals operator sends a SIGINT signal to the process with the PID specified in the /var/run/nginx.pid file. This is often used to gracefully stop the Nginx process, but it only executes if the /tmp/output.txt file exists.

## Example 3:

```yaml
pidFile: /var/run/nginx.pid
signal: SIGINT
osLimits: all
notIf: ls /etc/systemd/system/nginx.service
```

In this example, the Signals operator sends a SIGINT signal to the process with the PID specified in the /var/run/nginx.pid file. This is often used to gracefully stop the Nginx process, but it only executes if the /etc/systemd/system/nginx.service file does not exist.

In the next section, we'll discuss the Templates operator and how to use it in your manifest files.