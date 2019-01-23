# Docker project used to deploy BDMER3 with nginx and couchdb

#### Required: ####
  - docker
  - docker-compose

## Installation : ##

1. Clone git repository

`git clone git@github.com:sylviefiat/bdmer_deploy.git`

2. Run docker compose in order to start databse and app:

`docker-compose up`

## Automatise start with server with Systemctl ##

1. Go to

`cd /usr/lib/systemd/system/`

2. Create start file

` vi bdmer.service`

```
[Unit]
Description=bdmer
Requires=docker.service
After=docker.service

[Service]
User=root
ExecStartPre=/usr/local/bin/docker-compose -f /opt/docker/bdmer_deploy/docker-compose.yml down
ExecStart=/usr/local/bin/docker-compose -f /opt/docker/bdmer_deploy/docker-compose.yml up
ExecStop=/usr/local/bin/docker-compose -f /opt/docker/bdmer_deploy/docker-compose.yml stop

[Install]
WantedBy=multi-user.target
```

3. enable on start

`systemctl enable bdmer`

