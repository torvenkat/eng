---
title: "Integrating Home Assistant and SmartThings with MQTT"
description: ""
excerpt: ""
date: 2018-06-10T13:28:55-04:00
lastmod: 2018-06-10T13:28:55-04:00
draft: false
weight: 50
images: [hassio_ST.png]
categories: [Home Automation]
tags: [Home Automation, Smartthings]
contributors: []
pinned: false
homepage: false
---
I have been using Samsung SmartThings (ST) as my home automation hub for more than 2 years now. The availability of WebCORE automation tools is very useful to combine sensors and actuators, however it is very limited. Also SmartThings is a cloud-based platform which means that when there is a network outage, my entire home automation system will grid to a halt and overall the automations will run slow. I was looking for open source alternatives and initially considered OpenHab, but finally settled to <a href="https://www.home-assistant.io/components/lock.mqtt/" target="_blank" rel="noopener">Home Assistant</a> (and I am glad I did). My home automation hub now runs on a Raspberry Pi B+ using the docker based <a href="https://www.home-assistant.io/hassio/" target="_blank" rel="noopener">Haas.io</a> platform. HA has by far the maximum number of device integrations.

Adding other hub-based systems like Philips Hue bulbs, or WiFi-based systems like TP-Link plugs or MyQ garage door controls was very easy. Lutron Caseta Dimmers required a little bit of work (you can read it here). However, Zigbee and Z-Wave based systems needed additional hardware. I was initially considering abandoning the SmartThings totally and migrate entirely. Buying a USB Zigbee and Z-Wave dongle could cost anywhere between $60-$110 CAD, so I decided to integrate HA and ST using MQTT and use that only for devices that could not be natively connected. The process is a bit long and there I could not find a clear step-by-step guide available anywhere. So, here is one that combines multiple pieces of information scattered around in the web.

**This method is for those using a Raspberry Pi and Hassio**. If you are using Home Assistant by any other installation method, you may want to follow the guide here.

### Step 1: Installing the MQTT bridge and broker.

In the web interface, navigate to to `Hass.io > Store > Mosquitto broker add-on > Open` and install it.

You will be presented with the following configuration; do not change anything, leave it to default.

```
"plain": true
"ssl": false
"anonymous": true
"logins": []
"customize": 
"active": false,
"folder": "mosquitto"

"certfile": "fullchain.pem"
"keyfile": "privkey.pem"
```

The installation will default to port 1883. Do not change anything. Since you are most probably running the MQTT bridge and the SmartThings on the same (home) network, we do not bother about the login credentials and leave it open. However, later you can secure, if you feel like. For further information about the broker <a href="https://www.home-assistant.io/docs/mqtt/broker" target="_blank" rel="noopener">see this</a>.

### Step 2: Installing SmartThings Bridge Add-on

This add-on establishes communication between ST and HA. This is not the part of the standard Hassio store. We are going to use the script provided by <a href="https://github.com/vkorn/hassio-addons" target="_blank" rel="noopener">Vlad Korniev</a> which is based on smartthings-mqtt-bridge by St. John Johnson.

Navigate to Hass.io >Store icon

In the section ‘Add-on Repositories’, add the repository ‘<a href="https://github.com/vkorn/hassio-addons" target="_blank" rel="noopener">https://github.com/vkorn/hassio-addons</a>’ and save.

When you refresh the page, you will see a new section‘Vlad’s repository’ It will have a few things, click on SmartThingsBridge hass.io and install.

Now open the newly installed SmartThings Bridge. You will see the following default configurations;

`{<br />
"broker_host": "172.17.0.1",<br />
"broker_port": 8888,<br />
"preface": "smartthings",<br />
"state_suffix": "state",<br />
"command_suffix": "cmd",<br />
"login": "login",<br />
"password": "password",<br />
"bridge_port": 2080<br />
}`

This where I stumbled and spent a lot of time (after going through all steps described below) because my ST was communicating using MQTT, but HA was not able to listen. Remember in the previous step we left the MQTT broker running at port 1883, it is time to tell the SmartThins Bridge to listen to that port, so change to

`"broker_port": 1883,`

Leave everything else. If you change the Preface to something other than Smartthings you should remember to use that in your configurations.yaml file later.

### Step 3: Setting up Device Handler in ST

