---
title: "Getting data from old Ecobee thermostat"
description: ""
excerpt: ""
date: 2019-02-24T00:39:58-05:00
lastmod: 2019-02-24T00:39:58-05:00
draft: false
weight: 50
images: [ecobee_data.png]
categories: [Home Automation]
tags: [Home Automation]
contributors: []
pinned: false
homepage: false
---

I was recently migrating from Ecobee 3 to Ecobee 4. The installation itself was smooth (albeit I had to change both the furnace C-wire kit and the thermostat base, as they are not compatible between Ecobee 3 and 4). However, when I finished installation and added the new thermostat with to my account, Ecobee 3 data was not accessible any longer). The easiest thing to do, is to downloaded all your data just before you replace the thermostat. But sadly, I forgot to do that. 

When I logged in through the web browser my Ecobee3 data was not there any more. I spoke to an Ecobee employee and he was very helpful. All that i needed was a 24V DC power supply. This is how you do it: Connect the power supply to Rc and C terminals. Slap the thermostat to the backplate. Wait for a few minutes and your thermostat should be online. It took a while before it appeared on the Ecobee web portal. Once it is available the data can be downloaded. 

It is frustrating that **Ecobee ties the data to the individual thermostat unit rather than the user account**. If it were tied to my account, then upgrading should not cause any issue with old data. Hope Ecobee considers that. 

Also, remember that **you have access to download only the last 12 months of data**. So, it is is a good idea to periodically download all your data.