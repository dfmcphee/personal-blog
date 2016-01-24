---
title: Responsive layouts with flexbox
date: 2016-01-17 11:19:56
tags:
  - css
  - flexbox
  - layout
---

Recently I have been playing around with some new ideas for responsive layouts. Typically one would probably set some breakpoints and use media queries throughout their CSS to change the layout at different screen sizes. This works, but you can also end up having many different breakpoints that can be difficult to manage. An alternative approach is to use flexbox with the flex-wrap property and let the component or content dictate how it fits into the layout.

Let's assume we have this markup for a two column layout.

```language-markup
<div class="layout">
  <div class="layout__item"></div>
  <div class="layout__item"></div>
</div>
```


First, we allow the flex container to wrap its children as needed.

```language-css
.layout {
  display: flex;
  flex-wrap: wrap;
}
```


Then we specify the preferred min-width of the children using the `flex-basis` property. We also allow the items to grow and shrink as needed.

```language-css
.layout__item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 200px;
}
```


Or even better, we can shorten this to one line using the shorthand flex property.

```language-css
.layout__item {
  flex: 1 1 200px;
}
```


With just these few lines of CSS we already have a working responsive layout. The key here is the flex-basis that is being set to a specific width. This allows the item to wrap when it can't fit into that minimum size that it prefers. This is also nice because when it does wrap, it can still stretch to fill the container. Our component can now dictate the space it requires and respond correctly to fit itself into the layout. We also don't even need any media-queries to do it. Neat.

You can see the working example on [codepen](http://codepen.io/dfmcphee/pen/pgrGmW).