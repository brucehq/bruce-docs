---
title: "Client Application Usage"
weight: 2
---
## Overall Usage
To get started with the cfs client application, download the appropriate binary for your platform from the official releases page. Once downloaded, extract the archive.

For Linux or macOS users, you can use the tar command to extract the archive:

```bash
tar -xzf cfs-<VERSION>-<PLATFORM>.tar.gz
```
Replace <VERSION> with the specific version number, and <PLATFORM> with your platform (e.g., linux-amd64 or darwin-amd64).

For Windows users, you can use a tool like 7-Zip to extract the archive.

Adding the cfs binary to your PATH
To use the cfs command from any directory, add the binary to your system's PATH:

Linux and macOS:

Move the cfs binary to /usr/local/bin:

```bash
mv cfs-<VERSION>-<PLATFORM>/cfs /usr/local/bin
```

Windows:

Create a new folder for the cfs binary, e.g., C:\cfs
Move the cfs.exe file to the new folder
Add the new folder to your system's PATH:
1. Right-click on the Computer icon on your desktop or in the Start menu, and select Properties.
2. Click on the Advanced system settings link on the left side.
3. Click the Environment Variables button at the bottom.
4. In the System Variables section, find the Path variable, select it, and click Edit.
5. Add ;C:\cfs to the end of the existing Path value (make sure to include the semicolon).
6. Click OK to save your changes, and close all remaining windows.

After adding the cfs binary to your PATH, you can use the client application from any directory.