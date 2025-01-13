# JavaScript file load
Demonstration of different ways of loading a JavaScript file in HTML.

## Instructions
**Traditional loading**

Open `index.html` in a browser, then open the browser developer tools. The console will show an error. The reason is that the external file `script.js` is loaded in the page header. As said file loads and executes, it tries to interact with the page's `<body>` element before HTML is parsed.

A traditional solution consists in loading the JavaScript file at the end of the HTML document, but it diminishes performance by delaying page load.

**Traditional loading with DOMContentLoaded**

To avoid the previous issue, a common technique was to include the JavaScript code in an event listener for the `DOMContentLoaded` event, which executes once all elements on the page are loaded. This technique is exemplified in `index_dcl.html`.

**Async and defer**

Now open either `index_async.html` or `index_defer.html`, which use the `async` and `defer` attributes respectively. In both cases, `script.js` will load in parallel to HTML parsing, thus increasing performance.

In the case of `defer`, `script.js` will not start execution until the HTML is fully parsed. No errors are expected here, and it is not necessary to create an event listener on `DOMContentLoaded`.

In the case of `async`, `script.js` will start to execute right after being loaded. For a page as small as this one it is fine, since HTML will be fully parsed before JavaScript code executes.

**Potential issues with async**

Open `index_async2.html`. It first loads `long.js` and then `short.js`, both of them with `async`. At the end of `long.js` (which is just the 290Kb jQuery library), a `<div>` is added to the page. Said `<div>` is accessed in `short.js`. This causes an error (check the console), as asynchronous loading causes `short.js` to execute before `long.js` is fully loaded.

Now change both `async` to `defer`. The error is gone and the code works as expected.

**Modules**

Open `index_module.html`. It opens `script.js` as a module, thus it is loaded deferredly by default. Again, it is not necessary to create an event listener on `DOMContentLoaded`. JavaScript modules have wide browser support, so this is the recommended option.

Notice that, if a JavaScript file is loaded as a module, `'use strict'` is not necessary, as modules are automatically in strict mode.

## Further information
- [MDN - Script loading strategies](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/What_is_JavaScript#script_loading_strategies)
- [Web Developer - HTML Script Element Attributes: async vs. defer vs. type='module'](https://webdeveloper.beehiiv.com/p/html-script-element-attributes-async-vs-defer-vs-typemodule)
- [JavaScript.info - Scripts: async, defer](https://javascript.info/script-async-defer)

## Tools
JavaScript / HTML5

## Author:
Arturo Mora-Rioja