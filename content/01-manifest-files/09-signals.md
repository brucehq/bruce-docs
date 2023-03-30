---
title: "Signals Operator"
weight: 9
---
The Signals operator is used to send signals to a process, typically to reload configuration files or gracefully stop the process.

## Syntax

```yaml
pidFile: <PID_FILE>
signal: <SIGNAL>
osLimits: <OS_LIMITS>
```

* `pidFile`: The path to the process ID (PID) file for the process you want to send a signal to.
* `signal`: The signal to send to the process. Currently supports: SIGHUP, SIGINT.
* `osLimits`: A list of operating systems that the operator should run on.

## Example:

```yaml
pidFile: /var/run/nginx.pid
signal: SIGHUP
osLimits: all
```

In this example, the Signals operator sends a SIGHUP signal to the process with the PID specified in the /var/run/nginx.pid file. This is often used to reload the Nginx configuration without stopping the process.

In the next section, we'll discuss the Templates operator and how to use it in your manifest files.