# How To Install and Use Docker Compose on Ubuntu 22.04

## Introduction
Docker simplifies the process of managing application processes in containers. While containers are similar to virtual machines in certain ways, they are more lightweight and resource-friendly. This allows developers to break down an application environment into multiple isolated services.

For applications depending on several services, orchestrating all the containers to start up, communicate, and shut down together can quickly become unwieldy. Docker Compose is a tool that allows you to run multi-container application environments based on definitions set in a YAML file. It uses service definitions to build fully customizable environments with multiple containers that can share networks and data volumes.

In this guide, you’ll demonstrate how to install Docker Compose on an Ubuntu 22.04 server and how to get started using this tool.

Prerequisites
To follow this article, you will need:

Access to an Ubuntu 22.04 local machine or development server as a non-root user with sudo privileges. If you’re using a remote server, it’s advisable to have an active firewall installed. To set these up, please refer to our Initial Server Setup Guide for Ubuntu 22.04.
Docker installed on your server or local machine, following Steps 1 and 2 of How To Install and Use Docker on Ubuntu 22.04.
Note: Starting with Docker Compose v2, Docker has migrated towards using the compose CLI plugin command, and away from the original docker-compose as documented in our previous Ubuntu 20.04 version of this tutorial. While the installation differs, in general the actual usage involves dropping the hyphen from docker-compose calls to become docker compose. For full compatibility details, check the official Docker documentation on command compatibility between the new compose and the old docker-compose.

## Step 1 — Installing Docker Compose
To make sure you obtain the most updated stable version of Docker Compose, you’ll download this software from its official Github repository.

First, confirm the latest version available in their releases page. At the time of this writing, the most current stable version is 2.3.3.

Use the following command to download:
```
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose`
```
Next, set the correct permissions so that the docker compose command is executable:

`chmod +x ~/.docker/cli-plugins/docker-compose`

To verify that the installation was successful, you can run:

`docker compose version`

Docker Compose is now successfully installed on your system. In the next section, you’ll see how to set up a `docker-compose.yml` file and get a containerized environment up and running with this tool.

## Step 2 — Setting Up a docker-compose.yml File
To demonstrate how to set up a docker-compose.yml file and work with Docker Compose, you’ll create a web server environment using the official Nginx image from Docker Hub, the public Docker registry. This containerized environment will serve a single static HTML file.

Start off by creating a new directory in your home folder, and then moving into it:
```
mkdir ~/compose-demo
cd ~/compose-demo
```
In this directory, set up an application folder to serve as the document root for your Nginx environment:

`mkdir app`

Using your preferred text editor, create a new index.html file within the app folder:

`nano app/index.html`
Place the following content into this file:

~/compose-demo/app/index.html
``` html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Docker Compose Demo</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/kognise/water.css@latest/dist/dark.min.css">
</head>
<body>

    <h1>This is a Docker Compose Demo Page.</h1>
    <p>This content is being served by an Nginx container.</p>

</body>
</html>
```
Save and close the file when you’re done. If you are using nano, you can do that by typing CTRL+X, then Y and ENTER to confirm.

Next, create the docker-compose.yml file:

nano docker-compose.yml
Insert the following content in your docker-compose.yml file:

docker-compose.yml
version: '3.7'
services:
  web:
    image: nginx:alpine
    ports:
      - "8000:80"
    volumes:
      - ./app:/usr/share/nginx/html
The docker-compose.yml file typically starts off with the version definition. This will tell Docker Compose which configuration version you’re using.

You then have the services block, where you set up the services that are part of this environment. In your case, you have a single service called web. This service uses the nginx:alpine image and sets up a port redirection with the ports directive. All requests on port 8000 of the host machine (the system from where you’re running Docker Compose) will be redirected to the web container on port 80, where Nginx will be running.

The volumes directive will create a shared volume between the host machine and the container. This will share the local app folder with the container, and the volume will be located at /usr/share/nginx/html inside the container, which will then overwrite the default document root for Nginx.

Save and close the file.

You have set up a demo page and a docker-compose.yml file to create a containerized web server environment that will serve it. In the next step, you’ll bring this environment up with Docker Compose.
