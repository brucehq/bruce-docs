---
title: "Remote Command Operator"
weight: 8
---
The remote command operator allows you to run commands over an ssh encrypted tunnel as if it was on your local machine.  The intent is to allow for SSH remote execution of commands natively in both linux / mac and windows environments.

### - Note it only support ssh key authentication, interactive authentication is out of scope.
## Syntax

```yaml
- remoteCmd: <CMD>
  host: <HOST or user@host>
  setEnv: <ENV_VAR>
  key: </path/to/private/key>
  allowInsecure: true|false
  onlyIf: <sub-command>
  notIf: <sub-command>
  exitIf: <sub-command>
```

* `remoteCmd`: The command to be executed on the remote server.
* `host`: The host to connect to (supports `user@host` form).
* `setEnv`: Sets the stdout of the remote command into a local environment variable.
* `key`: SSH private key path. If not set, the CLI default is used (see `--private-key` in `bruce` flags).
* `allowInsecure`: Boolean flag to indicate whether to allow insecure connections, where the host is unknown.
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

Templating: `remoteCmd`, `host`, and conditionals support environment templating via `RenderEnvString()`.

Example connecting to the remote server with the current user name (useful in Linux if your SSH key is already set up)

## Example 1:
```yaml
- remoteCmd: sudo apt update -y
  host: www.somehost.com
  notIf: ls /var/lib/something.txt
```

In this example we will now use a different username for instance connecting to an ec2-user on an amazon box with the current ssh key:

## Example 2:
```yaml
- remoteCmd: sudo apt install -y nginx
  host: ec2-user@somehost.aws.com
```