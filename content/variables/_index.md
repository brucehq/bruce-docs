---
title: "Variables & Properties"
weight: 4
---
Variables within brucedom are effectively environment variables that are read from the current environment but also set in the current running process to ensure that they are available to all operators.  Variables can be set in a number of ways, including: The variables section in the main manifest.  Setting them in the environment prior to running the bruce command.  Setting them in the environment properties file.  Setting them in the command line.  Finally you can also use the set env capabilities of the operators like command to set a value for use.

## Variable **Order of Precedence**
Variables are loaded in a very specific order in order to ensure that you can override the values with maximum flexibility.  The order of precedence is as follows:
1. Pre set environment variables
2. Variables in manifest being executed
3. Properties file specified from `-p` or `--property-file` flag
4. Operators like cmd calling the setEnv capability

## Pre set environment variables

These are the environment variables that are pre-set on every machine for the current user that you are running as.  That ensures that you have all the data available for execution.  These variables are also set outside of scope of bruce but are part of the operating environment as set up by the OS and the user.  These variables are available to all operators and templates, as well as all other applications on the OS.

## Variables in manifest being executed

The main manifest file may look something like this:
```yaml
variables:
  ServiceOwner: www-data
  RotateDays: 7
  VHOST_ROOT: /opt/vhosts/hello-world
steps:
- cmd: apt install -y nginx logrotate
```
This is the most common way to establish variables for the operators to make use of.  The service owner, and remote days as well as the vhost document root are set and can now be used by the operators and templates.  Operators use template variable notation eg. `{{.ServiceOwner}}` to reference the variable.  Templates use the golang text/template notation eg. `{{.ServiceOwner}}` to reference the variable.

Both operators and templates can make use the full range of golang text/template functions and operators to manipulate the variables as needed.  For example you can use the `printf` function to format the variable as needed.  For example you can use the following to format the RotateDays variable as a string with a leading zero if it is less than 10.

```yaml
- cmd: echo {{printf "%02d" .RotateDays}}
  setEnv: RotateDays
```

## Properties file specified from `-p` or `--property-file` flag

The properties file is a file that contains a list of key value pairs that are loaded into the environment prior to execution.  This allows you to pre-set a set of variables that can be used by the operators and templates.  This is a great way to set up a set of variables that can be used across multiple executions.  For example you can set up a properties file that contains the following:
```yaml
ServiceOwner=www-data
RotateDays=7
VHOST_ROOT=/opt/vhosts/hello-world
```
### Properties file for different environments

Second to this a standard pattern is to create different properties files for different environments.  For example you can create a properties file for your dev environment, one for your staging environment and one for your production environment.  This allows you to have a single manifest file that can be used across all environments but the properties file will be different for each environment.  For example you can have a properties file for your dev environment that contains the following:
```yaml
AppEnv=dev
Endpoint=https://dev.example.com
```
And then you can have a properties file for your staging environment that contains the following:
```yaml
AppEnv=staging
Endpoint=https://staging.example.com
```

## Operators like cmd calling the setEnv capability

The command operator provides a means to take the current output of the command and set it as a variable.  This allows you to override behavior that was previously set with the current operating environment.  This is extremely useful as you may want to extract a value from the current operating system and then use it in a template or other operator.  For example you can use the following command to extract the IP address of the current server and then use it in a template to set the domain name of a virtual host.
```yaml
- cmd: ip addr show $(ip route | awk '/default/ {print $5}') | awk '/inet / {print $2}' | awk -F/ '{print $1}'
  setEnv: Domain