# Fliparoo Read Me File

## Warning

**THIS IS STILL ALPHA AND BROKEN. A RELEASE VERSION WILL BE COMING SOON. BUT DO NOT USE UNTIL THEN.**

## Overview

Fliparoo is a jQuery plugin which is like Vanna White for your web page.

![A flipping alternative to carousels](wheel-of-fortune.jpg)

This script is intended to swap out items in a "display" list with those in a "queue" list. The most obvious use is for a strip of images which swap out from a larger list.

This is meant to be an alternative to a carousel - a little more ambient with less user interaction.

It is probably best understood by looking at the **[demo page](http://lullabot.github.io/fliparoo/)**.

*Created by Jeff Robbins with [Lullabot](http://www.lullabot.com).*

## Code examples: 

    $('#mylist li').fliparoo();
    $('#mylist li').fliparoo({displayCount: 5});
    $('ul.display li').fliparoo($('ul.queue li'));
    $('ul.display li').fliparoo($('ul.queue li'), {
      delay: 1000,
      transTime: 1000, 
      randomize: true
    });  

Requires Rico Sta Cruz' [jQuery Transit plugin](http://ricostacruz.com/jquery.transit/)

## Why Fliparoo Is Better Than Carousels and Sliders
For anyone who has tried to implement a carousel or slider on a responsive website, you know that it can be frustrating. These complex animations and interactions often don't resize or re-adapt easily to different display sizes. Although they can look great on desktop browsers, the fact that they become one big "blob" limits options for a responsive design. 

Fliparoo does not create a blob like most carousel libraries. Instead, it identifies "display" elements which flip around to display other elements. These elements don't get blobbed together. They don't slide around on the page. They don't get a lot of esoteric CSS applied to them to hold the blob together. They can be styled and adapted however you like. A horizontal list can become vertical, elements can resize as a percentage of the width of their parent, and you can do all of that good responsive mojo. It is even possible to define non-contiguous display elements, such as splitting display elements above and below a non-swapping element or even (gasp!) table cells in different rows of a table.

Many times the purpose of a carousel is to showcase work or display a gallery of photos. It's basically a way to display more elements on the page without taking up a lot of real estate and weighing down the design. While I probably wouldn't recommend Fliparoo for the large front-and-center [hero](http://en.wikipedia.org/wiki/Hero_graphic) display where many designers use carousels, it can certainly replace carousels and sliders for more atmospheric uses showcasing longer lists of similarly-weighted items like sponsor logos or photo galleries. 

See also:

* http://weedygarden.net/2013/01/carousel-stats/
* http://bradfrostweb.com/blog/post/carousels/
* http://blog.bearded.com/post/41445520202/slide-rules
* http://krogsgard.com/2013/sliders-suck/
* http://www.nngroup.com/articles/auto-forwarding/
* http://insideintercom.io/why-cards-are-the-future-of-the-web/

## Advantages of Fliparoo

* Smooth CSS3 animations
* Infinitely style-able and responsive-design friendly
* Fallback to non-animated swapping for non-CSS3-savvy browsers

## Limitations of Fliparoo

* Not (currently) interactive
* Elements need to be the same height/width

## Usage Notes
Fliparoo should be pointed at container elements representing the display and queue list. Most web developers will use a `<ul>` or `<ol>` list for this purpose. The children of these elements are used as the list items for display and queue. Since it is invalid to add elements between the `<ul>` and `<li>` items, Fliparoo creates a `<div>` element inside of each display `<li>` and effectively moves the content of the `<li>` into the `<div>`. Example:

    <ul>
      <li>one</li>
      <li>two</li>
      <li>three</li>
      <li>four</li>
    </ul>
    
after processing, becomes:

    <ul>
      <li class="fliparoo-display-container">
        <div class="fliparoo-display fliparoo-front">one</div>
        <div class="fliparoo-display fliparoo-back">five</div>
      </li>
      <li class="fliparoo-display-container">
        <div class="fliparoo-display fliparoo-front">two</div>
        <div class="fliparoo-display fliparoo-back">six</div>
      </li>
      <li class="fliparoo-display-container">
        <div class="fliparoo-display fliparoo-front">three</div>
        <div class="fliparoo-display fliparoo-back">seven</div>
      </li>
      <li class="fliparoo-display-container">
        <div class="fliparoo-display fliparoo-front">four</div>
        <div class="fliparoo-display fliparoo-back">eight</div>
      </li>
    </ul>
    
Note the addition of classes and `<div>`s surrounding content.

The `<li>` "container" items are the items which use 3D transforms to flip. The front/back divs flip with their parent. However, note that the `<li>` items should not have a background color on them or they will obscure the child elements when flipped. Instead add styling to the "fliparoo-display" items. Also, `overflow:hidden` on the li items will be problematic. Again, apply it to the nested divs.

Also note that the display items need to be a type of html element which can accept sub-elements. Above, each `<li>` gets `<div>` elements inserted into it. For instance, a collection of `<img>` elements wouldn't work because you can't nest another element inside an image.

### Single vs. Double Lists
Fliparoo works with either two lists or just one. In the case of two lists, one list is the "display" list and the other is the "queue". This allows the queue list to be hidden with CSS so if Javascript is disabled and Fliparoo doesn't do anything, only a few of the list items will be displayed. This also solves the FOUC (flash of unstyled content) problem which can happen briefly during the page load. 

It is also possible to use a single list and define the number of items to display using the `displayCount` parameter. Although this is an easier method for most web developers, keep in mind that if Javascript is disabled, all list items will be diplayed. Please allow for this in your CSS styling.

Note that these 'lists' don't actually need to be `<li>` lists. You could also use `<div>`s or whatever html meets your needs.

## Options

You can find these at the bottom of the `jquery.fliparoo.js` file:

```javascript
    delay: 2000,
    // milliseconds between flips
    
    transTime: 1000,
    // transition time of each flip in milliseconds
    
    easing: 'cubic-bezier(.44,-0.23,.51,1.44)',
    // easing of flip animation
    // options from http://ricostacruz.com/jquery.transit/
    // I recommend http://cubic-bezier.com/
    
    setDelay: 0,
    // delay between iterations through the display set
    // This is an additional delay added after all items in display set have been flipped
    
    randomize: false,
    // true = Randomize items to be displayed.
    // false = Go through display and queue in order.
    
    displayCount: 4,
    // when using a single list, how many items should be displayed?
    // the remainder will be hidden
    // 0 = all (hide none)
    
    displayOrder: 'random',
    // options: 'random', 'forward', 'reverse'
    // how should the repeating pattern of display order be chosen?
    
    perspective: '500px',
    // Depth of perspective. Lower values give a more pronounced effect.
    
    rotateAxis: 'Y',
    // options: 'X', 'Y', 'XY', 'XZ', 'YZ, or 'XYZ'
    // rotate along X, Y, or all axes
    // simple X or Y work best - others are buggy
        
    rotateDirection: '+',
    // options: '+', or '-'
    // rotate forward or back
    
    flipFlop: false,
    // if true, rotationDirection will alternate with each flip
    
    transit: {},
    // Additional Transit properties. See http://ricostacruz.com/jquery.transit/
```

## Performance
Fliparoo uses the Transit plugin, which applies CSS3 transition animations to the display elements. Most web browsers will engage hardware acceleration for CSS3 animations, making them much more efficient than Javascript-based or even Flash-based animations. However, these animations can still be processor intensive, especially when many different animations are happening simultaneously on the same page. Test in a variety of browsers on a variety of operating systems and processors before deploying. You've been warned.

## Fallback
Older browsers without support for 3D transformations will simply get no animations. 

## Legal Stuff
Fliparoo is copyright &copy;2013 by [Lullabot](http://www.lullabot.com) and licensed under the [MIT License](http://opensource.org/licenses/MIT) without waranty or guarantees of any kind.

