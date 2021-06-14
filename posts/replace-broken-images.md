---
title: Replace broken images
category: Basic
tags:
  - posts
layout: layouts/post.njk
metadata:
  keywords:
---

Replace the broken images with an image telling visitors that they are not found:

```js
// Assume that I want to replace all images on the page
const images = document.querySelectorAll('img');

// Loop over them
[].forEach.call(images, function(ele) {
    ele.addEventListener('error', function(e) {
        e.target.src = '/path/to/404/image.png';
    });
});
```

## More

* [Attach or detach an event handler](/attach-or-detach-an-event-handler)
* [Loop over a nodelist](/loop-over-a-nodelist)