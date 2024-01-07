---
title: "Solving too big and unresponsive Home Assistant Database Problem"
description: ""
excerpt: ""
date: 2021-06-05T21:33:33-04:00
draft: false
weight: 50
images: []
categories: [Home Automation]
tags: [Home Assistant]
contributors: []
pinned: false
homepage: false
---

## Database problems

If all records are kept, soon the database can grow too large and stifle the system. My database grew to 240 GB and the system was too slow.  Here is the way to get out of the situation and keep sanity. 

## Delete database

If database gets too big, yes, it’s safe to delete *home-assistant_v2.db* and after that restart Hass. Deleting it fixes a multitude of problems with the downside only that you lose your history. Its a good idea to stop HA before deleting the database. Home Assistant will create a new database on start.

HA cannot restore the last states with a new database, so check that.

## Automatic purge

Configuration options on Recorder

``` bash 
recorder:
  purge_interval: 1
  purge_keep_days: 28
``` 

Automatic purge function of the db sometimes takes 24 hours to run. So if HA is restarted anytime within that 24 hours, it restarts the 24 hours timer.

You can also call a service* *recorder.purge* with *repack* set to true, with this payload:

```yaml
{“keep_days”:“2”, “repack”:“true”}
```


Maybe the best way is to create an automation like this one:

``` yaml
- alias: Database Purge
  trigger:
    platform: time
    at: '12:00:00'
  action:
    - service: recorder.purge
      data:
        keep_days: 10
        repack: true
```

The key is the repack option being set to true, otherwise, file size won’t be reduced.

## Moving the database

It is possible to use an external MySQL instance. But, I ended up setting the local MariaDB with add-on as it was trivial.

It is also possible to move to another SQLite file on network drive.