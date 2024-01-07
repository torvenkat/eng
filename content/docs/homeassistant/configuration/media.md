---
title: "Media"
description: ""
lead: ""
date: 2023-01-27T08:10:57-05:00
lastmod: 2023-01-27T08:10:57-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "media-dfa459140deff62c2933bfd1fd0e2a93"
weight: 179
toc: true
---


| Device                                                       | Quantity | Connection | Integration                                                  | Notes         |
| ------------------------------------------------------------ | :------: | ---------- | ------------------------------------------------------------ | ------------- |
| [Spotify](https://www.spotify.com/) | 1 | Cloud | [spotify](https://www.home-assistant.io/integrations/spotify/) |
| [Plex Media Server](https://plex.tv)                         |    1     | Ethernet   | [Plex](https://www.home-assistant.io/components/media_player.plex) / [Plex Activity Monitor](https://www.home-assistant.io/components/sensor.plex/) | (1) See below |
| [Pi Music Box](https://www.pimusicbox.com/)                  |    1     | Ethernet   | [mpd](https://www.home-assistant.io/integrations/mpd/)       | (2) See below |
| [Amazon Echo v1](https://www.amazon.com/Amazon-Echo-Bluetooth-Speaker-with-Alexa-Black/dp/B00X4WHP5E) |    1     | Wi-Fi      | [Alexa Media Player](https://github.com/custom-components/alexa_media_player) | (3) See below |
| [Amazon Echo Dot](https://www.amazon.com/Amazon-Echo-Dot-Portable-Bluetooth-Speaker-with-Alexa-White/dp/B015TJD0Y4) |    1     | Wi-Fi      | [Alexa Media Player](https://github.com/custom-components/alexa_media_player) | (3) See below |
| [Alexa in Ecobee4](https://www.ecobee.com/en-ca/smart-thermostats/smart-wifi-thermostat-with-voice-control/) |    1     | Wi-Fi      | [Alexa Media Player](https://github.com/custom-components/alexa_media_player) | (4) See below |
|                                                              |          |            |                                                              |               |

(1) Plex server runs in a Raspberry Pi 4, primarily configured as an [Openmediavault](https://www.openmediavault.org/) server, with external USB hard drives. 

(2) The Pi Music Box is a Raspberry Pi 3B+.  It scans and picks up audio files from the same Openmediavault server that runs Plex and provides additional music streaming through the home theatre speakers. 

(3) Amazon echo devices configured via Nabu Casa (See Voice Assistants Section) do not function as media players.  This necessitates using a custom integration [Alexa Media Player](https://github.com/custom-components/alexa_media_player).  I had purchased my first Amazon Echo when it was introduced in the USA (not available in Canada, then) so, it got integrated to my Amazon USA account and I had great difficulty in passing the verification step (which simply kept blanking out, instead of sending OTP to my phone).  I enabled Two-Factor Authentication (TFA) for my Amazon account and this helped me generate OTP locally using my Authenticator app and complete the process. 

(4) Ecobee4 has a built-in Alexa voice assistant which doubles (triples? considering it is primarily a thermostat) up as a medica player via the above custom integration. 

There are Google Home devices configured throughout the house that can play from thier cloud services and stream from Pi Music Box.  These got easily configured as media players via Nabu Casa integration. These are explained in Voice Assistants section. 