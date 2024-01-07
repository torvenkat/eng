---
title: "Host"
description: ""
lead: ""
date: 2023-08-18T22:15:15-04:00
lastmod: 2023-08-18T22:15:15-04:00
draft: false
images: []
menu:
  docs:
    parent: ""
    identifier: "host-8671cbb274889d327a0b1372db796eeb"
weight: 109
toc: true
---

My installation runs on a [Home Assistant Blue](https://www.home-assistant.io/blue/) device.  Here are the core specs:

* __Processor__ - 6-Core Amlogic S922X Processor (ARMv8-A), Quad-core Cortex-A73 @ 2.2Ghz
* __Memory__ - 4GB DDR4
* __Storage__ - 128GB eMMC Flash included

I keep regularly updating it.  The current versions are 

* __Frontend__: 20230802.0 
* __Operating System__ : Version 10.4


### Previous

I repurposed an old Mac Mini (*circa 2014*). 

* Dual-core Intel i5 (Haswell ULT), at 2.7 GHz
* 4 GB RAM
* 1 TB SSD (Samsung SSD 860 QVO)

It runs [Proxmox VE](https://www.proxmox.com/en/proxmox-ve), an open-source Virtualization Platform, on a skeletal Debian.  The Home Assistant runs in a container, with no restrictions on CPU, Memory, or disk space utilization. Along with this I run [WeeWx weather server](http://www.weewx.com/)  on  another. 