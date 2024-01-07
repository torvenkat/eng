---
title: "Server"
description: ""
lead: ""
date: 2023-08-18T22:15:29-04:00
lastmod: 2023-08-18T22:15:29-04:00
draft: false
images: []
menu:
  docs:
    parent: ""
    identifier: "server-10bee08f5c5c18a564fcd5be01d384aa"
weight: 233
toc: true
---
## TrueNAS Scale
This is the main file/media server.  I monitor this through [this custom integration](https://github.com/tomaae/homeassistant-truenas), through [HACS](https://hacs.xyz/).  The integration is straightforward, generating an API token via TrueNAS web interface and including that in the configuration.  It provides a lot of data on CPU, Memory, Disks, ZFS pool, storage space used by all datasets, etc.  
## Open Media Vault
I run an OMV server as a secondary server.  This is monitored in Home Assistant via [this custom integration](https://github.com/tomaae/homeassistant-openmediavault), again through [HACS](https://hacs.xyz/).  I created a dedicated user in OMV for Home Assistant integration and included those credentials in the configuration process.  This provides sensors for CPU, Memory, and File System usage. 

## Previous
### Proxmox VE
I previously ran a Proxmox server with Home Assistant running as a virtual machine.  This was monitored through [Proxmox VE Custom Integration](https://github.com/dougiteixeira/proxmoxve)
### QNAP
I also have an old QNAP HS-251.  This was monitored in Home Assistant with the [native QNAP integration](https://www.home-assistant.io/components/sensor.qnap/)
### Other
At various times, I experimented with Raspberry Pi (for Pi-Hole and AdGuard). These were configured with their native Home Assistant Integrations and monitored. 