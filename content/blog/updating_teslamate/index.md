---
title: "Updating Teslamate"
description: ""
excerpt: ""
date: 2021-12-22T21:31:50-04:00
draft: false
weight: 50
images: []
categories: [Home Automation]
tags: [TeslaMate, Tesla]
contributors: []
pinned: false
homepage: false
---

First create a backup, just in case anything goes wrong.  Check it is done.  You may probably want to move/copy it to another machine as well. 

```zsh
mkdir backup
docker-compose exec -T database pg_dump -U teslamate teslamate > backup/teslamate.bck
cd backup/
ls -al
```

Now, get back to the directory where the docker file is, and run these commands sequentially. 

```zsh
cd ..
docker-compose pull
docker-compose up -d
```

That's it.  Once it is complete.  Check the teslamate page and grafana page.  Everything should look good.  If you get an error, just try rebooting

```zsh
sudo reboot
```

If you ever want to periodically backup, get to the root folder and run the backup command. 