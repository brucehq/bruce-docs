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
```

* `packageList`: A list of package names to install on the system.
* `osLimits`: A list of operating systems that the operator should run on.

## Example:

```yaml
packageList:
  - bind9-utils
osLimits: ubuntu:20.04|debian
```

In this example, the Packages operator installs the bind9-utils package on Ubuntu 20.04 and Debian systems.

In the next section, we'll discuss the Services operator and how to use it in your manifest files.