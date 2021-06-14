---
title: Show a loading indicator when an iframe is being loaded
category: Intermediate
tags:
  - posts
layout: layouts/post.njk
metadata:
  keywords: addEventListener, hide element, iframe load event, show loading indicator
---

It's always a good practice to let user know what is happenning. This post demonstrates a common case where we show a loading indicator while an iframe is being loaded.

Here is our iframe:

```html
<iframe id="frame"></iframe>
```

## The markup

The loading indicator and iframe are organized as following:

```html
<div class="container">
    <!-- The loading indicator -->
    <div class="loading" id="loading">
        Loading
    </div>

    <!-- The iframe -->
    <iframe id="frame" style="opacity: 0"></iframe>
</div>
```

Initially, the iframe will be hidden by setting the opacity to zero. On the other hand, the loading indicator could be displayed at the center and on top of the iframe. 

We can apply some CSS styles to the container and loading elements:

```css
.container {
    /* To position the loading */
    position: relative;
}

.loading {
    /* Absolute position */
    left: 0;
    position: absolute;
    top: 0;

    /* Take full size */
    height: 100%;
    width: 100%;

    /* Center */
    align-items: center;
    display: flex;
    justify-content: center;
}
```

{% callout %}
### Resource

This [page](https://csslayout.io/patterns/centering) introduces the most simple way to center an element in both horizontal and vertical directions.
{% endcallout %}

## Handle the event

The layout looks good now. By default, user will see only the loading indicator. We will [hide](/show-or-hide-an-element) the loading indicator (or even [remove](/remove-an-element) it if you want) as soon as the iframe is loaded:

```js
// Query the elements
const iframeEle = document.getElementById('iframe');
const loadingEle = document.getElementById('loading');

iframeEle.addEventListener('load', function() {
    // Hide the loading indicator
    loadingEle.style.display = 'none';

    // Bring the iframe back
    iframeEle.style.opacity = 1;
});
```

## More

* [Attach or detach an event handler](/attach-or-detach-an-event-handler)
* [Remove an element](/remove-an-element)
* [Resize an iframe to fit its content](/resize-an-iframe-to-fit-its-content)
* [Set css style for an element](/set-css-style-for-an-element)
* [Show or hide an element](/show-or-hide-an-element)