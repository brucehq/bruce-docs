---
title: "Manifest Files"
weight: 2
---

Manifest files are the core building blocks of cfs. They are used to describe the desired state of your infrastructure and define the actions, components, and configurations required for a specific task. Manifest files are written in a simple, easy-to-understand language that is both human-readable and machine-parseable.

## Structure of a Manifest File

A manifest file is divided into two main sections: `variables` and `steps`. The `variables` section is used to define any variables that will be used within the manifest file. The `steps` section is used to define the actions that will be taken to achieve the desired state of the infrastructure.  Variables defined here can also be overwritten by using a properties file or by overwriting them with the setEnv flag in a command step.  This allows for maximum flexibility where you can download a pre-configured manifest file and then overwrite the variables to suit your needs.  Please note that if you make use of templates that are referenced in the manifest file, your templates will make use of the same variables that are set.

NOTE: Variables that are defined are only available within the execution, and do not persist after the execution is complete.  This is important to note as we will be introducing a vault feature in the future that will allow you to interact with HashiCorp, retrieve a value, quickly set / use it as a command for bootstrapping purposes and then it's removed when the execution is complete, without bleeding into the regular operating system.

Below is an example of a manifest file that can be used to set up a basic Nginx web server, it is also published on configset.com and you can execute it with: `cfs https://configset.com/api/manifests/d616af8e-9663-5a68-be93-9af0e3013ae6/data`

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
  remoteLocation: https://configset.com/api/templates/7cc81042-b638-5260-bd09-2e6066fbfc46/data

# Create a symlink for the virtual host
- cmd: ln -sf /etc/nginx/sites-available/hello-world /etc/nginx/sites-enabled/hello-world

# Clone the static HTML repo
- gitRepo: https://github.com/configset/static-content-example.git
  dest: VHOST_ROOT

- template: /etc/logrotate.d/nginx
  remoteLocation: https://configset.com/api/templates/9095d69e-e419-57bc-b888-08e8a60fc11a/data

# Enable and start the Nginx service
- service: nginx
  setEnabled: true
  state: started
  restartTrigger:
  - /etc/nginx/sites-available/hello-world
```


In the above referenced structure you can see that we first define a set of variables, ServiceOwner and RotateDays are used by the manifest file to set up the logrotate configuration.  The VHOST_ROOT variable is used to define the location of the static content that will be served by Nginx.  The Domain variable is used to set the domain name of the virtual host that will be created.  The Domain variable is set by executing a command that will retrieve the IP address of the server and set it as the Domain variable.  This is a great example of how you can use a command to retrieve a value and then use it in a template or other step.  The domain variable is later used within the template step to set the domain name of the virtual host.  For reference to the template that uses this variable (click here)[https://configset.com/api/templates/7cc81042-b638-5260-bd09-2e6066fbfc46/data].

## Available Operators

cfs provides a wide range of operators that cater to various use cases. Some of the most common operators include:

- Tarball: Download and extract a tarball to a specified directory.
- Command: Execute a command on the system.
- Copy: Make a copy of a file or directory.
- Cron: Set up a cron task.
- Git: Checks out a git repository, without the need to have git installed on the system.
- PackageRepo: Set up a package repository, such as apt or yum.
- Packages: Install a package based on the system type.
- Services: Set up a service to start and ensure the application runs with the service.
- Signals: Send a signal to a specific process.
- Templates: Load a template and write it to the local filesystem.

Future operators will include:
GithubRelease: Ability to download a particular github release (or latest) and extract it to a specified directory.
RecursiveCopy: Ability to recursively copy targets (http/https, s3, localhost, etc.) to a local directoy.  Useful for copying a directory from a remote server to a local server, this was requested for copying weights for ML models, from remote servers to local servers.
Vault: Ability to interact with HashiCorp Vault and retrieve a value, quickly set / use it as a command for bootstrapping purposes.

Each operator has its own set of properties and behavior, which will be discussed in detail in the following sections.

In the next section, we will explore each operator in more detail and provide examples of their usage in a cfs manifest file.
