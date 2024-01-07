---
title: "Jekyll Image Alignment"
description: ""
excerpt: ""
date: 2021-10-22T19:25:21-04:00
draft: false
weight: 50
images: []
categories: [Jekyll]
tags: [Jekyll, CSS]
contributors: []
pinned: false
homepage: false
---

Jekyll image shortcode does not have an option for aligining the image to left, right, or centre.  This makes formatting paragraphs with images unwieldy.  

Thankfully, many markdown commands let you to add 'extra' processors to support options for the commands.  Here is an alternative  that used the ALT tag and a CSS selector on the alt tag... Instead, add a URL hash like this:

Here is the Markdown image code:

```md
![my image](/img/myImage.jpg#left)
![my image](/img/myImage.jpg#right)
![my image](/img/myImage.jpg#center)
```

Note the added URL hash #center.

Now add this rule in CSS using CSS 3 attribute selectors to select images with a certain path.

```css
img[src*='#left'] {
    float: left;
}
img[src*='#right'] {
    float: right;
}
img[src*='#center'] {
    display: block;
    margin: auto;
}
```

You should be able to use a URL hash like this almost like defining a class name and it isn't a misuse of the ALT tag like some people had  commented about for that solution. It also won't require any additional  extensions. Do one for float right and left as well or any other styles  you might want.

Thanks: [Stack Overflow](https://stackoverflow.com/questions/255170/markdown-and-image-alignment/16278366#16278366)