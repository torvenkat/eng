---
title: "Calibre-Web Open Media Vault"
description: ""
excerpt: ""
date: 2022-04-05T19:41:11-04:00
draft: false
weight: 50
images: []
categories: [Open Media Vault]
tags: [OMV, Calibre, Books]
contributors: []
pinned: false
homepage: false
---

Docker image available at: https://hub.docker.com/r/linuxserver/calibre-web 

Use Stacks in Portainer for easy installation, 

``` yaml 
version: "2.1"
services:
  calibre-web:
    image: lscr.io/linuxserver/calibre-web
    container_name: calibre-web
    environment:
      - PUID=998
      - PGID=100
      - TZ=America/Toronto
    volumes:
      - /srv/dev-disk-by-uuid-4154932d-19c8-4da9-9f47-ab5119d6a980/config/calibre:/config
      - /srv/dev-disk-by-uuid-4154932d-19c8-4da9-9f47-ab5119d6a980/eBook_library:/books
    ports:
      - 8083:8083
    restart: unless-stopped
```

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=998` and `PGID=100`, to find yours use `id user` as below:

```bash
  $ id username
    uid=1000(dockeruser) gid=1000(dockergroup) groups=1000(dockergroup)
```

At this point you may want to verify if the docker container is installed properly and running.  You can try logging into Calibre-Web. 

Webui can be found at `http://your-ip:8083`

**Default admin login:** _Username:_ admin _Password:_ admin123

You will be asked to locate the metadata.db file. 


On the initial setup screen, enter _/books_ as your calibre library location. But you will not find the database file.  There is an easy work around.  You need to copy an empty database 
[Ref](https://forum.openmediavault.org/index.php?thread/39073-calibre-web-portainer/&postID=274530#post274530)

Download an empty database from [here](https://drive.google.com/file/d/1zY07g_V9Yxx5p7YCIUXX1CSxVLJWd2a8/view?usp=sharing)

The dowloaded file will be *metadata.db.empty* 

Remove the _.empty_ from file name and upload to the _/books_ folder (which is the same as _- /srv/dev-disk-by-uuid-4154932d-/eBook_library:/books_     in the above configuration example.  So, you can use Samba mount to upload the *metadata.db* file (or use an sftp client).  

In my case, the file was uploaded without write permission, this had to be fixed.  

Login into Portainer.  Using that get into the console of the docker container.  Go to the _/books_ folder and fix the file permission. 

Now, in the web interface if you select /books for your metadata location, you will see the empty file there and everything should work fine. 

You will not be able to bulk upload your book collection and get them into calibre database by scanning for metadata.  The books need to be uploaded one by one.  In order to do that,

Go to the _Admin Panel >  Settings > Basic Configuration > Features_

Check and opt to enable upload books and save the settings.  Now you will see the upload enabled in the menu at the top.  Use that to upload your book (and fix metadata if needed by searching at google or amazon).  That's it. 