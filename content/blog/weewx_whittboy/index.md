---
title: "Integrating Ecowitt Whittboy with WeeWx"
description: "Full Instructions for integrating Wittboy and WeeWx"
summary: "This post summarizes steps inovled in integrating Ecowitt 7-in-1 Solar-powered weather station with WeeWx for full weather monitoring"
date: 2024-03-03T19:11:44-05:00
lastmod: 2024-03-03T19:11:44-05:00
draft: false
weight: 50
categories: ["Home Automation"]
tags: ["home-automation", "weewx", "ecowitt"]
contributors: [V. Venkataramanan]
pinned: false
homepage: false
seo:
  title: "" # custom title (optional)
  description: "Full Instructions for integrating Wittboy and WeeWx" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

## Ecowitt Wittboy 

[Ecowitt GW2001 Wittboy Weather Station](https://shop.ecowitt.com/en-ca/products/wittboy) is a Wi-Fi Hub with 7-in-1 Outdoor Solar Powered Anti-vibration Haptic Rainfall Sensor.  Its features include,

* Sensor:Piezoelectric rain gauge;
* Ultrasonic anemometer（start wind speed 0.3m/s);
* Temperature;Humidity;Solar light intensity and UV index;
* Waterproof IPX5;

It comes with an indoor hub that coordinates the outdoor sensors and acts WLAN or LAN Wi-Fi gateway.  It also includes a Barometric Pressure, Temperature, and Humidity sensors for indoor measurements. 

## WeeWx

