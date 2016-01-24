---
title: Prioritizing layouts with the order property
date: 2016-01-24 10:57:09
tags:
  - css
  - layout
  - flexbox
  - order
---

In my last post I wrote about building [responsive layouts with flexbox](/2016/01/responsive-layouts-with-flexbox/), but we can take it one step further and use the [order](https://developer.mozilla.org/en-US/docs/Web/CSS/order) property to help prioritize those layouts.

Let's pretend we have a fairly typical two column layout with a sidebar on the left, and a section for the page content on the right.

We start with some simple markup.

```language-markup
<div class="layout">
  <aside class="layout__sidebar"></aside>
  <main class="layout__main"></main>
</div>
```

Then we add the following CSS to get a working responsive layout.

```language-css
.layout {
  display: flex;
  flex-wrap: wrap;
}

.layout__sidebar {
  flex: 1 1 200px;
}

.layout__main {
  flex: 20 1 600px;
}
```

We set the main column to `flex: 20 1 600px`. That is shorthand for `flex-grow: 20`, `flex-shrink: 1`, and `flex-basis: 600px`. The `flex-grow` will make the main column grows 20 times more than the sidebar, which causes the sidebar to almost stay the same size. The flex-basis of `600px` is so that it will wrap when it shrinks below that width.

Here is an example [codepen](http://codepen.io/dfmcphee/pen/vLWPYb?editors=1100). Try resizing your browser and notice how the sidebar goes above the main content on smaller screens. This may be fine for some designs, but let's pretend the sidebar content isn't that important and we don't want it to be the highest priority on smaller screens.

This is where we can allow the `order` property to work its magic.

First, let's rearrange that markup we had created to look like this.

```language-markup
<div class="layout">
  <main class="layout__main"></main>
  <aside class="layout__sidebar"></aside>
</div>
```

We change the order in the DOM so that by default the sidebar will come after the main content. We can then use the `order` property to change the visual order on larger screens.

Then we create a breakpoint at the width where our layout will wrap. This will be the sum of the sidebar flex-basis (`200px`), and the main content flex-basis (`600px`). This is even easier if we are using a preprocessing language like LESS or Sass because we can create variables for these values and then add them automatically for the breakpoint.

Finally, we change the order of both the sidebar and main column using the `order` property.

```language-css
@media (min-width: 800px) {
  .layout__sidebar {
    order: 1;
  }

  .layout__main {
    order: 2;
  }
}
```

Now when we resize our browser the sidebar will be to the left of the main content when there is enough space, and underneath on smaller screens. You can see a working example in this [codepen](http://codepen.io/dfmcphee/pen/vLdVde?editors=1100).

## Hold up, are you sure this is a good idea?

This is a useful technique and can be a big help when it makes sense to reorganize content at different screen sizes, but it should be used with caution.

There are some drawbacks to only reorganizing content visually, and not the actual DOM elements themselves. Unexpected tab order may be confusing to users. Even though an input appears to come before another, it could actually be reversed in the tab order.

Still, in some cases that makes sense anyway. So like Spider-Man once said, "with great power, comes great responsibility". Use it responsibly.
