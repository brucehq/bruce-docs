---
title: "Remote Command Operator"
weight: 11
---
The remote command operator allows you to run commands over an ssh encrypted tunnel as if it was on your local machine.  The intent is to allow for SSH remote execution of commands natively in both linux / mac and windows environments.

### - Note it only support ssh key authentication, interactive authentication is out of scope.
## Syntax

```yaml
- remoteCmd: <CMD>
  host: <HOST>
  onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
  notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

* `remoteCmd`: The command to be executed on the remote server.
* `host`: The host to connect to in order to execute the command.
* `setEnv`: This will set the output of the remote command to the local environment variable.
* `key`: The key to use for the remote connection (ssh key). uses the default key if not specified.
* `allowInsecure`: Boolean flag to indicate whether to allow insecure connections, where the host is unknown.
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

Example connecting to the remote server with the current user name (useful in linux if your ssh key is already set up)

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