We need to do a few things on the SmartThings side to get the MQTT Bridge as a device running. I assume that you have developer account in SmartThings and you are logged in there using either SmartThings or Samsung account.

Go to the SmartThings Device IDE and Create New Device Handler.  
Choose From Code and paste in the MQTT Bridge Device Code. <a href="https://github.com/stjohnjohnson/smartthings-mqtt-bridge/blob/master/devicetypes/stj/mqtt-bridge.src/mqtt-bridge.groovy" target="_blank" rel="noopener">https://github.com/stjohnjohnson/smartthings-mqtt-bridge/blob/master/devicetypes/stj/mqtt-bridge.src/mqtt-bridge.groovy</a>  
Click Save, Publish, and then For Me.

### Step 4: Setting up the Device in ST

Still under the SmartThings IDE, Go My Devices and click New Device.  
Enter a name, and pick any random set of characters for the Device Network Id (this will automatically update later). Under the pull down menu for Type, scroll to the bottom of the list and find your newly created MQTT Bridge. Choose that. Fill in the other boxes however you like.

Go back to My Devices, and click on the MQTT Bridge you just created. This will bring up a page that allows you to edit your device’s Preferences. You need to tell the network information to listen to.

`MQTT Bridge IP Address:` This is the private IP address of your Raspberry Pi, something like <192.168.1.50>  
`MQTT Bridge Port:` <1883> (Remember this is the port your bridge is communicating at, as per Step 2)  
`MQTT Bridge MAC Address:` <Mac address> of your Raspberry pi. This is of the format xx:xx:xx:xx:xx

### Step 4: Setting up the Smart App in ST

Now that you have successfully set up the MQTT bridge as a device, you need to configure the Smart App in the IDE.

Click New SmartApp  
Choose From Code. Paste in the MQTT Bridge SmartApp code from here <a href="https://github.com/stjohnjohnson/smartthings-mqtt-bridge/blob/master/smartapps/stj/mqtt-bridge.src/mqtt-bridge.groovy" target="_blank" rel="noopener">https://github.com/stjohnjohnson/smartthings-mqtt-bridge/blob/master/smartapps/stj/mqtt-bridge.src/mqtt-bridge.groovy</a>  
Click Save.  
Click Publish and then For Me.

### Step 5: Setting up Smart App in the mobile phone

This is performed in your mobile phone. Open the SmartThings mobile app.

Under Automation Section, click on SmartApps Tab

Click on Add a SmartApp and go to the bottom of the list click on My Apps.

Click on the MQTT Bridge you just created through the previous steps.

Under Notify this Bridge select the MQTT Bridge and Save everything.

Choose all the inputs you want through the MQTT bridge. I left things like Philips Hue bulbs and Lutron Caseta dimmers that were natively configured in HA. I mostly opted for the Zigbee and Z-Wave devices

### Step 6: Configuring MQTT Components in HA

Now that a bi-way communication is established between HA and ST you need to add MQTT to the config.yaml file.

`mqtt:<br />
broker: localhost<br />
discovery: true<br />
discovery_prefix: smartthings`

If you experience any problem, you may specify the broker with the local IP address, something like broker: 192.168.1.50

### Step 7: Adding Components to your configuration

The final step is to add MQTT-delivered components to your config.yaml file. I found it easy to first add and test a couple Zigbee bulbs as you will be able to see them react to your comments instantaneously.

Look into your SmarthingsBridge log under Hassio table in HA. You will see a line item:

`info: Subscribing to smartthings/Aquara Temp/temperature/cmd, smartthings/XiaTemp/temperature/cmd, …`

These subscription tags your MQTT topics for configuration. I found it useful to copy this line and keep it in a temporary file for easy reference. Then go on an add items to your config.yaml such as:

`- platform: mqtt<br />
name: "Front Light Left"<br />
state_topic: "smartthings/Front Left Light/switch/state"<br />
command_topic: "smartthings/Front Left Light/switch/cmd"<br />
payload_off: "off"<br />
payload_on: "on"<br />
optimistic: false<br />
retain: true`

The command\_topic is the MQTT topic to publish commands to change the component’s state and the state\_topic is the MQTT topic subscribed to receive state updates.

Remember everything in yaml files is case-sensitive. If you ever run into issues, the first thing to be checked is the lower/upper case of entries.