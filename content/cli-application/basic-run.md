---
title: "Install Command"
weight: 2
---
The install command is the default action and will be run if no commands are specified. It allows you to set up your environment based on the provided configuration file.

```bash
cfs <CONFIG_URL>
```
Alternatively, you can use the install command to which is the current default action.

```bash
cfs install <CONFIG_URL>
```

## Example
```bash
cfs https://someinstallhost/installme.yml
```

In the above example cfs will download the configuration file from the provided URL and install the configuration on the system.