---
title: Wrappable content with flexbox
date: 2016-02-07 15:58:44
tags:
  - CSS
  - Flexbox
  - Layout
---

Although specifying widths and proportions for layout items works, sometimes you need those widths to be based on the content rather than specific values. Sometimes we won't know how long our content will be. This is where having a layout that responds to its content is handy.

Let's say for example we want to create a list of items. We want the title of the item on the left, and the content for the item on the right. We would prefer if these items stay on one line, but if they don't have enough room, the title should go above the content.

We will start with this markup

```language-markup
<section class="item">
  <div class="item__title">
    <h2>Item title</h2>
  </div>
  <div class="item__content">
    <p>Item content</p>
  </div>
</section>
```

We will now apply a little flexbox magic to get the wrapping we want. First we setup the `item` class as our flex container.

```language-css
.item {
  display: flex;
  flex-wrap: wrap;
}
```

We want the title to only take up as much space as it needs to we set the `flex-grow` and `flex-shrink` properties to `0` with the shorthand `flex: 0 0 auto`.

```language-css
.item__title {
  flex: 0 0 auto;
}
```

The content should take up whatever space is left so we set the `flex-grow` and `flex-shrink` properties to `1` with the shorthand `flex: 1 1 auto`.

```language-css
.item__content {
  flex: 1 1 auto;
}
```

So far, this is great. If our content is too long, it will simply wrap underneath the title. No need to set arbitrary widths or breakpoints to do it either.

But wait, let's say we want some margin in between the title and the content. The problem is, if we add margin to the left or right, it will still be there when it wraps. Luckily there is a bit of a hack we can do to get around this.

First, we add some negative margins to our `item` flex container.

```language-css
.item {
  display: flex;
  flex-wrap: wrap;
  margin-top: -20px;
  margin-bottom: -20px;
}
```

We then add margins on the flex children to counteract the negative margins on the container.

```language-css
.item__title {
  flex: 0 0 auto;
  margin-bottom: 20px;
  margin-left: 20px;
}

.item__content {
  flex: 1 1 auto;
  margin-bottom: 20px;
  margin-left: 20px;
}
```

Now our item can have `20px` of margin between the title and the content, but when it wraps it will still be flush with the edge of the `item`.

We also may want vertical margins between two `item`s. To do this we add another rule to our CSS.

```language-css
.item + .item {
  margin-top: 20px;
}
```

This will add margin to the top of any `item` that is directly following another `item` in the DOM.

So there we have it. A simple way to wrap our layout based on the content within it. It allows us to use a fairly generic structure for all different lengths of content and still have it look nice.

Check out this [codepen](http://codepen.io/dfmcphee/pen/yeRrmy) for an example of this in action.
