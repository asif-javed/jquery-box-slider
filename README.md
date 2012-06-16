jQuery 3D content slider
===

This jQuery plugin is a light-weight content slider that provides a simple
interface for creating cool 2D or 3D slide animation transitions. It comes, by
default, with a 3D vertical scrolling box transition and I intend to create
more cool effects as I find time.

Not officially released yet but browse index.html for demos.

Support
---

Currently, I've only added 3D support for webkit and Firefox, all other browsers
will fallback gracefully to a simple fade transition.

Usage
---

Create a view port for the 3D perspective and within that add the HTML to create
a box containing slides of content.

```html
<div class="slider-viewport"><!-- works as a viewport for the 3D transitions -->
  <div id="content-box"><!-- the 3d box -->
    <figure>
      <img src="img/slide-1.png">
      <figcaption>This is slide one's description</figcaption>
    </figure>
    <figure>
      <img src="img/slide-2.png">
      <figcaption>This is slide two's description</figcaption>
    </figure>
    <figure>
      <img src="img/slide-3.png">
      <figcaption>This is slide three's description</figcaption>
    </figure>
    <figure class="slide">
      <img src="img/slide-4.png">
      <figcaption>This is slide four's description</figcaption>
    </figure>
  </div>
</div>
```

Technically no CSS is required but if the outer box `div.slider-viewport` is
statically positioned the plugin will apply relative positioning to it so that
it can hold the absolutely positioned box. Always a good idea to constrain the 
size of the viewport so that the slides don't spew down the page at load time.

```css
.slider-viewport { width: 560px; height: 380px; overflow: hidden }
```

Then on page load the usual jQuery sugaryness applies...

```javascript
$('#content-box').boxSlider( /* options */ );
```

Options
---

* `speed (default: 800)` The time interval in milliseconds within which the
  slide animation will complete
* `autoscroll (default: false)` Set true to automatically transition through
  the slides
* `timeout (default: 5000)` The time interval between slide transitions. For use
  with autoscroll
* `pause (default: null)` A DOM element, jQuery object or selector for an element
  that when clicked will toggle the autoscoll state of the slider. When the slider
  is in a paused state the element will be applied a class name of paused
* `pauseOnHover (default: false)` Pause an auto-scrolling slider when the users
  mouse hovers over it. For use with autoscroll
* `next (default: null)` A DOM element, jQuery object or selector for an element
  that when clicked will advance the slider to the next slide
* `prev (default: null)` A DOM element, jQuery object or selector for an element
  that when clicked will advance the slider to the previous slide
* `effect (default: 'scrollVert3d')` The slide animation effect to use when
  scrolling through content slides
* `perspective (default: 1000)` The 3D perspective at which the content slides
  are placed from the view port during transition

Methods
---

### `showSlide`

Shows a slide at the specified index starting from 0

```javascript
$('#content-box').boxSlider('showSlide', 3); // show 4th slide
```
### `playPause`

Start autoScrolling a slideshow or pause an already running slideshow

```javascript
$('#content-box').boxSlider('playPause');
```

### `option`

Get or set a specific option

```javascript
$('#content-box').option('speed'); // returns speed option value
$('#content-box').option('speed', 1200); // sets the speed option to 1200
```

Events
---

### `onbefore`

Fires before each slide transition starts. The function parameter will be bound
to the jQuerified box and will receive the current slide as it's first parameter
and the next slide as its second.

```javascript
$('#content-box').option('onbefore', function ($currentSlide, $nextSlide) {
  // 'this' is effectively $('#content-box')
});
```

### `onafter`

Fires after each slide transition is complete. The function parameter will be bound
to the jQuerified box and will receive the current slide as it's first parameter
and the next slide as its second.

```javascript
$('#content-box').option('onafter', function ($currentSlide, $nextSlide) {
  // 'this' is effectively $('#content-box')
});
```
