JS-Ghost
===

JS-Ghost contains a MooTools based class and a CSS file for styling. It&#039;s
primary function is to layer labels over inputs for intuitive, real-estate
conscious input labels.

With a brute-simple instantiation, this class doesn&#039;t require much tweaking
(of which can be done entirely through an additional CSS file to maintain the
codebase).

A &quot;ghost&quot; value is retrieved, by default, from the input&#039;s title
attribute.

### Instantiation Example

``` javascript

(new Ghost($('input')));
```

Yup! That&#039;s it :)  
For a real-life example, check out
[example.html](https://github.com/onassar/JS-Ghost/blob/master/example.html).
