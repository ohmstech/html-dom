---
title: Make a draggable element
category: Advanced
tags:
  - posts
layout: layouts/post.njk
metadata:
  keywords:
---

Assume that we want to turn the following element to draggable element:

```html
<div id="dragMe" class="draggable">Drag me</div>
```

The element needs to have the following styles:

```css
.draggable {
    /* Indicate the element draggable */
    cursor: move;

    /* It will be positioned absolutely */
    position: absolute;

    /* Doesn't allow to select the content inside */
    user-select: none;
}
```

In order to make it draggable, we need to handle three events:

* `mousedown` on the element: Track the current position of mouse
* `mousemove` on `document`: Calculate how far the mouse has been moved, and determine the position of element
* `mouseup` on `document`: Remove the event handlers of `document`

```js
// The current position of mouse
let x = 0;
let y = 0;

// Query the element
const ele = document.getElementById('dragMe');

// Handle the mousedown event
// that's triggered when user drags the element
const mouseDownHandler = function(e) {
    // Get the current mouse position
    x = e.clientX;
    y = e.clientY;
    
    // Attach the listeners to `document`
    document.addEventListener('mousemove', mouseMoveHandler);
    document.addEventListener('mouseup', mouseUpHandler);
};

const mouseMoveHandler = function(e) {
    // How far the mouse has been moved
    const dx = e.clientX - x;
    const dy = e.clientY - y;

    // Set the position of element
    ele.style.top = `${ele.offsetTop + dy}px`; 
    ele.style.left = `${ele.offsetLeft + dx}px`;

    // Reassign the position of mouse
    x = e.clientX;
    y = e.clientY;
};

const mouseUpHandler = function() {
    // Remove the handlers of `mousemove` and `mouseup`
    document.removeEventListener('mousemove', mouseMoveHandler);
    document.removeEventListener('mouseup', mouseUpHandler);
};

ele.addEventListener('mousedown', mouseDownHandler);
```

{% callout %}
### Tip

This post uses the [Attach event handlers inside other handlers](/attach-event-handlers-inside-other-handlers) tip.
{% endcallout %}

## Use cases

We can use the technique in this post to 

1. [Create a range slider](/create-a-range-slider)
2. [Create an image comparison slider](/create-an-image-comparison-slider)
3. [Create resizable split views](/create-resizable-split-views)
4. [Drag to scroll](/drag-to-scroll)
5. [Resize columns of a table](/resize-columns-of-a-table)

## Demo

<iframe src='/demo/make-a-draggable-element/index.html'></iframe>

## More

* [Attach event handlers inside other handlers](/attach-event-handlers-inside-other-handlers)
* [Attach or detach an event handler](/attach-or-detach-an-event-handler)
* [Calculate the mouse position relative to an element](/calculate-the-mouse-position-relative-to-an-element)
* [Create a range slider](/create-a-range-slider)
* [Create an image comparison slider](/create-an-image-comparison-slider)
* [Create resizable split views](/create-resizable-split-views)
* [Drag and drop element in a list](/drag-and-drop-element-in-a-list)
* [Drag and drop table column](/drag-and-drop-table-column)
* [Drag and drop table row](/drag-and-drop-table-row)
* [Drag to scroll](/drag-to-scroll)
* [Make a resizable element](/make-a-resizable-element)
* [Resize columns of a table](/resize-columns-of-a-table)
* [Set css style for an element](/set-css-style-for-an-element)
* [Show a ghost element when dragging an element](/show-a-ghost-element-when-dragging-an-element)
* [Zoom an image](/zoom-an-image)