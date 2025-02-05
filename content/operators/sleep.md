---
title: "Sleep Operator"
weight: 12
---
The sleep operator is a very simple operator in that it does exactly what is stated.  It will sleep for a set amount of seconds at which point it will continue the execution.  Please note that the standard notIf/ onlyIf can still be used to alter 
the behaviour.  For instance if you only want to sleep when a new server is being created in aws, but not if the server is already running then you can make use of the conditionals to set this up.

## Syntax

```yaml
- sleep: <seconds>
  onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
  notIf: <sub-command> #(Requires version 1.2.6 or higher)
  exitIf: <sub-command> #(Requires version 1.5.0 or higher)
```
* `sleep`: The amount of time to sleep in seconds
* `onlyIf`: [See detailed docs here](sub-commands)
* `notIf`: [See detailed docs here](sub-commands)
* `exitIf`: [See detailed docs here](sub-commands)
