---
title: "The operators"
weight: 3
---

Manifest files are the core building blocks of bruce. They are used to describe the desired state of your infrastructure and define the actions, components, and configurations required for a specific task. Manifest files are written in a simple, easy-to-understand language that is both human-readable and machine-parseable.  Each manifest file will contain one or many operators and their associated variables to drive the operators to accomplish your task.

## Structure of a Manifest File

A manifest file is divided into two main sections: `variables` and `steps`. The `variables` section is used to define any variables that will be used within the manifest file. The `steps` section is used to define the actions that will be taken to achieve the desired state of the infrastructure.  Variables defined here can also be overwritten by using a properties file or by overwriting them with the setEnv flag in a command step.  This allows for maximum flexibility where you can download a pre-configured manifest file and then overwrite the variables to suit your needs.  Please note that if you make use of templates that are referenced in the manifest file, your templates will make use of the same variables that are set.

NOTE: Variables that are set using the `setEnv` sub-command are only available within the execution, and do not persist after the execution is complete. This allows you to set a temporary "secure" variable that cannot 
be re-used after execution is complete.  Good for items like initialing a system with a specific secret then having the environment scrubbed after without bleeding into the regular operating system.

Below is an example of a manifest file that can be used to set up a basic Nginx web server.

```yaml
---
variables:
  ServiceOwner: www-data
  RotateDays: 7
  VHOST_ROOT: /opt/vhosts/hello-world
steps:
- packageList:
  - nginx
  - logrotate

# get my ip address to set as the vhost domain
- cmd: ip addr show $(ip route | awk '/default/ {print $5}') | awk '/inet / {print $2}' | awk -F/ '{print $1}'
  setEnv: Domain

# Create a virtual host via a template
- template: /etc/nginx/sites-available/hello-world
  source: https://raw.githubusercontent.com/brucehq/bruce/refs/heads/main/examples/nginx/templates/etc/nginx/vhosts/default.conf

# Create a symlink for the virtual host
- cmd: ln -sf /etc/nginx/sites-available/hello-world /etc/nginx/sites-enabled/hello-world

# Clone the static HTML repo
- gitRepo: https://github.com/brucedom/static-content-example.git
  dest: VHOST_ROOT

- template: /etc/logrotate.d/nginx
  source: https://raw.githubusercontent.com/brucehq/bruce/refs/heads/main/examples/nginx/templates/etc/nginx/vhosts/default.conf

# Enable and start the Nginx service
- cmd: systemctl daemon-reload && systemctl restart nginx
```


In the above referenced structure you can see that we first define a set of variables. `ServiceOwner` and `RotateDays` are used by the manifest to set up logrotate. `VHOST_ROOT` defines the location of static content served by Nginx. `Domain` is set by a command that retrieves the server IP address, then used in a template step to set the virtual host domain. For reference, see the template that uses this variable: [example template](https://brucedom.com/api/templates/7cc81042-b638-5260-bd09-2e6066fbfc46/data).

## Available Operators
|Operator|	Description|
|-|-|
|[API](/operators/api/)|	Make HTTP(s) requests and set the response as an environment variable, or dump it to a file to be used later. Has built in capabilities to parse json for dot notation of keys.|
|[Command](/operators/command/)|	Execute native commands with arguments. Optional capabilities for running onlyIF or notIf conditions. Output can also be set as envars for use later in the configuration.|
|[Copy](/operators/copy/)|	Copy provides a means to copy files from one location to another, sources could include http(s) or s3 or local files on the same box.|
|[Cron](/operators/cron/)|	Enables the ability to add or remove cron jobs from the system, specifically for *nix environments.|
|[Git](/operators/git/)|	Clone or pull a git repository to a specified location, does not require git to be installed on the system.|
|[Loop](/operators/loops/)|	Allows for looping over a list of commands, useful for iterating over a list of items. Example use case would be installing kafka and providing a different ID for each instance.|
|[RecursiveCopy](/operators/recursive-copy/)|	Copy files from one location to another, recursively. Sources could include http(s) or s3 or local files on the same box, this uses concurrency to allow for multiple files to be processed at the same time.|
|[RemoteExecution](/operators/remotecmd/)|	Execute commands on remote hosts via ssh, this allows you to execute a remote command and also set the output as an environment variable.|
|[Sleep](/operators/sleep/)| Sleep allows you to pause the execution of the manifest for a set period of time in seconds|
|[Signals](/operators/signals/)|	Send signals like SIGINT or SIGHUP to running processes.|
|[Tarball](/operators/tarball/)|	Extract a tarball to a specified location, removing the tarball after extraction, without having to have tar installed on the system.|
|[Template](/operators/templates/)|	Render templates with injected variables and environment variables, which allows for stable system configurations across multiple environments.|

Each operator has its own set of properties and behavior, which will be discussed in detail in the following sections.

In the next section, we will explore each operator in more detail and provide examples of their usage in a bruce manifest file.
