---
title: "Client Application Usage"
weight: 1
---
## Overall Usage
To install the application please see the [installation](/cli-application/install) page.

CFS has many built in operators and actions that can be performed.  The following is a list of the available commands and their usage.  This list can be produced by running the cfs --help command once the application is installed.

```bash
cfs --help
NAME:
   cfs - Start with: /path/to/cfs https://someinstallhost/installme.yml

USAGE:
   cfs [global options] command [command options] [arguments...]

COMMANDS:
   install, setup  this is the default action and will be run if no commands are specified
   search, find    this will search the ConfigSet repository for a related manifest
   view, open      this command opens the manifest for you to view in CLI prior to executing install
   create          this command will create a new manifest or template for you to upload directly to your configset.com account and then install, you must have CFS_KEY env variable set to your API key from configset.com
   edit            this command will edit a manifest or template by re-uploading to your configset.com account, you must have CFS_KEY env variable set to your API key from configset.com, name and description can be edited directly on configset.com
   upgrade         this command will upgrade the cfs application to the latest version
   version         this prints the current version of cfs and the current latest version of cfs
   help, h         Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --config value                   See docs for supported endpoints, eg: https://s3.amazonaws.com/somebucket/my_install.yml (default: "/etc/cfs/config.yml")
   --property-file value, -p value  Loads properties from a file, eg: /etc/cfs/properties.yml to be used as environment variables for operators and templates
   --debug, -d                      Enable debug logging (default: false)
   --help, -h                       show help
```


## Install
This is the default operator within CFS if you point the client library to a manifest file it will make use of this operator in order to install it, it effectively just loads the variables and iterates over steps to install / configure whatever is defined in the manifest file.

## Search
This command allows you to search the ConfigSet repository for a manifest/template that you may be useful for your usecase.  For example if you are looking for a manifest that will install Nginx you can run the following command:

```bash
cfs search nginx
```

By default the search command will search manifest files if you choose you can also use a subcommand to direct search to find template files instead of manifest files. The search command has 2 sub commands and they are as follows:

```bash
cfs search manifest nginx
cfs search template nginx
```

While the search action defaults to manifests using teh templates subcommand will allow you to search for specific tempaltes that have been created, this could be useful if someone created a template for a kafka properties file and you intend to use it.

## View
The view command is a built in capability that keeps you on the command line without the need to go to the web to inspect a manifest file or template file.  This is a great way to quickly inspect a manifest file prior to running it.  The view command has 2 sub commands and they are as follows:

```bash
cfs view https://configset.com/api/manifests/7cc81042-b638-5260-bd09-2e6066fbfc46
```
Think of this as a curl command without having to have curl installed.  But be careful when you use this command on items that are not on configset.com.

## Create
The create command is a built in capability that allows you to create a new manifest or template file directly from the command line.  This is a great way to quickly create a manifest file or template file without having to go to the web to create it.  The create command has 2 sub commands for creating manifests and templates respectively and they are as follows:

```bash
cfs create manifest
cfs create template
```
Please note that the create command does require that you have a token configured for the configset.com site and it must be set in your environment prior to being able to use it.  If it is not set you will see the following error message, when trying to run the create command.  Private hosting and securing of templates, manfests and vault linking is planned for the future.
    
```bash
CFS_KEY environment variable not set, please set this to your API key from configset.com
```

## Edit
The edit command is a built in capability that allows you to edit a manifest or template file directly from the command line.  This is a great way to quickly edit a manifest file or template file without having to go to the web to edit it.  The edit command has 2 sub commands for editing manifests and templates respectively and they are as follows:

```bash
cfs edit manifest
cfs edit template
```
Similar to the create command you must have first set your CFS Key in order to make use of the edit command.

## Upgrade
The upgrade command is a built in capability that allows you to upgrade the cfs application to the latest version.  This is a great way to quickly upgrade the cfs application without having to go to the web to download it.  The upgrade command has no sub commands and is run as follows:

```bash
cfs upgrade
```
Please note that if your `cfs` application is installed into a location like /usr/local/bin you will need to run this command with elevated privileges. An example of this may look like:
```bash
sudo cfs upgrade
```

## Version
This will show the current version of the cfs application as deployed on your system as well as the latest published version of the cfs application.  This is a great way to quickly check if you are running the latest version of the cfs application.  The version command has no sub commands and is run as follows:

```bash
cfs version
```

## Help
This will show the help for the cfs application.  This is a great way to quickly check the usage of the cfs application.  The help command has no sub commands and is run as follows:

```bash
cfs help
```
All new functionality will be added to the help command as it is added to the cfs application.

# Global Options
The following commands provide the options that make each of the operators function.  While these are global options not all operators support the global options, for instance providing a properties file while doing a cfs search will net you no installation results and will just follow the functionality of the operator itself, which is to search for manifests.

## Config
The config file is a yaml manifest that contains the variables as well as the steps responsible for setting up or deploying applicaitons. For standard functionality the config file, you can pass the config file without the need of the parameter name.  For example:

```bash
cfs /path/to/install-manifest.yml
```
or
```bash
cfs --config /path/to/install-manifest.yml
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
The debug flag enables debug logging for the cfs application.  This is a great way to see what is happening behind the scenes when you are running the cfs application.  When you supply it all of the operators will output debug information to the console.  For example:

```bash
cfs --debug /path/to/install-manifest.yml
```

## Help
The help flag will show the help for the cfs application.  This is where you will find usage information for the cfs client application.