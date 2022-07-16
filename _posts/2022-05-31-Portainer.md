---
title: Installing Portainer Using Docker
date: 2022-05-31 18:55:00 -500
categories: [guides, docker]
tags: [servers,guides,homelab,docker,portainer]  # Tag names should always be lowercase
published: true
---

![Portainer](https://www.seekpng.com/png/full/717-7171842_portainer-logo.png)

1 - Create the volume that Portainer Server will use to store its database:

```bash
docker volume create portainer_data
```

2 - Download and install the Portainer Server container:

```bash
sudo docker run -d \
    -p 8000:8000 \
    -p 9443:9443 \
    --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```

## Logging In:

Now that the installation is complete, you can log into your Portainer Server instance by opening a web browser and going to:

```html
https://localhost:9443
```

Replace ''localhost'' with the relevant IP address or FQDN if needed, and adjust the port if you changed it earlier.

You will be presented with the initial setup page for Portainer Server.

# Upgrading Portainer

To upgrade Portainer we need to stop and remove the current Portainer instance.

```bash
sudo docker stop portainer
```
```bash
sudo docker rm portainer
```

Now we need to pull the latest image again, otherwise docker will just use the existing image named "latest"

```bash
docker pull portainer/portainer-ce:latest
```

Now launch the container with docker run in the terminal:

```bash
docker run -d \
    -p 8000:8000 \
    -p 9443:9443 \
    --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```
