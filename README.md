Cloud9 IDE with MEAN.JS
================

[![MEAN.JS Logo](http://meanjs.org/img/logo-small.png)](http://meanjs.org/)  
<a href="https://c9.io/?redirect=0">
<img src="https://cdn.c9.io/nc-3.1.2777-37571e6c-wf/static/plugins/c9.profile/static/images/cloud9-logo.svg" width="120">
</a>


This repository contains Dockerfile Cloud9 and MEAN.JS for my exercise.  I will make readme clear step by step.
The Cloud9 IDE with some usefull features for convenience and secure development environment for Docker's automated build published to the public Docker Hub Registry.
MEAN.JS is a full-stack JavaScript open-source solution, which provides a solid starting point for [MongoDB](http://www.mongodb.org/), [Node.js](http://www.nodejs.org/), [Express](http://expressjs.com/), and [AngularJS](http://angularjs.org/) based applications. The idea is to solve the common issues with connecting those frameworks, build a robust framework to support daily development needs, and help developers use better practices while working with popular JavaScript components.

## Before You Begin
Before you begin we recommend you read about the basic building blocks that assemble a MEAN.JS application:
* MongoDB - Go through [MongoDB Official Website](http://mongodb.org/) and proceed to their [Official Manual](http://docs.mongodb.org/manual/), which should help you understand NoSQL and MongoDB better.
* Express - The best way to understand express is through its [Official Website](http://expressjs.com/), which has a [Getting Started](http://expressjs.com/starter/installing.html) guide, as well as an [ExpressJS](http://expressjs.com/en/guide/routing.html) guide for general express topics. You can also go through this [StackOverflow Thread](http://stackoverflow.com/questions/8144214/learning-express-for-node-js) for more resources.
* AngularJS - Angular's [Official Website](http://angularjs.org/) is a great starting point. You can also use [Thinkster Popular Guide](http://www.thinkster.io/), and [Egghead Videos](https://egghead.io/).
* Node.js - Start by going through [Node.js Official Website](http://nodejs.org/) and this [StackOverflow Thread](http://stackoverflow.com/questions/2353818/how-do-i-get-started-with-node-js), which should get you going with the Node.js platform in no time.

## features:
- Auto protect the IDE with user defined (or default) password.
- SSH access to the container using user defined(or generated) password and or user defined SSH key.
- Custom container workspace directory (make it easier to link with VOLUME_FROM other container, not just host directory mapping).
- Optimized build process (please suggest if any idea to make it better)

# Base Docker Image
[tutum/ubuntu:trusty](https://registry.hub.docker.com/u/tutum/ubuntu/)

# Installation

## Install Docker.

Download automated build from public Docker Hub Registry: 

    docker pull agungf/cloud9-ide

alternatively, you can build an image from Dockerfile:

    docker build -t="$USER/cloud9-ide" github.com/agungf/cloud9-ide
    
    
## Basic Usage

    docker run -it -d -p 8181:8181 -p 2222:22 agungf/cloud9-ide
    
It will take care all the defaults to:

- Cloud9 Basic http auth User `root` , with DEFAULT password: `secret`
- See Auto generated SSH password for root at log, `docker logs <continer instance name>`
- Workspace directory at `/cloud9/workspace` 
    
You can add a workspace as a volume directory with the argument *-v /your-path/workspace/:cloud9/workspace* like this :

    docker run -it -d -p 8181:8181 -v /your-path/workspace/:/cloud9/workspace agungf/cloud9-ide


## Advance Usage

Get the latest version from github

    git clone https://github.com/agungf/cloud9-ide
    cd cloud9-ide/

Run with docker compose:

    docker-compose up -d
    
Example docker-compose.yml:

    ide:
      build: .
      environment:
        - ROOT_PASS=thesecrets
        - C9_WORKSPACE=/data/workspace
      volumes_from:
        - data
      ports:
        - 8181:8181
        - 22
    data
        image:tutum/ubuntu
        volumes:
        - /data/workspace


It will set the parameters to:

- Cloud9 Basic hhtp Auth User `root` , with password: `thesecrets`
- SSH root password : `thesecrets`
- Workspace directory at `/data/workspace` linked to VOLUME_FROM `data` container
 

## Set SSH Key
 
 [See tutum/ubuntu README](https://github.com/tutumcloud/tutum-ubuntu/blob/master/README.md)


Happy Coding !!
