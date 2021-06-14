---
title: Get the document height and width
category: Basic
tags:
  - posts
layout: layouts/post.njk
metadata:
  keywords: clientHeight, clientWidth, document height, document width, offsetHeight, offsetWidth, scrollHeight, scrollWidth
---

## Get the document height

```js
// Full height, including the scroll part
const fullHeight = Math.max(
    document.body.scrollHeight, document.documentElement.scrollHeight,
    document.body.offsetHeight, document.documentElement.offsetHeight,
    document.body.clientHeight, document.documentElement.clientHeight
);
```

## Get the document width

```js
// Full width, including the scroll part
const fullWidth = Math.max(
    document.body.scrollWidth, document.documentElement.scrollWidth,
    document.body.offsetWidth, document.documentElement.offsetWidth,
    document.body.clientWidth, document.documentElement.clientWidth
);
```

## More

* [Check if an element is in the viewport](/check-if-an-element-is-in-the-viewport)