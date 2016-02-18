# Baseline.js

seeAlso [Changes in this fork ...](#CHANGES)

Baseline.js is a simple jQuery / Zepto plugin for restoring baselines thrown off by odd image sizes.

Simply call the plugin like so, passing the height of your baseline as a variable. It even works on responsive designs!

```javascript
$('img').baseline(24); // Apply a 24px baseline to all images on the page
$('.content img').baseline(30); // Apply a 30px baseline to all images inside .content
```

You can also define multiple baselines for different breakpoints. Perfect for responsive design!

```javascript
$('.content img').baseline({ '0px': 24, '700px': 30 }); // Apply a 24px baseline for all widths, 30px for widths above 700px
```

Or you can pass a function that must return a number which is used as the grid size.

```javascript
$('.content img').baseline(function() {
  // Get the current font-size from the HTML tag – the root font-size `rem` –
  // which may change through to some CSS media queries
  return parseFloat(getComputedStyle(document.documentElement, null).getPropertyValue('font-size'));
});
```

The used CSS may look like:

```css
html   { font-size: 12px; }
@media (min-width: 480px) {
  html { font-size: 13px; }
}
@media (min-width: 720px) {
  html { font-size: 14px; }
}
@media (min-width: 1024px) {
  html { font-size: 15px; }
}

body {
  /* This one is a computed value based on the given root em
   * and is used as the final font-size for body copy. */
  font-size: 1.2rem;
}
```


## Vanilla JS

Baseline.js is also available without jQuery or Zepto.

```javascript
baseline('img', 24); // Apply a 24px baseline to all images on the page
baseline('.content img', 30); // Apply a 30px baseline to all images inside .content
baseline('.content img', {0:24, 700:30}); // Apply a 24px baseline for all widths, 30px for widths above 700px
```

The first parameter accepts either a selector string or one or more elements, e.g. selected through `document.getElementById()`.

The vanilla JS version was initially created by the rocking [Ben Howdle](https://twitter.com/benhowdle).

---
<a name='CHANGES'/>
## Changes in this fork

- Makes use of `.getBoundingClientRect`'s `height` if possible. <br>(It returns a float which is better for device pixels)

- You can now specify your baseline-rules directly in CSS, for example:

```css
.baselined,
.baselined[data-baseline="1.8rem"],
.ui.list[data-baseline="1.8rem"] {
  position: relative;
  top: -.25em;
};
```

and just include the script (no IE < 9 yet).

• This rule declares the .js enhancement
```css
.baselined[data-baseline="1.8rem"] {};
```
.js will now add the data-baseline attribute as unitless pixels, e.g. <br>[data-baseline="27"] for a 15px font...<br>
So:

• This rule will work always ...
```css
.baselined {}
```

• This rule will work only if JS did its work ...
```css
.baselined[data-baseline] {}
```

## License

Baseline.js is licensed under the [WTFPL license.](http://sam.zoy.org/wtfpl/)
