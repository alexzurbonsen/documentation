---
title : "Example applications"
description: "Example applications."
lead: ""
date: 2022-06-18T08:49:15+00:00
draft: false
images: []
---

## Structure
All of our example applications the same structure:

```
.
├── usage_scenario.json
├── Dockerfile
├── compose.yml
├── README.md
└── ...
```

- `usage_scenario.json`
- `Dockerfile` is needed in order for you to reproducibly build the container that will be used later in the measurement.
- `compose.yml` is only used for development / demo purposes if you wanna see what the application does in your terminal / browser / desktop.
- *...* is either a file, a folder or missing.
    - It contains supplemental files that are needed to build the `Dockerfile` and / or to make a bind-volume for the `compose.yml` be missing /will be a file / will be a folder. This contains the supplemental Code that the

Please check out our repository of example applications on Github: [Example Applications Repo](https://www.github.com/green-coding-berlin/green-metrics-tool/demo-containers)

## Demoing the example application (optional)

```bash
docker compose
```
See in the `README.md` where to view output if present and how to trigger the application.

If you just want to run a part of our example application or debug run
```bash
docker compose run SERVICE bash
```
Replace **SERVICE** with the relevant service in the `compose.yml`

## Building the example application

```bash
docker build .
```

What you get is an image in your `docker images` that is used in the [usage_scenario.json →]({{< relref "usage-scenario" >}})

 ## Measuring the example applications

To run the measurements please refer to: [Measuring locally →]({{< relref "measuring-locally" >}})

## Containerizing and measuring own applications

Please refer to [Containerizing and measureing own applications →]({{< relref "containerizing-applications" >}})