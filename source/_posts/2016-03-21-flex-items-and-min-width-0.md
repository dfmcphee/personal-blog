---
title: Flex items and min-width 0
date: 2016-03-21 20:57:51
tags:
---

Earlier I wrote about [using flexbox to build responsive layouts](/2016/01/responsive-layouts-with-flexbox/). There is a behavior that can be surprising when using flexbox for layout like this. Let’s say you have a long url displayed somewhere in your layout that you want to truncate. Applying `overflow: hidden` will not cause the flex item to shrink like you might expect. You can see an example in this  [codepen](http://codepen.io/dfmcphee/pen/reyPLa?editors=1100) when resizing your browser.

This may appear as a bug, but it is actually a part of the [spec for flexbox](https://www.w3.org/TR/2016/CR-css-flexbox-1-20160301/#flex-common).

It states:

> By default, flex items won’t shrink below their minimum content size

This means whenever you include a child element with `overflow` set to anything other than `visible`, and its content is wider than the bounds you set in the layout, the item won’t shrink past that width. This can result in layouts appearing uneven or wrapping too early. By adding `min-width: 0` to the item, it will resize at the correct ratio and still apply the overflow as desired. You can see an example [here](http://codepen.io/dfmcphee/pen/aNJXEp?editors=1100).

For more reading on this issue and others related to flexbox see this [list of known bugs](https://github.com/philipwalton/flexbugs#1-minimum-content-sizing-of-flex-items-not-honored) and the [w3 spec](https://www.w3.org/TR/2016/CR-css-flexbox-1-20160301/#min-size-auto).
