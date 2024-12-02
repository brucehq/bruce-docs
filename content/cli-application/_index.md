---
title: "Client Application Usage"
weight: 1
---
## Overall Usage
To install the application please see the [installation](/cli-application/install) page.

Bruce has many built in operators and actions that can be performed.  The following is a list of the available commands and their usage.  This list can be produced by running the bruce --help command once the application is installed.

```bash
bruce --help
NAME:
   bruce - Start with: /path/to/bruce https://someinstallhost/installme.yml

USAGE:
   bruce [global options] command [command options] [arguments...]

COMMANDS:
   install, setup  this is the default action and will be run if no commands are specified
   upgrade         this command will upgrade the bruce application to the latest version
   version         this prints the current version of bruce and the current latest version of bruce
   help, h         Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --config value                   See docs for supported endpoints, eg: https://s3.amazonaws.com/somebucket/my_install.yml (default: "/etc/bruce/config.yml")
   --property-file value, -p value  Loads properties from a file, eg: /etc/bruce/properties.yml to be used as environment variables for operators and templates
   --debug, -d                      Enable debug logging (default: false)
   --help, -h                       show help
```


## Install
This is the default operator within CFS if you point the client library to a manifest file it will make use of this operator in order to install it, it effectively just loads the variables and iterates over steps to install / configure whatever is defined in the manifest file.

## Upgrade
The upgrade command is a built in capability that allows you to upgrade the bruce application to the latest version.  This is a great way to quickly upgrade the bruce application without having to go to the web to download it.  The upgrade command has no sub commands and is run as follows:

```bash
bruce upgrade
```
Please note that if your `bruce` application is installed into a location like /usr/local/bin you will need to run this command with elevated privileges. An example of this may look like:
```bash
sudo bruce upgrade
```

## Version
This will show the current version of the bruce application as deployed on your system as well as the latest published version of the bruce application.  This is a great way to quickly check if you are running the latest version of the bruce application.  The version command has no sub commands and is run as follows:

```bash
bruce version
```

## Help
This will show the help for the bruce application.  This is a great way to quickly check the usage of the bruce application.  The help command has no sub commands and is run as follows:

```bash
bruce help
```
All new functionality will be added to the help command as it is added to the bruce application.

# Global Options
The following commands provide the options that make each of the operators function.  While these are global options not all operators support the global options, for instance providing a properties file while doing a bruce search will net you no installation results and will just follow the functionality of the operator itself, which is to search for manifests.

## Config
The config file is a yaml manifest that contains the variables as well as the steps responsible for setting up or deploying applicaitons. For standard functionality the config file, you can pass the config file without the need of the parameter name.  For example:

```bash
bruce /path/to/install-manifest.yml
```
or
```bash
bruce --config /path/to/install-manifest.yml
```
is the exact same functionality.

## Property File
While manifest files have variable section defined in them the property file enables you to override these variables with a set of variables that are loaded into the environment prior to execution.  This allows you to pre-set a set of variables that can be used by the operators and templates.  This is a great way to set up a set of variables that can be used across multiple executions.  For example you can have a properties file for your dev environment that contains the following:
```yaml
AppEnv=dev
Endpoint=https://dev.example.com
```

And then you can have a properties file for your staging environment that contains the following:
```yaml
AppEnv=staging
Endpoint=https://staging.example.com
```

## Debug
The debug flag enables debug logging for the bruce application.  This is a great way to see what is happening behind the scenes when you are running the bruce application.  When you supply it all of the operators will output debug information to the console.  For example:

```bash
bruce --debug /path/to/install-manifest.yml
```

## Help
The help flag will show the help for the bruce application.  This is where you will find usage information for the bruce client application.