---
title: Installing Uptime Kuma using Docker
date: 2022-07-16 10:55:00 -500
categories: [docker]
tags: [servers,guides,homelab,docker,uptime_kuma]  # Tag names should always be lowercase
published: true
---

# Uptime Kuma

It is a self-hosted monitoring tool like "Uptime Robot".

<img src="https://uptime.kuma.pet/img/dark.jpg" width="700" alt="" />

## Features

* Monitoring uptime for HTTP(s) / TCP / HTTP(s) Keyword / Ping / DNS Record / Push / Steam Game Server.
* Fancy, Reactive, Fast UI/UX.
* Notifications via Telegram, Discord, Gotify, Slack, Pushover, Email (SMTP), and [90+ notification services, click here for the full list](https://github.com/louislam/uptime-kuma/tree/master/src/components/notifications).
* 20 second intervals.
* [Multi Languages](https://github.com/louislam/uptime-kuma/tree/master/src/languages)
* Multiple Status Pages
* Map Status Page to Domain
* Ping Chart
* Certificate Info
* Proxy Support
* 2FA available

##  How to Install:

### Docker

```bash
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

Please use a **local volume** only. Other types such as NFS are not supported.

Browse to http://localhost:3001 after starting.

### Non-Docker

Required Tools: 
- [Node.js](https://nodejs.org/en/download/) >= 14
- [Git](https://git-scm.com/downloads) 
- [pm2](https://pm2.keymetrics.io/) - For run in background

```bash
# Update your npm to the latest version
npm install npm -g

git clone https://github.com/louislam/uptime-kuma.git
cd uptime-kuma
npm run setup

# Option 1. Try it
node server/server.js

# (Recommended) Option 2. Run in background using PM2
# Install PM2 if you don't have it: 
npm install pm2 -g && pm2 install pm2-logrotate

# Start Server
pm2 start server/server.js --name uptime-kuma
```
Browse to http://localhost:3001 after starting.

More useful PM2 Commands

```bash
# If you want to see the current console output
pm2 monit

# If you want to add it to startup
pm2 save && pm2 startup
```


## 🖼 More Screenshots

Light Mode:

<img src="https://uptime.kuma.pet/img/light.jpg" width="512" alt="" />

Status Page:

<img src="https://user-images.githubusercontent.com/1336778/134628766-a3fe0981-0926-4285-ab46-891a21c3e4cb.png" width="512" alt="" />

Settings Page:

<img src="https://louislam.net/uptimekuma/2.jpg" width="400" alt="" />

Telegram Notification Sample:

<img src="https://louislam.net/uptimekuma/3.jpg" width="400" alt="" />

