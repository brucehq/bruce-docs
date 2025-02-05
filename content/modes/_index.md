---
title: "Operating Modes"
weight: 1
---

As mentioned before Bruce currently runs in one of 2 operating modes.  The default and most commonly used operating mode is execution mode.  Second to that is server mode.

## Execution Mode

Majority of the documentation here is centralized on execution mode as that is what is at the heart of bruce.  Execution mode makes use of a manifest file to execute a list of steps to configure / build / deploy or run a set of run books in a 
reproducible manner on the respective machine you are on.  As seen in the getting started guide and the previous CLI application start guide. A manifest consists of variables and steps of operators which will execute in order as a sequence.

Since the vast majoirty of the documentation already focuses on this behaviour, within this section we will concentrate on the secondary execution mode.

## Server Mode.

Server mode is intended for bruce to enter an always on listening mode and execute specific manifests based on a trigger.  Triggers can be both events that occur and are sent by the bruce.tools backend.  Or they are cadence based events, which 
are events triggered based on a specific time cadence.  This allows you for instance to upload a file to S3 every 5 minutes for example.  Or truncate log files every 30 minutes and so on.

Event mode in contrast is slightly different in that you still set up different manifests that will be executed, but each manifest is coded to a specific action name.  Each manifest file must also include a default action.
Since an action corresponds to a manifest it allows you to effectively set up run books for your server, deployment pipelines or even agentic workflows for different models to hand of jobs.  This is an extremely important feature of bruce.

Server mode as mentioned before still requires a manifest file, but it is slightly different from that of a normal execution flow.

Let's take a look at how you may set this up.

First and foremost, since we are on a linux server we will make use of a SystemD unit file in order to start bruce in server mode and to keep it running.
### SystemD Unit File
```bash
[Unit]
Description=Bruce Server Instance
After=network-online.target
Wants=network-online.target

[Service]
User=root
Group=root
TimeoutStartSec=10
Restart=always
Environment="APP_ENV=dv"
ExecStart=/usr/local/bin/bruce server /some/deploy/path/install.yml

[Install]
WantedBy=multi-user.target
```

## Setting the bruce server configuration.
As mentioned before the server configuration file looks slightly different from a regular execution file:
### Example configuration for server mode:
```yaml
---
endpoint: wss://brucedom.com/workers
runner-id: 4e9eaaxb-8v50-418b-9013-cda07820ffc4
authorization: f9d6258z-0dbc-5gb4-a94d-13x95e5ea2f7
execution:
  - name: run all default
    action: default # you must have a default action.
    type: event # can also be cadence
    cadence: 10 # execution in minutes if cadence is chosen
    target: test.yaml # should be the path to the manifest to be executed, in this case main branch example config
  - name: Runs an action event 
    action: SecondTest #executes the action "SecondTest" which is registered on brucedom.com and tagged to this runner.
    type: event
    target: /tmp/test2.yaml 
  - name: Parse Files in Dir every 5 minutes
    action: ThirdTest
    type: cadence
    cadence: 5
    target: /tmp/parsefiles.yaml
```

In the above example we have a few different execution types. It will connect to the provided websocket endpoint and authenticate with the provided runner-id and authorization token.  It will then register itself for events and start listening for events to occur.  When an event occurs it will trigger the manifest file to run assocated with either the default or a specific "action" that you have defined.  The first execution type is an event driven execution for the default runner.  Each runner when registered on brucedom.com has it's own execution endpoint which can be triggered. The second execution type is a event driven execution and will trigger the "SecondTest" action which was registered on brucedom.com and tagged with this runner.  The third execution type is a cadence driven execution but it will run the manifest file every 5 minutes.

Note that this server configuration file can be deployed anywhere on the server where bruce will have access to.  As example you may choose to run bruce in non root mode which will require you to set the server configuration file in a proper 
location.

## Changes to the file.

Whenever a change to the manifest file is done you must restart the service.  For instance running: `systemctl restart bruce`