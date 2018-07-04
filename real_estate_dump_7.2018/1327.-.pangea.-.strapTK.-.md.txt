# Strap'd ToolKit

Strap'd ToolKit is a JavaScript framework for building sites with Bootstrap.  It handles construction and insertion of HTML as well as providing some easy methods of using Bootstrap's built-in element styling for typed elements (like buttons).  In the future, it will provide a means to automatically update a Source based on its data.

StrapTK has found its best uses in dynamic web applications and is very well suited to that environment.  It won't replace static HTML in your apps, but it will suppliment and empower dynamic applications.

## Using StrapTK
### Requirements
In order to use StrapTK, you'll need a few other libraries.
* [Twitter Bootstrap](http://twitter.github.com/bootstrap/index.html) - While Strap'd doesn't directly interact with Bootstrap, it was built entirely for working with Bootstrap.
* [FontAwesome](https://github.com/FortAwesome/Font-Awesome) - For additional icons.  FontAwesome can be omitted at the expense of a number of icons provided by the Icon class.
* [jQuery](http://jquery.com/) - If you're not already using jQuery, I strongly recommend it.
* [Lo-Dash](http://lodash.com/) - This _can_ be substituted for Underscore, but you will encounter a errors when Lo-Dash's chaining syntax is used.

Once you have all those, you're ready to use Strap'd.

### Coding it up
Strap'd was designed for use by JavaScript developers that are sick of writing HTML (like me).  Strap'd requires some very minimal boilerplate to get set up and you can be up and running with a site using Strap'd in minutes.  <small>If you're a fan of Ruby, you'll find some handy HAML compilation code in the Rakefile that will trim your boilerplate down even farther!</small>

So, let's write some code!  We'll start with a simple example:
````javascript
new P("Look!  A paragraph with some text in it!");

// Renders to <p>Look! A paragraph with some text in it!</p>
````
It can be that simple.

Strap'd supports nesting via the ````children```` attribute.  Allowing you to make more complex objects and markup.
````javascript
new Panel({
  classes: "well",
  children: [
    new Header("Look here!"),
    new P("We could nest this further, but who wants to read that?")
  ]
});

/*  Renders to:
 *    <div class='well'>
 *      <h1>Look here!</h1>
 *      <p>We could nest this further but who wants to read that?</p>
 *    </div>
 */
````

This isn't the only way to define the children of an element, just the most likely use case.  Most components (those being the ones that extend Component), also allow you to pass an array instead of an object in the constructor.  For example, if, in the last example, we hadn't wanted our panel to have the class "well", we could have written it as:
````javascript
new Panel([
  new Header("Look here!"),
  new P("We could nest this further, but who wants to read that?")
])
````
And you would have gotten just that.  A div with some children.

That's all well and good, but you may have noticed that the last examples had a bit more code to it than the resulting markup and didn't really make it that much easier to write.  Which is true, Strap'd isn't meant to make creating HTML shorter, per se, just easier to manage.  A good example of something with complex markup is Bootstrap's Carousel.
````javascript
new Carousel({
  id: "carousel",
  children: [
    new Img("http://placehold.it/350x150&text=Placeholder+Image"),
    new Img("http://placehold.it/350x150&text=Placeholder+Image"),
    new Img("http://placehold.it/350x150&text=Placeholder+Image"),
    new Img("http://placehold.it/350x150&text=Placeholder+Image")
  ]
});

/* Renders to:
 *  <div id='carousel' class='carousel slide'>
 *    <ol class='carousel-indicators'>
 *      <li data-slide-to='0' data-target='#carousel' classes='active'></li>
 *      <li data-slide-to='1' data-target='#carousel' ></li>
 *      <li data-slide-to='2' data-target='#carousel' ></li>
 *      <li data-slide-to='3' data-target='#carousel' ></li>
 *    </ol>
 *    <div class='carousel-inner'>
 *      <img src='http://placehold.it/350x150&text=Placeholder+Image' class='item active' />
 *      <img src='http://placehold.it/350x150&text=Placeholder+Image' class='item' />
 *      <img src='http://placehold.it/350x150&text=Placeholder+Image' class='item' />
 *      <img src='http://placehold.it/350x150&text=Placeholder+Image' class='item' />
 *    </div>
 *    <a class='carousel-control left' data-slide='prev' href='#carousel'>&lsaquo;</a>
 *    <a class='carousel-control right' data-slide='next' href='#carousel'>&rsaquo;</a>
 *  </div>
 */
````

So, we have examples of use and why it might be better, but lets really delve into something cool.  Lets say you have a form.  With Bootstrap, there is some markup you should use to make your forms look as pretty as possible.  However, you'll end up writing the same bits of code over and over.  This lack of DRY-ness is the bane of most developers existance, but is easily remedied in Strap'd.  Because we're using JavaScript, we can leverage all the awesomeness that it provides.  How about an example!
````javascript
function inputControl(options) {
  var label = options.label; // label isn't used by StrapTK's FormInput element, so we can leave it in

  return new Panel({
    classes: "control-group",
    children: [
      new Panel({
        classes: "control-label",
        body: label;
      }),
      new Panel({
        classes: "controls",
        children: [
          new FormInput(options);
        ]
      })
    ]
  });
}

new Form({
  id: "login-form",
  action: "/login",
  method: "POST",
  children: [
    inputControl({
      label: "Username",
      type: "text",
      name: "username"
    }),
    inputControl({
      label: "Password",
      type: "password",
      name: "password"
    })
  ]
})

/* Which would render to:
 *
 *  <form id='login-form' action='/login' method='POST'>
 *    <div class='control-group'>
 *      <div class='control-label'>Username</div>
 *      <div class='controls'>
 *        <input type='text' class='input input-text' name='username' />
 *      </div>
 *    </div>
 *    <div class='control-group'>
 *      <div class='control-label'>Password</div>
 *      <div class='controls'>
 *        <input type='password' class='input input-password' name='password' />
 *      </div>
 *    </div>
 *  </form>
 */
````
This example is, in my opinion, still a little contrived.  It doesn't really show you how powerful what you've made is.  Imagine, if you will, you needed 8 forms like this.  Now, you can just write a function that builds them and outputs them whenever you need with whatever setup you need.  The only limit is your skill in the language.

To use an example from my own codebase, I have a function that generates list items for a Dropdown Menu:
````javascript

function neighborhoodDropdownItem(val) {
  return  new Link([
            new FormLabel({
              body: val,
              children: [
                new FormInput({
                  type: "checkbox",
                  name: "locations[]",
                  value: val,
                  classes: "pull-left"
                })
              ]
            })
          ]);
}
````

Given a list of neighborhoods, I could easily make a DropdownMenu from them like so:

````javascript
new DropdownMenu({
  id: "neighborhood-dropdown",
  children: _.map(neighborhoods, function(nbh) {
    return neighborhoodDropdownItem(nbh);
  });
})
````
Assuming a neighborhood menu of sufficent size, this could save you a lot of trouble!

Obviously, this is just the tip of the iceburg of what you can really do with StrapTK.  More advanced topics are still in the works and even I haven't really found the 'optimal' use for the library.  It's still very young and trying to find it's place, but, with your help, it might just get there.


## Attributions
* [Pangea Real Estate](http://www.pangeare.com) for letting me work on Strap'd on their dime and providing an all around great place to work.
* [Bryan Zettler](https://github.com/BryIsAZombie) for his work on the original HAML/HTML templates used to create the Lo-Dash templates.
* [Chris Rankin](https://github.com/rankin) for the original idea and kicking my ass into actually doing it.
* [The jQuery team](http://jquery.com/) for making, arguably, the best DOM manipulation library ever.
* [The Lo-Dash team](http://lodash.com/) for their work on a nice API for manipulating JavaScript objects in a way that makes sense.
* [The Bootstrap team](http://twitter.github.com/bootstrap/index.html) for building an awesome framework to build on.
* [The FontAwesome team](https://github.com/FortAwesome/Font-Awesome) for making a damn cool icon pack that just works.
* [The Backbone team](http://backbonejs.org/) for being way smarter than I am and writing a pretty damn perfect <code>extend</code> function
* [Me (Chris Hall)](https://github.com/chall8908) for getting shit done.

Speaking of attributions to myself, if you're using Strap'd, let me know!  I'd love to hear from you.  While you're letting me know, you should let everyone ELSE know too.  A little blurb somewhere out of the way is all I ask.  If you're feeling especially generous, a link back here would be awesome!

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Strap'd ToolKit</span> by <span xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName">Pangea Real Estate</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.
