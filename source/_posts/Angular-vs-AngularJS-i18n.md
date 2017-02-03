---
title: Angular vs AngularJS i18n
date: 2016-09-28 20:54:17
tags: Angular, Browser APIs
---
I was recently looking into how Angular differs from AngularJS in regards to internationalization (also known as i18n).  I was delighted to see Angular makes use of the Internationalization API to perform date and currency conversions.  This allows language specific formatting to be preformed directly by the browser.

To contrast, in AngularJS a developer would be required to load a culture specific helper script that would provide the proper formats per culture.  With Angular and a modern browser, this is functionality is supported out-of-the-box.

The Internationalization API is supported in the following browsers, to get Angular pipes to work with older IE and Safari 9 a polyfill is required.

Can I Use internationalization? [Checkout the support](http://caniuse.com/#feat=internationalization) for the internationalization API across the major browsers from [caniuse.com](http://caniuse.com).