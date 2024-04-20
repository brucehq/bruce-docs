---
title: "View Command"
weight: 4
---

The view command allows you to view a manifest in the CLI before executing the install command. This way, you can review the configuration and steps included in the manifest before applying it to your system.

```bash
bruce view <MANIFEST_URL>
```

## Example

```bash
bruce view https://someinstallhost/installme.yml
```

In the above example, bruce will download the manifest file from the provided URL and display the manifest in the CLI, so it can be reviewed before applying it to the system.  You should always do this prior to running the install command to ensure that the manifest is what you expect.