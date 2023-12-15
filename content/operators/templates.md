---
title: "Templates Operator"
weight: 10
---
The Templates operator is used to create and manage template files on the system. It also allows injecting variables from commands or provided input data.

## Syntax

```yaml
template: <TEMPLATE_PATH>
source: <REMOTE_LOCATION>
perms: <PERMISSIONS>
owner: <OWNER>
group: <GROUP>
vars:
  - type: <TYPE>
    input: <INPUT>
    variable: <VARIABLE>
osLimits: <OS_LIMITS>
```

* `template`: The local path where the template file will be saved.
* `source`: The URL or path to the template file's source location.
* `perms`: The file permissions to set (e.g., 0664).
* `owner`: The owner of the file.
* `group`: The group owner of the file.
* `vars`: A list of variables to inject into the template.
* `type`: The type of variable source (e.g., value).
* `input`: The input value or expression to evaluate.
* `variable`: The variable name to use in the template.
* `osLimits`: A list of operating systems that the operator should run on.

## Example:

```yaml
template: /etc/nginx/nginx.conf
source: https://raw.githubusercontent.com/configset/cfs/main/examples/nginx/templates/etc/nginx/nginx.conf
perms: 0664
owner: root
group: root
vars:
  - type: value
    input: nginx|apt=www-data
    variable: NGINX_USER
osLimits: all
```

In this example, the Templates operator downloads the Nginx configuration file from the provided URL and saves it to /etc/nginx/nginx.conf with the specified permissions, owner, and group. It also injects the variable NGINX_USER with the value nginx or www-data, depending on the operating system.
