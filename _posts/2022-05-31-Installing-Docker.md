---
title: Installing Docker on Linux
date: 2022-05-31 18:55:00 -500
categories: [guides, docker, linux]
tags: [servers,guides,homelab,docker]  # Tag names should always be lowercase
published: true
---

![Docker](https://www.docker.com/wp-content/uploads/2022/03/horizontal-logo-monochromatic-white.png)

## Install using the repository
Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

### Set up the repository:

1 - Update the ''apt'' package index and install packages to allow ''apt'' to use a repository over HTTPS:

```bash
sudo apt-get update 
sudo apt-get install ca-certificates curl gnupg lsb-release
```
2 - Add Docker’s official GPG key:

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

3 - Use the following command to set up the repository:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker Engine:
Update the ''apt'' package index, and install the //latest version// of Docker Engine, containerd, and Docker Compose, or go to the next step to install a specific version:

```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Confirm your docker installation was sucessfull by running 

```bash 
sudo systemctl status docker
```

The output should show "active"
![](https://www.howtogeek.com/wp-content/uploads/csit/2021/08/e1e87514.png?trim=1,1&bg-color=000&pad=1,1)