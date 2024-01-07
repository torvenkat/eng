---
title: "Tesla Plugged State"
description: ""
lead: ""
date: 2023-08-17T14:19:39-04:00
lastmod: 2023-08-17T14:19:39-04:00
draft: false
images: []
menu:
  docs:
    parent: ""
    identifier: "tesla_plugged-be9e53242278dbefbfaa59689cefab6a"
weight: 600
toc: true
---

{{< callout context="note" title="Note" icon="info-circle" >}}
This scripts sents a notification to phones if Tesla is not plugged in by 7pm and ready for overnight charging. <br> It will only notifiy if the car is in the garage, verifying the geolocation
{{< /callout >}}

For Tesla integration [see here](../../configuration/tesla/)

```yaml
alias: Notify if Tesla is not plugged in at night
description: Notify if Tesla is not plugged in at night
trigger:
  - platform: time
    at: "19:30:00"
condition:
  - condition: and
    conditions:
      - condition: state
        entity_id: binary_sensor.tesla_plugged_in
        state: "off"
      - condition: state
        entity_id: sensor.tesla_geofence
        state: Home
        enabled: false
action:
  - service: notify.notify
    data:
      message: >-
        Tesla is not plugged in for charging. May not charge overnight!. You may
        want to plug it in.
mode: single
```