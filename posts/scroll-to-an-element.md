---
title: Scroll to an element
category: Basic
tags:
  - posts
layout: layouts/post.njk
metadata:
  keywords: scrollIntoView, scrollIntoView behavior smooth, smoothly scroll
---

## Scroll to the `ele` element

```js
ele.scrollIntoView();
```

## Smoothly scroll

The `behavior` option [isn't supported](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView#Browser_compatibility) in IE and Safari.

```js
ele.scrollIntoView({ behavior: 'smooth' });
```

{% callout %}
### Good to know

The similar CSS property which provides the same functionality is

```css
scroll-behavior: smooth;
``

It [is not supported](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior#Browser_compatibility) in IE and Safari.
{% endcallout %}

## More

* [Scroll to an element smoothly](/scroll-to-an-element-smoothly)
* [Scroll to top of the page](/scroll-to-top-of-the-page)