---
title: core-js Merged into Angular
date: 2016-09-21 20:50:29
tags: Angular
---

[core-js](https://github.com/zloirock/core-js) is a modular library created by Denis Pushkarev that’s recently been opening some eyes in the web comm
Previously, it has gained serious reputation by use of Babel, which utilizes it for many of its polyfills.  
[Most recently](https://github.com/angular/angular/commit/66df335998d097fa8fe46dec41f1183737332021), it was pulled into Angular as the de facto standard for shimming older IE 9-10 with ES2015 features.

What makes core-js unique is how beautifully architected it is.  Each polyfill can be pulled in individually, making it a truly modular library.  As with other libraries such as es6-shim a developer would need to require the entire library to make use of one ES2015 feature like promises.  With core-js a developer can simply import a Promise polyfill with one import.

For example, using a bundler such as Webpack, you can compose your own polyfill.js with only the polyfills the application requires.
```javascript
require('core-js/fn/map');
require('core-js/fn/set');
require('core-js/fn/weak-map');
require('core-js/fn/promise');
```
More impressively core-js’s [browser support](https://github.com/zloirock/core-js#supported-engines) goes all the way back to IE6.

If you’re looking for a one-stop shop library to provide polyfills, core-js is it!