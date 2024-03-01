---
title: "Packages Operator"
weight: 7
---
The Packages operator is used to install packages on the system using the supported package manager based on the operating system type.

## Syntax

```yaml
packageList:
  - <PACKAGE_NAME_1>
  - <PACKAGE_NAME_2>
  - ...
osLimits: <OS_LIMITS>
onlyIf: <sub-command> #(Requires version 1.2.6 or higher)
notIf: <sub-command> #(Requires version 1.2.6 or higher)
```

* `packageList`: A list of package names to install on the system.
* `osLimits`: A list of operating systems that the operator should run on.
* `onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
* `notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Example:

```yaml
packageList:
  - bind9-utils
osLimits: ubuntu:20.04|debian
```

In this example, the Packages operator installs the bind9-utils package on Ubuntu 20.04 and Debian systems.


## Example 2:

```yaml
packageList:
  - bind9-utils
osLimits: ubuntu:20.04|debian
onlyIf: ls /etc/bind
```

In this example, the Packages operator installs the bind9-utils package on Ubuntu 20.04 and Debian systems if the `/etc/bind` directory exists.

## Example 3:

```yaml
packageList:
  - bind9-utils
osLimits: ubuntu:20.04|debian
notIf: which bind9
```

In this example, the Packages operator installs the bind9-utils package on Ubuntu 20.04 and Debian systems if the `bind9` command is not installed.

In the next section, we'll discuss the Services operator and how to use it in your manifest files.