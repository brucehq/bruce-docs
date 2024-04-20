---
title: "Installing CFS Client Application"
weight: 1
---
## Installing CFS Client Application
To get started with the bruce client application, download the appropriate binary for your platform from the official releases page. Once downloaded, extract the archive.

For Linux or macOS users, you can use the tar command to extract the archive:

```bash
tar -xzf bruce-<VERSION>-<PLATFORM>.tar.gz
```
Replace <VERSION> with the specific version number, and <PLATFORM> with your platform (e.g., linux-amd64 or darwin-amd64).

For Windows users, you can use a tool like 7-Zip to extract the archive.

Adding the bruce binary to your PATH
To use the bruce command from any directory, add the binary to your system's PATH:

Linux and macOS:

Move the bruce binary to /usr/local/bin:

```bash
mv bruce-<VERSION>-<PLATFORM>/bruce /usr/local/bin
```

Windows:

Create a new folder for the bruce binary, e.g., C:\bruce
Move the bruce.exe file to the new folder
Add the new folder to your system's PATH:
1. Right-click on the Computer icon on your desktop or in the Start menu, and select Properties.
2. Click on the Advanced system settings link on the left side.
3. Click the Environment Variables button at the bottom.
4. In the System Variables section, find the Path variable, select it, and click Edit.
5. Add ;C:\bruce to the end of the existing Path value (make sure to include the semicolon).
6. Click OK to save your changes, and close all remaining windows.

After adding the bruce binary to your PATH, you can use the client application from any directory.