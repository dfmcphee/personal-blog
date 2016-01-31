---
title: Building a CSS component with BEM
date: 2016-01-30 21:18:18
tags:
  - CSS
  - Components
  - BEM
---

This article will walk you through creating a simple component in CSS.

## Why a component?
As your CSS for a project gets larger, a single CSS file with random selectors will become more and more difficult to navigate. It may also cause you to run into issues with specificity as you add more complicated selectors to target elements. You will need a way to organize this to make it reusable and allow it to scale.

This is why many developers believe it is best to split your CSS into separate components that have specific purposes using a modular approach like [BEM](https://en.bem.info/method/key-concepts/) or [SMACSS](https://smacss.com/).

For example, let's say we want to create a new way to alert users with some information. Sometimes it will be just generic information, but other times it will be an error or success message. We will start with some simple markup.

```language-markup
<div class="alert"></div>
```

In BEM the `B` stands for block. The block is just the base class of the component. In this case we will use the class `alert` as the base. We use that class to add some styling to the default alert.

```language-css
.alert {
  background: DeepSkyBlue;
  border: 1px solid DodgerBlue;
  color: white;
  padding: 20px;
}
```

This message should have a title, so we add a new heading to our markup with the class `alert__title`. The double underscore here signifies that the `title` element belongs to the `alert` component. In BEM the `E` stands for element, but this can also just be thought of as a sub-component.

```language-markup
<h2 class="alert__title">Alert</h2>
```

```language-css
.alert__title {
  font-size: 1.2rem;
  font-weight: 300;
}
```

Because the selector is just a single class, it doesn't add any extra [specificity](https://developer.mozilla.org/en/docs/Web/CSS/Specificity). This helps to avoid issues when trying to overwrite rules later on.

The other nice thing about the selector is that we can easily change the element if needed. Say we decide these titles should be `h3`s instead of `h2`s semantically. We can simply change the heading level and the styling will still work.

We also want this alert to have a more detailed message so we add another new sub-component. We use the class `alert__message` for this.

```language-markup
<p class="alert__message">Details alert message</p>
```

```language-css
.alert__message {
  font-size: 0.9rem;
  font-weight: 400;
}
```

But we don't just want to use the alert for basic information, we also want to use it to display errors to the user. To do this we create a new variant of our alert component. In BEM the `M` stands for modifier. We use the class `alert--error` because the two hyphens signify it is a modifier on the component. Modifiers can be used to create new variations of a component.

```language-markup
<div class="alert alert--error">
  <h2 class="alert__title">Error</h2>
  <p class="alert__message">Error message.</p>
</div>
```

```language-css
.alert--error {
  background: Crimson;
  border-color: FireBrick;
}
```

You will notice we use both the `alert` class as well as `alert--error`. This allows us to inherit the text color and padding styles from a default alert, but also overwrite with the background and border color we want for an error. Notice we use `border-color` here as to not overwrite the other `border` properties as well.

We can also have multiple modifiers for a component. Let's say we also want to display a success message to the user. We add another variant to the component to accomplish this.

```language-markup
<div class="alert alert--success">
  <h2 class="alert__title">Success</h2>
  <p class="alert__message">Success message.</p>
</div>
```

```language-css
.alert--error {
  background: YellowGreen;
  border-color: LimeGreen;
}
```

So there you have it. A simple component that is flexible and can be reusable in your markup. You can see an example in this [codepen](http://codepen.io/dfmcphee/pen/ZQRxoE?editors=1100).

This same concept can be applied to all the pieces of your design system as you build them. Although all the hyphens and underscores in BEM may seem wacky at first, they will make it easier to parse mentally when looking at them. You may find it cumbersome at first, but you will thank yourself later on.

> Build for the future.
