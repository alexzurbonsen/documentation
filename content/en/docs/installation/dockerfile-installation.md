---
title: "Dockerfile Installation"
description: "Dockerfile Installation"
lead: ""
date: 2019-06-06T08:49:15+00:00
draft: false
images: []
---

Having done all the steps as instructed on [Installation Overview →]({{< relref "installation-overview" >}}), you can now proceed to the Dockerfile installation of our tool.

## Dockerfiles method

The Dockerfiles will provide you with a running setup of the working system with just a few commands.

It can technically be used in production, however it is designed to run on your local machine for testing purposes.

The system binds in your host OS to port 8000. So it will be accessible through ```http://metrics.green-coding.local:8000```

Please set an entry in your ```/etc/hosts``` file accordingly like so:

```bash
127.0.0.1 api.green-coding.local metrics.green-coding.local
```

### Setup

- Open the ```compose.yml.example``` change the default password and save the file as ```compose.yml```
- Build and run with ```docker compose up```
- The compose file uses volumes to persist the state of the database even between rebuilds. If you want a fresh start use: ```docker compose down -v && docker compose up```
- To start in detached mode just use ```docker compose -d```

### Connecting to DB
You can now connect to the db directly on port 5432, which is exposed to your host system.\
The expose to the host system is not needed. If you do not want to access the db directly just remove the ```5432:5432``` entry in the ```compose.yml``` file.

The database name is ```green-coding```, user is ```postgres```, and the password is what you have specified during the ```compose.yml``` file.

### Limitations
These Dockerfiles are not meant to be used in production. The reason for this is that the containers depend on each other and have to be started and stopped alltogether, and never on their own.


## Architecture explanation:
- The postgres container has a volume mount. This means that data in the database will persists between container removals / restarts
- The interconnect between the gunicorn and the nginx container runs through a shared volume mount in the filesystem. Both use the user ```www-data``` to read and write to
a UNIX socket in ```/tmp```
- all webserver configuration files are mounted on start of the container as read-only. This allows for changing configuration of the server through git-pull / yourself
without having to rebuild the docker image.
- postgresql can detect changes to the structure.sql. If you issue a ```docker compose down -v``` the attached volume will be cleared and the postgres container
will import the database structure fresh.