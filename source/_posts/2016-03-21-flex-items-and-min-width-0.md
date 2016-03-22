---
title: Flex items and min-width 0
date: 2016-03-21 20:57:51
tags:
  - CSS
  - Flexbox
  - Layout
---

Earlier I wrote about [using flexbox to build responsive layouts](/2016/01/responsive-layouts-with-flexbox/). There is a behavior that can be surprising when using flexbox for layout like this. Content that is too long can force a flex item to not shrink appropriately. Let’s say for example you have a long URL displayed somewhere in your layout that you want to truncate. Applying `overflow: hidden` will stop the flex item from shrinking like you may expect it to. You can see an example in this  [codepen](http://codepen.io/dfmcphee/pen/reyPLa?editors=1100) when resizing your browser.

This may appear as a bug, but it is actually a part of the [spec for flexbox](https://www.w3.org/TR/2016/CR-css-flexbox-1-20160301/#flex-common).

In the spec it says:

> By default, flex items won’t shrink below their minimum content size

This means the minimum width of an item is set to the width of its content and it won’t shrink past that width. This can result in layouts appearing uneven or wrapping too early. By adding `min-width: 0` to the item, it will resize at the correct ratio and still apply the overflow as desired. You can see an example [here](http://codepen.io/dfmcphee/pen/aNJXEp?editors=1100).

For more reading on this issue and others related to flexbox see this [list of known bugs](https://github.com/philipwalton/flexbugs#1-minimum-content-sizing-of-flex-items-not-honored) and the [w3 spec](https://www.w3.org/TR/2016/CR-css-flexbox-1-20160301/#min-size-auto).
