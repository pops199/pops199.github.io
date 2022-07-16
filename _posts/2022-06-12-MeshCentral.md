---
title: Installing MeshCentral on AWS
date: 2022-06-12 14:55:00 -500
categories: [guides, cloud-hosting]
tags: [servers,guides,meshcentral,aws,cloud]  # Tag names should always be lowercase
published: true
---

![MeshCentral](https://repository-images.githubusercontent.com/101663032/a0f76700-4b4f-11eb-981e-ee7eea9fddf2)

# MeshCentral

MeshCentral is a free open source web-based remote computer management software. You
could setup your own management server on a local network or on the internet and remote
control and manage computers that runs either Windows* or Linux* OS.

## Installing NodeJS

The first prerequisite is to ensure NodeJS is installed on the system. We will install the node version manager, activate it, then install the LTS version of NodeJS.

```bash
sudo add-apt-repository universe
sudo apt update
sudo apt install nodejs -y
sudo apt install npm -y
```

##You can verify the versions of NodeJS and NPM just installed with the following commands:

```bash
node -v
npm -v
```

## Port Permissions

On Linux, as a security feature, ports below 1024 are reserved for processes running as “root” user. In our case, we need MeshCentral to listen/run on ports 80 and 443. To accomplish this, we first need to discover where NodeJS runs from:

```bash
whereis node
node: /usr/bin/node /usr/include/node /usr/share/man/man1/node.1.gz
```

In this case, the result shows NodeJS binaries are found at /usr/bin/node. We will this path in the next command, which will allow NodeJS to utilize ports below 1024. Note that these permissions may sometimes be lost when updating the Linux Kernel and the command may need to be run again. 1)

```bash
sudo setcap cap_net_bind_service=+ep /usr/bin/node
```

## Installing MeshCentral

We are finally ready to install MeshCentral! We use NPM to install the latest version of MeshCentral with the command below:

```diff
- !!DO NOT USE "SUDO" FOR THIS COMMAND!! -

npm install meshcentral
```

After the installation completes we can manually run MeshCentral for the first time:

```bash
node ./node_modules/meshcentral
```

## Automatically Starting the Server

Since Ubuntu supports systemd, we are going to use that to auto start MeshCentral in the background. First we need to know what our own username and group are. The simplest way to find this info is (from your home folder) run

```bash
ls -l
```
Doing so should give output similar to this example below:

```bash
drwxr-xr-x 2 user default 4096 Jul 20 00:03 Desktop
drwxr-xr-x 2 user default 4096 Jul 20 00:03 Documents
drwxr-xr-x 2 user default 4096 Jul 20 00:03 Download
...
```

Make note of the username and group. In the sample above, the username is user and the group is default.

We will also need to know the path where NodeJS binaries are at. to find this enter:

```bash
whereis node
```

Node is usually installed at /usr/bin/node but if your check above shows a different path, make note of it and enter it into the appropriate place in the file we are about to create.

We will need all of this information to create the description file for the MeshCentral service we create. To create this description file, enter:

```bash
sudo nano /etc/systemd/system/meshcentral.service
```

In this new file, enter the following lines:

```
[Unit]
Description=MeshCentral Server

[Service]
Type=simple
LimitNOFILE=1000000
ExecStart=/usr/bin/node /home/user/node_modules/meshcentral
WorkingDirectory=/home/user
Environment=NODE_ENV=production
User=user
Group=default
Restart=always
# Restart service after 10 seconds if node service crashes
RestartSec=10
# Set port permissions capability
AmbientCapabilities=cap_net_bind_service

[Install]
WantedBy=multi-user.target
```

Be sure you set the username and group values correctly for your specific installation.Notice that the ExecStart and WorkingDirectory lines include the path to the user's home folder. So make sure you have the correct username in there. Also be sure to double check the path to NodeJS in the ExecStart line.

Once we have this file created we can now enable, start, stop and disable MeshCentral:

```bash
sudo systemctl enable meshcentral.service
sudo systemctl start meshcentral.service
sudo systemctl stop meshcentral.service
sudo systemctl disable meshcentral.service
```

Run the first two commands to enable then start MeshCentral. Enabling the service will make MeshCentral start up automatically each time the computer restarts.

Once MeshCentral is started, you can access it via web browser just as we did earlier. You should now refer to the MeshCentral User's Guide or this wiki's configuration guides for information about on how to further configure and use MeshCentral.