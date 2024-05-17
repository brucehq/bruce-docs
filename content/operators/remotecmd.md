---
title: "Remote Command Operator"
weight: 10
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
* `onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
* `notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

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