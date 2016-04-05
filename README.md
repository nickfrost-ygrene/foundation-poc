# Foundation grid bug proof-of-concept

## [Demo 1](https://nickfrost-ygrene.github.io/foundation-poc/demo1.html)

```html
...
<body>
  <div class="grid-frame vertical">
    <header>
      <div id="header" class="grid-block">
        <h1>#header</h1>
      </div>
    </header>
    <div class="grid-block vertical">
      <div lass="grid-content" id="content">
        <h1>#content</h1>
        ...
```

This vertical grid is rendered differently in Safari than in Chrome. When a
``grid-block`` element is nested inside a non-``grid-block`` element, Chrome
sets the parent element's height to the height of the children of the
``grid-block``, in this case the ``<header>``'s height is set to the ``<h1>``'s.
Safari does not.

The result is that Foundation renders the header height proportionally relative
to ``#content``'s height. Since there is no minimum height on the ``<header>``,
it shrinks, with its contents overflowing and ``#content`` rendered over it.

Note the black border in demo, it shows the height Foundation is giving the
``<header>``, while it is overridden to a minimum height of its children in
Chrome.

## [Demo 2](https://nickfrost-ygrene.github.io/foundation-poc/demo2.html)

```html
<header class="grid-block">
  <div id="header" class="grid-content">
```

This is the correct usage of the grid system, and behaves the same across
browsers. Since we don't want to shrink our header, browsers will respect a
``min-height`` CSS property. (however, it will override ``height``)

## [Demo 3](https://nickfrost-ygrene.github.io/foundation-poc/demo3.html)

```html
<header class="grid-block" style="min-height: 76px">
  <div id="header" class="grid-content">
```
