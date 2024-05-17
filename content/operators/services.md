---
title: "Services Operator"
weight: 12
---
The Services operator is used to manage services on the system, such as enabling, starting, stopping, and restarting them based on triggers.

## Syntax

```yaml
service: <SERVICE_NAME>
setEnabled: <SET_ENABLED>
state: <STATE>
restartTrigger:
  - <TRIGGER_FILE_1>
  - <TRIGGER_FILE_2>
  - ...
restartAlways: <RESTART_ALWAYS>
osLimits: <OS_LIMITS>
onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

* `service`: The name of the service to manage.
* `setEnabled`: A boolean value to enable or disable the service.
* `state`: The desired state of the service (started, stopped).
* `restartTrigger`: A list of file paths that, if changed, will trigger a service restart.
* `restartAlways`: A boolean value to always restart the service when the manifest is executed.
* `osLimits`: A list of operating systems that the operator should run on.
* `onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
* `notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Example:

```yaml
- service: nginx
  setEnabled: true
  state: started
  restartTrigger:
  - /etc/nginx/nginx.conf
  restartAlways: false
  osLimits: all
```

In this example, the Services operator enables and starts the Nginx service. It also sets up a trigger to restart the service if the /etc/nginx/nginx.conf file is changed. The service will not be restarted every time the manifest is executed.

## Example 2:

```yaml
- service: nginx
  setEnabled: true
  state: started
  restartTrigger:
  - /etc/nginx/nginx.conf
  restartAlways: true
  osLimits: all
  onlyIf: ls /tmp/output.txt
```

In the above example the Services operator will only execute the service if the /tmp/output.txt exists.

## Example 3:

```yaml
- service: nginx
  setEnabled: true
  state: started
  restartTrigger:
  - /etc/nginx/nginx.conf
  restartAlways: true
  osLimits: all
  notIf: ls /etc/systemd/system/nginx.service
```

In the above example the Services operator will only create the service if the /etc/systemd/system/nginx.service does not exist.


In the next section, we'll discuss the Signals operator and how to use it in your manifest files.