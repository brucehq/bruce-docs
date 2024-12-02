---
title: "Server Operator"
weight: 12
---
The server operator allows you to run bruce as a server on a remote server.  The purpose of this is to allow you to easily trigger a new continuous deployment without having to access the system remotely through ssh etc.  There is a catch however, you cannot just run arbitrary commands via the listening port.  The server operator will listen by default on port 3619 as an http server.  It will accept GET / POST / PUT commands and will execute the config file you specify during the run.

Lets take a look at how you may set this up.

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

## Getting up and running.
Above is a simple example of a systemd unit file that is used to start bruce in server mode.  The ExecStart will start bruce and use the /some/deploy/path/install.yml as the config file to run.  During the startup process bruce will run in two primary modes.  Cadence, and Event driven mode.  The two modes can both be used at the same time also.  The cadence mode will run every x minutes by and will execute the manifest file you have provided at said cadence.  The event driven mode will create a websocket connection to the provided bruce server, authenticate and register itself for events at which point it will start listening for events to occur.  When an event occurs it will trigger the manifest file to run assocated with either teh defaault or a specific "action" that you have defined.

### Example configuration for server mode:
```yaml
---
endpoint: ws://brucedom.com/workers
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


