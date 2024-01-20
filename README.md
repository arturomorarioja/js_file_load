# JavaScript file load

## Purpose
Demonstration of the modern JavaScript file loading in HTML.

## Instructions
**Traditional loading**

Open `index.html` in a browser, then open the browser developer tools. The console will show an error. The reason is that the external file `script.js` is loaded in the page header. As said file loads and executes, it tries to interact with the page's `<body>` element before HTML is parsed.

A traditional solution consists in loading the JavaScript file at the end of the HTML document, but it diminishes performance by delaying page load.

**Async and defer**

Now open either `index_async.html` or `index_defer.html`, which use the `async` and `defer` attributes respectively. In both cases, `script.js` will load in parallel to HTML parsing, thus increasing performance.

In the case of `defer`, `script.js` will not start execution until the HTML is fully parsed. No errors are expected here.

In the case of `async`, `script.js` will start to execute right after being loaded. For a page as small as this one it is fine, since HTML will be fully parsed before JavaScript code executes.

**Potential issues with async**

Open `index_async2.html`. It first loads `long.js` and then `short.js`, both of them with `async`. At the end of `long.js` (which is just the 290Kb jQuery library), a `<div>` is added to the page. Said `<div>` is accessed in `short.js`. This causes an error (check the console), as asynchronous loading causes `short.js` to execute before `long.js` is fully loaded.

Now change both `async` to `defer`. The error is gone and the code works as expected.

## Further information
- https://javascript.info/script-async-defer
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript, section "Script loading strategies"

## Tools
JavaScript / HTML5

## Author:
Arturo Mora-Rioja