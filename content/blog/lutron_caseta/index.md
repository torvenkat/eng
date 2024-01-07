---
title: "Adding Lutron Caseta to Home Assistant"
description: ""
excerpt: ""
date: 2018-08-28T04:17:26-04:00
lastmod: 2018-08-28T04:17:26-04:00
draft: false
weight: 50
images: [lutron_caseta.jpg]
categories: [Home Automation]
tags: [Home Assistant]
contributors: []
pinned: false
homepage: false
---
Adding Lutron Caseta Bridge&nbsp; Home Assistant&nbsp; is a bit complicated.&nbsp; The <a href="https://www.home-assistant.io/components/lutron_caseta/" target="_blank" rel="noopener">Component page</a> gives a link to the <a href="https://www.home-assistant.io/assets/get_lutron_cert.zip" target="_blank" rel="noopener">python script</a> to generate the necessary files and directs to follow the instructions at the top of the script.&nbsp; But the instructions in the script are not easy for newbies to follow.&nbsp; Here is what I did to get it done.&nbsp; These are for mac, but should be easy to follow in other OS as well.&nbsp; This assumes that python3 is installed.

  1. Copy the python script to a new directory, something like __~/Desktop/Caseta__
  2. Open a terminal and change to that directory
  3. run __python -m venv env__
  4. run __pip install cryptography==2.1.3 requests==2.18.4__
  5. run __python get_lutron_cert.py__
  6. It’ll ask you to go to the URL stated. Something like &#8221;
      Open Browser and login at https://device-login.lutron.com/oauth/authorize?client_id=&#8230;&#8230;&nbsp;20878c28e5a&redirect_uri=https%3A%2F%2Fdevice-login.lutron.com%2Flutron_app_oauth_redirect&response_type=code&#8221;
  7. Login to your Lutron account
  8. The browser will generate an error.&nbsp; Do not move close the tab. Copy the URL on the error page just generated.
  9. Paste the URL into the Command Prompt. &#8221; 
      __Enter the URL (of the &#8220;error&#8221; page you got redirected to (or the code in the URL):__
 10. __Type in your Lutron Bridge’s local IP address, at&nbsp;__ Enter the address of your Caseta bridge device:&nbsp;(This should be something like &#8216;192.168.1.xx&#8217;)
 11. If everything has gone perfect, it’ll give you a successfully connected to LEAP statement.&nbsp; I got an error statement:&nbsp; (but it did not matter)  
    `Traceback (most recent call last)
File "get_lutron_cert.py", line 156, in <module>
leap_response['Body']['PingResponse']['LEAPVersion'])
KeyError: 'Body'`
 12. __This will result in three files in your subdirectory. Copy all three&nbsp; to your <config> folder on your HA installation.&nbsp;__
 13. When setting up Home Assistant, use the following configuration in your configuration.yaml file:  
    `lutron_caseta:<br />
host: <your local ip address><br />
keyfile: caseta.key<br />
certfile: caseta.crt<br />
ca_certs: caseta-bridge.crt` 

Restart your Home Assistant and you will see the Lutron dimmers added to your system.

It is a good idea to reserve the local ip that was used to generate the keys in your router.&nbsp; I generally reserve all my device ip once they work successfully in Home Assistant.

I referred to several fragmented sources to get the full picture of this integration. Particularly, I am thankful to the following:

<a href="https://www.home-assistant.io/blog/2016/02/09/Smarter-Smart-Things-with-MQTT-and-Home-Assistant/" target="_blank" rel="noopener">Smarter SmartThings with MQTT and Home Assistant</a>

<a href="https://community.home-assistant.io/t/smartthings-mqtt-bridge/269" target="_blank" rel="noopener">Smartthings MQTT Bridge</a>

<a href="https://community.home-assistant.io/t/anyone-integrated-smartthings-into-hassio-yet/25324/7" target="_blank" rel="noopener">https://community.home-assistant.io/t/anyone-integrated-smartthings-into-hassio-yet/25324/7</a>