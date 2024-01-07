---
title: "Programming Honeywell Vista 15P"
description: ""
excerpt: ""
date: 2022-08-09T14:45:45-04:00
draft: false
weight: 50
images: []
categories: [Home Automation]
tags: [Home Assistant]
contributors: []
pinned: false
homepage: false
---
I previously got a monitored alarm system installed at my home.  This is a Honeywell Vista 15P panel and Honeywell K 4392 M7240 Rev E key panel combination.   This system includes several motion sensors, door and window contact sensors, and alarm siren.  They all work fine, but I wanted to integrate this system into Home Assistant so that I can remotely monitor it in my cell phone.  I purchased an Envisalink Eyezon 4 board to do that myself.  More about that integration in another note, but before that I had to gain full access to the Honeywell panel.  The previous company did not give me the installer access or any manual, I spent a couple of hours searching and eventually stumbled upon the procedure needed to get access.  Since this may be useful to someone else, here are the procedures. 

## To delete FC (communication failure) error

`[4digit installer code] + *41* + *42* + *54 + #15 + *55 + 1 + 99`

## Programming the panel

### Access system programming. 

Enter in `[Installer Code] + [800]` to access system programming.  The number "20" will be displayed if you are using a fixed English keypad. 

### Clear the phone number. 

Enter in `[*41*]`. You will hear three beeps. Then enter in `[*42*]`. You will hear another three beeps. This will remove all phone numbers that the panel used to dial out.

### Program dynamic signaling. 

Enter in `[*54] + [#15] + [*55] +[1]`. This will adjust the dynamic signaling settings so that the panel knows not to attempt to use its built-in dialer.

### Exit programming. 

Press `[*99]` to exit programming and save your changes.

[Read more](https://www.alarmgrid.com/faq/how-do-i-clear-the-fc-code-on-my-honeywell-alarm)

## Reset the Master User Code

The codes for Installer (User 01) and Master (User 02) are built-in. In our system these are already changed for safety and are available in password manager. If the master code needs to be changed again, use

```[4 digit installer code] + 8 + 02 + [new 4 digit master code]```

8 gets to the code reset mode, 02 specifies the user (here 02 is the master user). The same sequence can be followed to change the user codes as well. However, if the user is already programmed, it should be emptied first. So, to change the user [06] code;
```
[4 digit master code] + 8 + 06 + #0                           : blank 06's code 
[4 digit master code] + 8 + 06 + [new 4 digit user code]      : add new user code
```

Reset Error Codes Afeter New Battery Installation

The error message on keypad will persist even after new batteries are installed to get rid of that, try disabling alarm (i.e. as if your are entering the home and entering your code to disable alarm)
```
[4 digit user code] + 1 
```
If it does not work immediately, try it once more. It works.

### Enable/Disable Chime
Enabling chime is useful to find the door and window contacts. To enable or disable chime

```
[4 digit user code] + 9
```
