---
title: "Loop Operator"
weight: 6
---
The loop operator is used to execute a target script multiple times. During each iteration, it sets/updates an environment variable with the current index.

The loop operator supports the following options:

* `loopScript`: The script to run multiple times (passed to the current bruce binary as the first argument).
* `count`: The number of times to run the script.
* `var`: The variable to set and update.
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

Templating: `loopScript` and conditionals support environment templating via `RenderEnvString()`.

```notes
Please do not set the incremental variable inside the target script, as this will override the value set by the loop operator.
```
In the example above the script will be executed 3 times and the variable NODE_ID will be set to 0, 1, and 2, consecutively for each execution of the script.
This makes it easy for installing clusters and managing them in a loop in a consistent way, and it ensures a more effective iterative approach to deploying and managing clusters, as the loop is not dependent on the script.
### Warning:

Setting the incremental variable inside the target script will override the value set by the loop script, for instance:

```yaml
---
variables:
  # note do not set Option here as it will be overwritten
  NODE_ID: 0
steps:
- cmd: echo "Hello World = {{.NODE_ID}}" >> output.txt
```

And  then using a loop script like this:

```yaml
- loopScript: setup-kafka.yml
  count: 3
  var: NODE_ID
```

The above script will not set the NODE_ID value appropriately as it will be overwritten by the local variable.