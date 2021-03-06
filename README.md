# minimodal

Minimal, customizable, responsive modals

Examples available at https://influxweb.github.io/minimodal/

The original script has been updated to allow for `inline` and `iframe` options. The CSS classes have been updated to conform more with a name-spaced, BEM format.

## Features

- Fully responsive with minimal styling
- All scaling and calculations are done through CSS
- Use built-in CSS classes to transition between states (load, previous, next, etc)
- Dependency free (no jQuery)
- Keyboard accessible
- Built-in support for a variety of content types
- Ability to group and navigate between items
- Works in IE 10+ (requires [classList](http://caniuse.com/#search=classlist) support)
    - Close on overlay click uses CSS pointer-events and only works in IE 11+

## Install

### Standard

Include minimodal CSS:

```html
<link href="minimodal.css" rel="stylesheet">
```

Include minimodal JavaScript:

```html
<script src="minimodal.js"></script>
```

Call minimodal on your target elements:

```javascript
var targets = document.querySelectorAll('[data-mini-modal]');
for (var i = 0; i < targets.length; i += 1) {
  var modal = minimodal(targets[i], {
    // options
    statusTimeout: 600,
    removeTimeout: 600,
    closeTimeout: 600
  });
  modal.init();
}
```

### npm

You can also install minimodal using npm:

```
npm install minimodal --save
```

UMD is used to support both AMD and CommonJS environments. For example, with Browserify you could use `var minimodal = require('minimodal');` at the top of the above script block.

## Example

In the above example we're using the `data-mini-modal` attribute to target elements, but you can use whatever selector you'd like. Grouping is done using `data-mini-modal="group-name"` though, so it can be handy to stick with the default for that reason.

```html
<a href="image.jpg" data-mini-modal>image</a>
```

You can link to any of the content types in the next section to have minimodal handle them accordingly.

## Content Types

Most content types will be automatically detected based on the item's href attribute, however some noted below will need to have their types set explicitly.

- Image
  - default fallback if no other type is specified or detected
- YouTube
  - use `https://www.youtube.com/watch?v=xxxxxxxxxxx` format
- Vimeo
  - use `https://vimeo.com/xxxxxxx` format
- Google Maps
  - requires `googleMapsAPIKey` option to be set correctly
  - currently supports place and coordinate modes
    - place mode: `https://www.google.com/maps/place/City,+State/...`
    - coordinate mode: `https://www.google.com/maps/@latitude,longitude,#z...`
- AJAX
  - requires `data-mini-modal-type="ajax"` on triggering item
- iFrame
  - requires `data-mini-modal-type="iframe"` on triggering item
- inline
  - requires `data-mini-modal-type="inline"` on triggering item
  - you can access an element without having an `href` attribute on the triggering element by adding `data-mini-modal-content="ELEMENT"` on the triggering item

## Options

### Markup

Markup for the following elements can be customized when initializing minimodal. Any customizations will be added inside each element's container.

`loadingHTML`

default: 'Loading'

`previousButtonHTML`

default: 'Previous'

`nextButtonHTML`

default: 'Next'

`closeButtonHTML`

default: 'Close'

### Animation

Timeout delays can be used to have certain elements removed from the DOM after a set amount of time. Match up the CSS transition durations with the various timeout options below to have elements removed once their transitions are complete.

`statusTimeout`

default: 0

Delay before `c-mini-modal__status` element is removed from the DOM. This can be used to fade and remove a custom loading spinner once the item is ready, for example.

`removeTimeout`

default: 0

Delay before any `c-mini-modal__item` element is removed from the DOM. When a previous or next button is clicked, the last current item will be removed after this delay. Can be used to transition an old item out of view while the new one loads in.

`closeTimeout`

default: 0

Delay before the root `mini-modal` is removed from the DOM when clicking the close button.

### Other

`googleMapsAPIKey`

default: ''

Enter your API key to enable Google Maps support. Instructions on how to obtain an API key can be found [here](https://developers.google.com/maps/documentation/embed/guide#api_key).

## Classes

### State

`c-mini-modal--active`

Added to the root container once it's been added to the DOM. This class is also removed when the close button is clicked. Add rules to transition between this and the initial root `mini-modal` class to add open/close animations.

`c-mini-modal__item--loading`

Added to an item while loading. Can be used to transition the status element in and out.  Removed once the item has finished loading.

`c-mini-modal__item--loaded`

Added to an item once it has been fully loaded. Can be used to transition in the loaded content.

`c-mini-modal__item--added`

Items will receive this class briefly when they are added to the DOM. It is immediately removed from the item, allowing transitioning between this class and the standard `c-mini-modal__item` class.

`c-mini-modal__item--added--previous`

Modifier class that is briefly added when an item is added via the previous button.

`c-mini-modal__item--added--next`

Modifier class that is briefly added when an item is added via the next button.

`c-mini-modal__item--removed`

This class is added to an item when it is removed from the DOM. Styles can be set for this class to transition an item between it and the standard `c-mini-modal__item` class.

`c-mini-modal__item--removed--previous`

Modifier class that is added to an item when it is removed via the previous button.

`c-mini-modal__item--removed--next`

Modifier class that is added to an item when it is removed via the next button.

## Captions

Use the `title` attribute on your target links to have the contained content appear as a caption. Links and other HTML can be used here as needed.

```html
<a href="image.jpg" title="My caption. <a href='#'>source</a>" data-mini-modal>image</a>
```

## Groups

To group items into a navigable set, add the `data-mini-modal` attribute to each item with a matching value.

```html
<!-- group 1 -->
<a href="image1.jpg" data-mini-modal="group1">image</a>
<a href="image2.jpg" data-mini-modal="group1">image</a>
<a href="image3.jpg" data-mini-modal="group1">image</a>
<!-- group 2 -->
<a href="image4.jpg" data-mini-modal="group2">image</a>
<a href="image5.jpg" data-mini-modal="group2">image</a>
<a href="image6.jpg" data-mini-modal="group2">image</a>
```

Targets don't need to be visible on the page to be grouped, so you could have one visible entry item while all of the others are hidden with CSS.

```html
<a href="image1.jpg" data-mini-modal="group1">image</a>
<a href="image2.jpg" data-mini-modal="group1" style="display: none;">image</a>
<a href="image3.jpg" data-mini-modal="group1" style="display: none;">image</a>
```
