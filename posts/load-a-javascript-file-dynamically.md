---
title: Load a javascript file dynamically
category: Intermediate
tags:
  - posts
layout: layouts/post.njk
metadata:
  keywords:
---

## Load a JavaScript file

```js
// Create new script element
const script = document.createElement('script');
script.src = '/path/to/js/file.js';

// Append to the `head` element
document.head.appendChild(script);
```

## Execute code when the JavaScript file is loaded

```js
// Create new script element
...
script.addEventListener('load', function() {
    // The script is loaded completely
    // Do something
});

// Append to the `head` element
...
```

## Load multiple JavaScript files in order

Assume that you want to load an array of JavaScript files, `arrayOfJs`, in order.

To do that, we have to load the first script, and load the second script when the first one is loaded completely. And continue doing so until all scripts are loaded.

```js
// Load a script from given `url`
const loadScript = function(url) {
    return new Promise(function(resolve, reject) {
        const script = document.createElement('script');
        script.src = url;

        script.addEventListener('load', function() {
            // The script is loaded completely
            resolve(true);
        });

        document.head.appendChild(script);
    });
};

// Perform all promises in the order
const waterfall = function(promises) {
    return promises.reduce(
        function(p, c) {
            // Waiting for `p` completed
            return p.then(function() {
                // and then `c`
                return c().then(function(result) {
                    return true;
                });
            });
        },
        // The initial value passed to the reduce method
        Promise.resolve([])
    );
};

// Load an array of scripts in order
const loadScriptsInOrder = function(arrayOfJs) {
    const promises = arrayOfJs.map(function(url) {
        return loadScript(url);
    });
    return waterfall(promises);
};
```

The `loadScriptsInOrder` function returns a `Promise` indicates whether all scripts are loaded successfully:

```js
loadScriptsInOrder([
    '/path/to/file.js',
    '/path/to/another-file.js',
    '/yet/another/file.js',
]).then(function() {
    // All scripts are loaded completely
    // Do something
})
```

## More

* [Change the website favicon](/change-the-website-favicon)
* [Load a css file dynamically](/load-a-css-file-dynamically)