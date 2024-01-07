---
title: "Passing USB to guest OS in Proxmox Virtual Environment"
description: ""
excerpt: ""
date: 2018-08-28T13:27:22-04:00
lastmod: 2018-08-28T13:27:22-04:00
draft: false
weight: 50
images: [usb_list.png]
categories: [Linux]
tags: [Linux, Proxmox]
contributors: []
pinned: false
homepage: false
---
My home automation hub <a href="https://www.home-assistant.io/hassio/" target="_blank">hassio</a> is running in Ubuntu Bionic hosted as guest by <a href="https://www.proxmox.com/en/" target="_blank">Proxmox Virtual Environment</a>. I recently purchased a Linear <a href="https://www.amazon.com/GoControl-CECOMINOD016164-Linear-HUSBZB-1/dp/B01GJ826F8" target="_blank">HUSBZB-1</a> combined Zigbee and Z-wave controller stick. I need to make this available to hassio. Here is how it is done;

Running _lsusb_ command in the PVE host lists all the USB devices connected;

The HUSBZB-1 is listed as 

```
001 Device 008: ID 10c4:8a2a Cygnal Integrated Products, Inc.
```

To get full details of the USB devices, running usb-devices command provides a long list. Of that these are the lines pertaining to the zigbee/Z-wave stick;

```
root@pve:~# usb-devices
T:  Bus=01 Lev=01 Prnt=01 Port=00 Cnt=01 Dev#=  8 Spd=12  MxCh= 0
D:  Ver= 2.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS=64 #Cfgs=  1
P:  Vendor=10c4 ProdID=8a2a Rev=01.00
S:  Manufacturer=Silicon Labs
S:  Product=HubZ Smart Home Controller
S:  SerialNumber=612009D0
C:  #Ifs= 2 Cfg#= 1 Atr=80 MxPwr=100mA
I:  If#= 0 Alt= 0 #EPs= 2 Cls=ff(vend.) Sub=00 Prot=00 Driver=cp210x
I:  If#= 1 Alt= 0 #EPs= 2 Cls=ff(vend.) Sub=00 Prot=00 Driver=cp210x
```

```
root@pve:~# lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 05ac:8242 Apple, Inc. Built-in IR Receiver
Bus 001 Device 007: ID 05ac:8289 Apple, Inc. 
Bus 001 Device 003: ID 0a5c:4500 Broadcom Corp. BCM2046B1 USB 2.0 Hub (part of BCM2046 Bluetooth)
Bus 001 Device 002: ID 125f:c08a A-DATA Technology Co., Ltd. C008 Flash Drive
Bus 001 Device 008: ID 10c4:8a2a Cygnal Integrated Products, Inc. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

There are two serial ports running, using the driver cp201x. Now, ssh into the guest OS and verify the running USB hosts;

```
venkat@homehub:~$ lsusb
Bus 001 Device 002: ID 0627:0001 Adomax Technology Co., Ltd 
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
```

Running the following command;

```
qm set 101 -usb2 host=10c4:8a2a
```

allows the host OS to access the USB device. Now, listing the usb devices using _lsusb_ shows newly added device.

```
venkat@homehub:~$ lsusb
Bus 001 Device 002: ID 0627:0001 Adomax Technology Co., Ltd 
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hubBus 003 Device 002: ID 10c4:8a2a Cygnal Integrated Products, Inc.
```

I was then able to install my Leviton Z-Wave dimmers and a whole lot of Zigbee devices in my Home Assistant. 

This method works for USB 1 and USB 2 devices.  Accessing USB 3 devices is slightly different.  For full details about the whole process, including accessing USB 3, <a href="https://pve.proxmox.com/wiki/USB_Devices_in_Virtual_Machines#USB3.0_2" target="_blank">see this page. </a>

**Note;** This method of accessing USB is not restricted to a single type of device. You can access USB data keys, external hard disks, printers, etc. using the qm set command.