---
title: "Server Operator"
weight: 11
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
ExecStart=/usr/local/bin/bruce --config=/some/deploy/path/install.yml server

[Install]
WantedBy=multi-user.target
```

## Getting up and running.
Above is a simple example of a systemd unit file that is used to trigger bruce and initialize it as a server on port 3619.  The ExecStart will run bruce with the specified manifest file (/some/deploy/path/install.yml), if the manifest does not exist it will fail with an error.  At this point bruce will just listen if any curl / wget or other http commands hit the server for instance:
```bash
curl http://some-host.somedomain.net:3619
```
The URL above should reflect your current server you want to trigger. Based on the trigger above bruce will start to execute it's manifest file that exists at the specified path.  This manifest is a standard bruce manifest file so you can have it download a zip file from s3 extract it and run it or whatever your heart desires.


### NOTE:
* Attempting to trigger bruce to start multiple times will cause you to receive a 429 response from the server.  It will only allow a single run to occur at a time, once the run is complete it will allow you to start again.  You may also use this indirectly to check if a run is still in progress should you need to.

## Server Command options

* `--config` <config file path> that the server will run every time a trigger happens
* `--server-port OR -P` the port that the server will listen on (default 3619)


## Possible future additions

Running the server operator as a cluster operator to allow for single node deployments behind a load balancer, in the event of a failure it would "taint" that node and all following triggers would then only occur on the failed node to ensure you can achieve a correct state before it will allow the follow up triggers to run on additional nodes.  If this is something you are interested in feel free to submit an issue as a feature request for this.