[WeeWx](https://weewx.com/) is an open source weather station program that collects data from weather stations and produces graphs, reports and html pages. 

## Wittboy Installation

Usual method in an isolated LAN.   Once successfully installed the web page for Wittboy can be accessed at its ip address from the local network. 

We need to configure it to send data to WeeWx.  To do this go to _Weather Services_ from the sidebar. Go all the way down to the _Customized_ section.  Do the following settings

```
Customized = Enabled
Protocol Type = Ecowitt
Server IP/Hostname = (same as the Whitboy ip address)
Path = /data/report/
Port = 2324
Upload Interval = 60 Sec
```

Save this settings. 

### Virtual Server

A new Debian 12 virtual server was installed under the TrueNAS Core.  Run the usual _apt update_ to complete installation. 

## Weewx Installation

The most current version of WeeWx is 5.0.  There are several changes from version 4.x, most notably in the Utilities Commands. 

This is a guide to installing WeeWX from a DEB package on systems based on Debian, including Ubuntu, Mint, and Raspberry Pi OS.

### Configure `apt`

The first time you install WeeWX, you must configure `apt` so that it will trust weewx.com, and know where to find the WeeWX releases.

Trust weewx.com.

```
sudo apt install -y wget gnupg
wget -qO - https://weewx.com/keys.html | \
    sudo gpg --dearmor --output /etc/apt/trusted.gpg.d/weewx.gpg
```

Tell `apt` where to find the WeeWX repository.

```
echo "deb [arch=all] https://weewx.com/apt/python3 buster main" | \
    sudo tee /etc/apt/sources.list.d/weewx.list
```

### Installation

Use `apt` to install WeeWX. The installer will prompt for a location, latitude/longitude, altitude, station type, and parameters specific to your station hardware. When you are done, WeeWX will be running in the background.

```
sudo apt update
sudo apt install weewx
```

After about 5 minutes (the exact length of time depends on your archive interval), copy the following and paste into a web browser. You should see your station information and data.

```
/var/www/html/weewx/index.html
```

If things are not working as you think they should, check the status:

```
sudo systemctl status weewx
```

and check the system log:

```
sudo journalctl -u weewx
```

{{< callout note >}} To restart WeeWx use
```
sudo systemctl restart weewx
```
{{< /callout >}}


At this point WeeWx is running in the simulator mode.   

## Install Nginx

Use _sudo apt install ngnix_ to install a web server.  This installs with document root at _var/www/html_

The WeeWx simulator web page can now be accessed at 

```
http://server_ip/weewx/index.html
```

### Move Webroot 

{{< details "Click here to expand" >}}

On a fresh installation of Nginx, the document root is located at _/var/www/html_

You can search for the location of additional document roots using grep. We’ll search in the _/etc/nginx/sites-enabled_ directory to limit our focus to active sites. The -R flag ensures that grep will print both the line with the root directive and the filename in its output:

```
grep "root" -R /etc/nginx/sites-enabled
```

In Debian, we get the following output:

```
venkat@weather:~$ grep -R "root" /etc/nginx/sites-enabled
/etc/nginx/sites-enabled/default:	root /var/www/html;
/etc/nginx/sites-enabled/default:	# deny access to .htaccess files, if Apache's document root
/etc/nginx/sites-enabled/default:#	root /var/www/example.com;
```

Now, edit _/etc/nginx/sites-enabled/default_ and change, document root from _/var/www/html_ to _var/www/weewx_  (assuming that weewx is the new document root needed). 

Once you’ve finished the configuration changes, you can make sure the syntax is correct with this command:

```
sudo nginx -t

```
If everything is in order, it should return:

```
Outputnginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

```

If the test fails, track down and fix the problems.

Once the test passes, restart Nginx:

```
sudo systemctl restart nginx

```

When the server has restarted, visit your affected sites and ensure they’re working as expected. Once you’re comfortable everything is in order, don’t forget to remove the original copy of the data.

The Weather Station is now accessible at 

```
http://server_ip/index.html
```
{{< /details >}}

## Install Ecowitt Driver for WeeWx

This follows the [GW100 driver](https://github.com/gjr80/weewx-gw1000) 

Make sure that the WeeWx is successfully installed and using simulator mode and the web page is accessible. 

Install the latest version of the Ecowitt Gateway driver using the _weectl_ utility. (This is new in WeeWx 5.x)

```
weectl extension install https://github.com/gjr80/weewx-gw1000/releases/latest/download/gw1000.zip

```

Test the Ecowitt Gateway driver by running the driver file directly using the _--test-driver_ command line option.

```
PYTHONPATH=/usr/share/weewx python3 /etc/weewx/bin/user/gw1000.py --test-driver --ip-address=192.168.x.x
```

You should observe loop packets being emitted on a regular basis. Once finished press ctrl-c to exit.

Now configure  WeeWx to use the GW1000 driver.

For WeeWX package installs use:

```
weectl station reconfigure --driver=user.gw1000
```

This will write the weewx.conf file with the new driver information. 

```
[GW1000]
    # This section is for the Ecowitt Gateway driver.
    # How often to poll the API, default is every 20 seconds:
    poll_interval = 20
    # The driver to use:
    driver = user.gw1000
    ip_address = 192.168.20.227
    port = 45000
```

Finally, restart WeeWx 

```
sudo systemctl restart weewx
```

## Using weewx-wdc Skin

Follow the instructions at [weewx-wdc](https://github.com/Daveiano/weewx-wdc)

{{< picture src="weatherstation.webp" alt="Screenshot of the Weather Station" >}}

## Forecasting - OpenWeather  (not working)

{{< callout context="danger" title="Caution" icon="alert-triangle" >}} This is still not working.  

There seems to be some issue with this extension and the new WeeWx 5.x. {{< /callout >}}

Obtain API Key from [OpenWeather](https://openweathermap.org/)

Install WeeWx Forecast Extension 

```
root@weather:/etc/nginx/sites-enabled# weectl extension install weewx-forecast-3.4.0b12.zip
Using configuration file /etc/weewx/weewx.conf
Install extension 'weewx-forecast-3.4.0b12.zip' (y/n)? y
Traceback (most recent call last):
  File "/usr/share/weewx/weectl.py", line 74, in <module>
    main()
  File "/usr/share/weewx/weectl.py", line 66, in main
    namespace.func(namespace)
  File "/usr/share/weewx/weectllib/__init__.py", line 121, in dispatch
    namespace.action_func(config_dict, namespace)
  File "/usr/share/weewx/weectllib/extension_cmd.py", line 116, in install_extension
    ext.install_extension(namespace.source, no_confirm=namespace.yes)
  File "/usr/share/weewx/weecfg/extension.py", line 143, in install_extension
    raise InstallError(f"Unrecognized type for {extension_path}")
weecfg.extension.InstallError: Unrecognized type for weewx-forecast-3.4.0b12.zip
```
## Todo

1. Configure MQTT 
2. Embed weather station in Home Assistant
3. Complete Weather Forecasting. 


