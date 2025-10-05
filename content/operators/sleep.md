---
title: "Sleep Operator"
weight: 9
---
The sleep operator is a very simple operator in that it does exactly what is stated.  It will sleep for a set amount of seconds at which point it will continue the execution.  Please note that the standard notIf/ onlyIf can still be used to alter 
the behaviour.  For instance if you only want to sleep when a new server is being created in aws, but not if the server is already running then you can make use of the conditionals to set this up.

## Syntax

```yaml
- sleep: <seconds>
```
* `sleep`: The amount of time to sleep in seconds
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)
