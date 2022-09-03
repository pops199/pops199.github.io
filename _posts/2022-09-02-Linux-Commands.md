---
title: Usefull Linux Commands
date: 2022-09-02 18:55:00 -500
categories: [guides, linux]
tags: [servers,guides,homelab]  # Tag names should always be lowercase
published: true
---

## Update Your System

To update the repositories run the following command in the terminal:

#### Debian / Ubuntu
```bash
sudo apt update 
#If you are not logged in as the root user, make sure to use "sudo"
```

#### Fedora
```bash
sudo dnf update 
#If you are not logged in as the root user, make sure to use "sudo"
```

To install the available updates to the

#### Debian / Ubuntu
```bash
sudo apt upgrade 
#If you are not logged in as the root user, make sure to use "sudo"
```

#### Fedora
```bash
sudo dnf upgrade 
#If you are not logged in as the root user, make sure to use "sudo"
```

## Copying Files

If you are on the computer from which you want to send file to a remote computer:

```bash
scp /file/to/send username@remote:/where/to/put
```
Here the `remote` can be a FQDN(hostname) or an IP address.


On the other hand if you are on the computer wanting to receive file from a remote computer:

```bash
scp username@remote:/file/to/send /where/to/put
```
scp can also send files between two remote hosts:

```bash
scp username@remote_1:/file/to/send username@remote_2:/where/to/put
```