---
title: Installing Speedtest Tracker using docker
date: 2022-06-12 14:55:00 -500
categories: [guides, docker]
tags: [servers,guides,docker,speedtest]  # Tag names should always be lowercase
published: true
---
![Speedtest-Tracker](https://blog.thelazyfox.xyz/content/images/2021/11/publication-cover-speedtest-tracker-1.png)
To install speedtest tracker you need to create the following folder on the host machine:

```bash
mkdir -p /home/user/docker/speedtest-tracker/config
# user will be your username on the host machine.
```

Once the directory is created, just run the following docker command:
```bash
sudo docker run -d \
      --name=speedtest \
      -p 8765:80 \
      -v /home/user/docker/speedtest-tracker/config:/config \
      -e OOKLA_EULA_GDPR=true \
      --restart unless-stopped \
      henrywhitaker3/speedtest-tracker:dev-arm
# Remember to change `user` to your username.
```
This will use OOKLA speedtest.net to determine the internet speed, servers can be changed and also updated vir the UI, once deployed.
