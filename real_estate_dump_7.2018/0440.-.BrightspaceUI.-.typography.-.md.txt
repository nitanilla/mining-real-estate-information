# d2l-typography
[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/BrightspaceUI/typography)
[![Bower version][bower-image]][bower-url]
[![Build status][ci-image]][ci-url]

A set of [Polymer](https://www.polymer-project.org/1.0/) and [Sass](http://sass-lang.com/) mixins for applying D2L typography.

For further information on this and other Brightspace UI components, see the docs at [ui.developers.brightspace.com](http://ui.developers.brightspace.com).

## Installation

`d2l-typography` can be installed from [Bower][bower-url]:
```shell
bower install d2l-typography
```

## Typography Styles

The following typography styles are available for use in your application:

### Standard Body

"Standard Body" can be used to apply base font properties, but will also respond to viewport width changes.

![screenshot of standard text](/screenshots/standard.png?raw=true)

### Compact Body

Compact body is a smaller version of the standard body style, for use in areas that prefer to be conservative with the amount of real estate used by text.

![screenshot of compact text](/screenshots/compact.png?raw=true)

The compact style is not recommended for blocks of readable text, particularly in paragraph form. Rather, it is best employed for brief informative text or calls to action.

### Small Body

Never used by itself; always in support of another piece of content on the page. Used for inline assistive text in forms, and for specifying metadata or properties of an existing piece of content.

![screenshot of small text](/screenshots/small.png?raw=true)

### Label Text

Used for labels. Its font size/line spacing is relative to the root font
and respond to viewport width changes.

![screenshot of small text](/screenshots/label.png?raw=true)

### Headings

There are four available heading styles. These would typically be applied to the `<h1>`, `<h2>`, `<h3>` and `<h4>` HTML elements, though it's not a requirement.

![screenshot of headings](/screenshots/headings.png?raw=true)

## Usage

Typography fonts and styles can be applied using either [Polymer](https://www.polymer-project.org/1.0/) or [Sass](http://sass-lang.com/) mixins. Which one you use depends on your technology stack and comfort with each, however since Sass compiles to native CSS it's more performant.

### Sass

Import the main `d2l-typography.scss` file into your application's Sass. Then call the `d2l-typography-font-face()` mixin to define the web fonts and apply the `d2l-typography()` mixin to your `<body>` element:

```sass
@import 'bower_components/d2l-typography/d2l-typography.scss';

@include d2l-typography-font-face();

body {
	@include d2l-typography();
}
```

Mixins are also available for standard body, compact body, small body and heading styles:

```sass
.standard {
	@include d2l-body-standard();
}

.compact {
	@include d2l-body-compact();
}

.small {
	@include d2l-body-small();
}

.label {
	@include d2l-label-text();
}

h1 {
	@include d2l-heading-1();
}
h2 {
	@include d2l-heading-2();
}
h3 {
	@include d2l-heading-3();
}
h4 {
	@include d2l-heading-4();
}
```

### Polymer

Include the [webcomponents.js](http://webcomponents.org/polyfills/) "lite" polyfill (for browsers who don't natively support web components), import `d2l-typography.html`, and include `d2l-typography` in a custom style block:

```html
<head>
	<script src="../webcomponentsjs/webcomponents-lite.js"></script>
	<link rel="import" href="../d2l-typography/d2l-typography.html">
	<custom-style include="d2l-typography">
		<style is="custom-style" include="d2l-typography"></style>
	</custom-style>
</head>
```

The `d2l-typography` class can be used to set base font properties, typically applied to the `<body>` element.

```html
<body class="d2l-typography">
	...
</body>
```

Additional CSS classes are available for standard body, compact body, small body and headings:

```html
<!-- standard body -->
<div class="d2l-body-standard">
	...
</div>
<!-- small body -->
<div class="d2l-body-small">
	...
</div>
<!-- label text -->
<label class="d2l-label-text">Lorem Ipsum</label>

<!-- compact body -->
<div class="d2l-body-compact">
	...
</div>
<!-- headings -->
<h1 class="d2l-heading-1">...</h1>
<h2 class="d2l-heading-2">...</h2>
<h3 class="d2l-heading-3">...</h3>
<h4 class="d2l-heading-4">...</h4>
```

### Responsive Breakpoint

The fonts for headings, standard body, and compact body will all be styled to be smaller at a responsive breakpoint, defined as when the viewport width is 615px or smaller.

### Note About Font Size

Normally within Brightspace, the user-configured base font size will automatically be present, and requires no additional work to opt-in. However, if your application exists outside of Brightspace, you should set your desired font size on the `<html>` element. The default recommended size is `20px`:

```css
html {
    font-size: 20px;
}
```

## Coding styles

See the [Best Practices & Style Guide](https://github.com/Brightspace/valence-ui-docs/wiki/Best-Practices-&-Style-Guide) for information on naming conventions, plus information about the [EditorConfig](http://editorconfig.org) rules used in this repo.

[bower-url]: http://bower.io/search/?q=d2l-typography
[bower-image]: https://badge.fury.io/bo/d2l-typography.svg
[ci-url]: https://travis-ci.org/BrightspaceUI/typography
[ci-image]: https://img.shields.io/travis-ci/BrightspaceUI/typography.svg
