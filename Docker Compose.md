# How To Install and Use Docker Compose on Ubuntu 22.04

Introduction
Docker simplifies the process of managing application processes in containers. While containers are similar to virtual machines in certain ways, they are more lightweight and resource-friendly. This allows developers to break down an application environment into multiple isolated services.

For applications depending on several services, orchestrating all the containers to start up, communicate, and shut down together can quickly become unwieldy. Docker Compose is a tool that allows you to run multi-container application environments based on definitions set in a YAML file. It uses service definitions to build fully customizable environments with multiple containers that can share networks and data volumes.

In this guide, you’ll demonstrate how to install Docker Compose on an Ubuntu 22.04 server and how to get started using this tool.

Prerequisites
To follow this article, you will need:

Access to an Ubuntu 22.04 local machine or development server as a non-root user with sudo privileges. If you’re using a remote server, it’s advisable to have an active firewall installed. To set these up, please refer to our Initial Server Setup Guide for Ubuntu 22.04.
Docker installed on your server or local machine, following Steps 1 and 2 of How To Install and Use Docker on Ubuntu 22.04.
Note: Starting with Docker Compose v2, Docker has migrated towards using the compose CLI plugin command, and away from the original docker-compose as documented in our previous Ubuntu 20.04 version of this tutorial. While the installation differs, in general the actual usage involves dropping the hyphen from docker-compose calls to become docker compose. For full compatibility details, check the official Docker documentation on command compatibility between the new compose and the old docker-compose.

Step 1 — Installing Docker Compose
To make sure you obtain the most updated stable version of Docker Compose, you’ll download this software from its official Github repository.

First, confirm the latest version available in their releases page. At the time of this writing, the most current stable version is 2.3.3.

Use the following command to download:

mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
Next, set the correct permissions so that the docker compose command is executable:

chmod +x ~/.docker/cli-plugins/docker-compose
To verify that the installation was successful, you can run:

docker compose version
You’ll see output similar to this:

Output
Docker Compose version v2.3.3
Docker Compose is now successfully installed on your system. In the next section, you’ll see how to set up a docker-compose.yml file and get a containerized environment up and running with this tool.