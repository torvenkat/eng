---
title: "Installing Hassio in Ubuntu Bionic using Docker"
description: ""
excerpt: ""
date: 2018-06-17T18:57:22-04:00
lastmod: 2021-10-20T20:09:22-05:00
draft: false
weight: 50
images: [hassio_docker.jpg]
categories: [Home Automation]
tags: [Home Automation, Linux]
contributors: []
pinned: false
homepage: false
---
As always, begin with updating the package information.

`sudo apt-get update`

Then instal the dependencies

`sudo apt-get install jq curl dbus socat bash avahi-daemon`

These instructions are specifically for installing the test version of docker-ce on Ubuntu 18.04 (bionic)

`sudo apt install apt-transport-https ca-certificates curl software-properties-common<br />
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`

You will get a OK return

Add the apt repository for Docker

`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic test"<br />
sudo apt update`

Now, install Docker-ce

`sudo apt install docker-ce`

Check the version of Docker installed

`docker --version`  
Docker version 18.05.0-ce, build f150324

When I treid installing hassio (as described here: <a href="https://github.com/home-assistant/hassio-build/tree/master/install#install-hassio" target="_blank" rel="noopener">https://github.com/home-assistant/hassio-build/tree/master/install#install-hassio</a>), I got the following error:

`sudo curl -sL https://raw.githubusercontent.com/home-assistant/hassio-build/master/install/hassio_install | bash -s`

mkdir: cannot create directory ‘/usr/share/hassio’: Permission denied

I decided to download the bash script and execute it locally.

`wget https://raw.githubusercontent.com/home-assistant/hassio-build/master/install/hassio_install`

give it executable permission

`chmod +x ./hassio_install`

Run the scripts

`sudo ./hassio_install`

This installed hassio. Check the installation at

http://<localhost>:8123

The browser loads hassio and completes the installation. This takes a few minutes to complete. From here one should be able to configure and use Home Assistant.