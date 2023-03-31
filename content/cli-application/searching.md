---
title: "Search Command"
weight: 3
---

3. Search.md - Search Command
The search command allows you to search the ConfigSet repository for a related manifest.

```bash
cfs search <SEARCH_TERM>
```

## Example
```bash
cfs search nginx
```

In the above example, cfs will search the ConfigSet (https://configset.com/#manifests) repository for any manifests that contain the word nginx in the title or description.