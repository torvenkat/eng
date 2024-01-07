---
title: "Multi-level, deep lists in Dokuwiki"
description: ""
excerpt: ""
date: 2018-08-26T04:39:35-04:00
lastmod: 2018-08-26T04:39:35-04:00
draft: false
weight: 50
images: [multilevel_list.png]
categories: [Linux]
tags: [Linux, DokuWiki]
contributors: []
pinned: false
homepage: false
---
Dokuwiki is built in with only up to 3 levels of nested listing.  If you need to go deep in listing (such as 2.3.2.4.1) for sub-sections, follow these steps. 

Install the <a href="https://www.dokuwiki.org/plugin:wrap" target="_blank">wrap</a> plugin. 

Add the following code to the userstyle.css file (to be placed in <dokuwiki_root>/conf/

```
div.dokuwiki div.wrap_list-deep ol {
  list-style-type: none;
}
 
div.dokuwiki div.wrap_list-deep > ol {
  counter-reset: leva 0; /* set to one lower than intended value of first list item */
}
 
div.dokuwiki div.wrap_list-deep ol li div.li::before {
  counter-increment: leva;
  content: counter(leva) ". ";
  color: inherit;
  font-weight: bold;
}
/* ~~~~~~ */
 
div.dokuwiki div.wrap_list-deep ol ol {
  list-style-type: none;
}
 
div.dokuwiki div.wrap_list-deep > ol ol {
  counter-reset: levb 0; /* set to one lower than intended value of first list item */
}
 
div.dokuwiki div.wrap_list-deep ol li li div.li::before {
  counter-increment: levb;
  content: counter(leva) "." counter(levb) ". ";
  color: inherit;
  font-weight: bold;
}
 
/* ~~~~~~ */
 
div.dokuwiki div.wrap_list-deep ol ol ol {
  list-style-type: none;
}
 
div.dokuwiki div.wrap_list-deep > ol ol ol {
  counter-reset: levc 0; /* set to one lower than intended value of first list item */
}
 
div.dokuwiki div.wrap_list-deep ol ol ol div.li::before {
  counter-increment: levc;
  content: counter(leva) "." counter(levb) "." counter(levc) ". ";
  color: inherit;
  font-weight: bold;
}
```
Within the dokuwiki you can then use simple wiki markdown to get deep-nested (ordered) lists, as follows:
```
  - first level
    - second level
    - second level
  - first level
    - second level
  - first level
    - second level
      - third level
      - third level
   - second level
```