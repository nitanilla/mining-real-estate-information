

***
# Angular module to focuses into input field with error on form submission

***
## Overview

This angular module improves usability for screens with smaller real estate like mobile phones by focusing/scrolling to input field with error on form submission.

## Installation

- Using Bower : `bower install ngScrollToError`
    - Load "_**src/ng-scroll-to-error.js**_" in your index.html using script tag.
    - Include "_**ng-scroll-to-error**_" in your app's  list of module.

## Configuration and Usage

To disable at form level ,add the attribute _disable-scroll-on-submit="true"_   and to disable the auto focus feature please add the attribute _disable-focus-on-submit="true"_  on the _form_ or _ngForm_ DOM nodes in your templates.

## Gotcha
This module will work seemlessly only if all the input field validations are implemented as angular validations. If there are any explicit programatic validations, then it will not consider those fields to be input fields with errors and will not scroll to /focus onto those fields.
