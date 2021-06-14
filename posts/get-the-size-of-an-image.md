---
title: Get the size of an image
category: Basic
tags:
  - posts
layout: layouts/post.njk
metadata:
  keywords:
---

## Image is already loaded

```js
const image = document.querySelector(...);

// Get the original size
const naturalWidth = image.naturalWidth;
const naturalHeight = image.naturalHeight;

// Get the scaled size
const width = image.width;
const height = image.height;
```

## Image is not loaded yet

Listen on the `load` event to calculate the size of image which can be loaded via a given URL:

```js
const image = document.createElement('img');
image.addEventListener('load', function(e) {
    // Get the size
    const width = e.target.width;
    const height = e.target.height;
});

// Set the source
image.src = '/path/to/image.png';
```

We can use a `Promise` to turn the snippet to a reusable function:

```js
const calculateSize = function(url) {
    return new Promise(function(resolve, reject) {
        const image = document.createElement('img');
        image.addEventListener('load', function(e) {
            resolve({
                width: e.target.width,
                height: e.target.height,
            });
        });

        image.addEventListener('error', function() {
            reject();
        });

        image.src = url;
    });
};

calculateSize('/path/to/image.png').then(function(data) {
    const width = data.width;
    const height = data.height;
});
```

## Use case

Assume that you want to show the size of avatar which can be uploaded via a file input:

```html
<input type="file" id="avatar" />

<!-- Display the size -->
<div id="size" />
```

First, we need to get the selected file, and then load it via `FileReader`:

```js
const avatarEle = document.getElementById('avatar');
const sizeEle = document.getElementById('size');

avatarEle.addEventListener('change', function(e) {
    // Get the selected file
    const file = e.target.files[0];

    const reader = new FileReader();
    reader.readAsDataURL(file);
    reader.addEventListener('loadend', function(e) {
        const src = e.target.result;

        calculateSize(src).then(function(data) {
            const width = data.width;
            const height = data.height;

            sizeEle.innerHTML = `${width} x ${height}`;
        });
    });
});
```

## More

* [Attach or detach an event handler](/attach-or-detach-an-event-handler)
* [Preview an image before uploading it](/preview-an-image-before-uploading-it)