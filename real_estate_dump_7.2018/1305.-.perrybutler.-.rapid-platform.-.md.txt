![Rapid Platform](http://files.glassocean.net/github/rp-banner.jpg)
==============  
  
***Note: see the [Rapid.js](http://github.com/perrybutler/rapid.js) project for a glimpse into the future of Rapid Platform.***
  
Rapid prototyping and development for WordPress sites, apps and themes. It's a plugin for WordPress built from scratch with responsive web design principles and best practices at it's core.  

Join our [Google+ community](https://plus.google.com/u/0/b/110639079393921179427/communities/108899206842693997128) or visit the [official website](http://therapidplatform.com) for more information.  

Features
--------

### Rapid UI

A robust set of UI controls and components ready to drop into a page. OAuth2.0/OpenID Login (Google/Facebook/Yahoo/MyOpenID), Lightbox Popups, Buttons, Tabs, Sliders, Google Web Fonts, Glyph Icons, etc:  

    [rp_login_form]  
    [rp_lightbox]  
    [rp_button]  
    [rp_choice type="tabs"]  
    <p style="font-family:Open Sans;">...</p>  
    <span class="icon-download">Download</span>  

![responsive ui](http://files.glassocean.net/github/rp-responsive-ui.png)

#### Rapid UI Grid

A fluid grid based on fixed percentages, with columns that automatically stack vertically for smartphones. It's one of the easiest grid systems to use; Rapid Platform can build a four column responsive grid with the following shortcodes:  

    [rp_grid count="4" span="1"]html_content_goes_here[/rp_grid]  
    [rp_grid count="4" span="1"]html_content_goes_here[/rp_grid]  
    [rp_grid count="4" span="1"]html_content_goes_here[/rp_grid]  
    [rp_grid count="4" span="1"]html_content_goes_here[/rp_grid]  
  
![rp_grid](http://files.glassocean.net/github/rp-grid.png)

Tired of seeing Framework X offering "20 layout templates" and Premium Theme Y offering "premium layout templates for $30 more"? What's the obsession with all of these hard-coded layout templates? See our home page remakes of [Twitter Bootstrap](http://therapidplatform.com/showcase/bootstrap/) or [WordPress.org](http://therapidplatform.com/showcase/wordpress-org/) to see what kind of layouts we're able to achieve **in as little as 5 minutes** with the Rapid UI Grid. By the way, our home page remakes are fully responsive by default :)

### Rapid Settings

Automatically creates entire settings pages in the WordPress admin dashboard with forms and fields tied into the database. Settings are defined in plain text:

![rapid settings a](http://therapidplatform.com/wp-content/uploads/2012/11/options1.jpg)

...instantly becomes this:

![rapid settings b](http://therapidplatform.com/wp-content/uploads/2012/11/options2.jpg)

...and when the text file changes, the forms, fields and database are automatically updated. Traditionally, you might find yourself stripping out the field elements, deleting the validation/sanitation logic for those fields, modifying the database/sql procedures that couple these fields to the database, etc.

Quickstart
----------

Rapid Platform has not yet been released to the WordPress.org Plugins Repository. Until then, plugin installation and upgrades must be performed manually.

PROCEED AT YOUR OWN RISK. If you feel uncertain, or you don't have a solid backup strategy, or you don't have a temporary site to experiment with first, this plugin might not be for you until it has undergone a rigorous review by the WordPress.org team and added to the Plugins Repository.

That said, here's how to get started:

1. Manually download and install the Rapid Platform plugin for your WordPress site
2. Active the plugin via the WordPress admin dashboard
3. That's it! Documentation and examples can be found at [TheRapidPlatform.com](http://therapidplatform.com)

### Rapid UI Quickstart

WordPress shortcodes can be used to insert Rapid UI components into any WordPress Page or Post.

Adding a button:

1. Edit a Page/Post and type this shortcode somewhere in the body: [rp_button caption="My Button" link="bing.com"]
2. Publish, then visit the Page/Post to see your new button in action
3. That's it! Documentation and examples can be found at [TheRapidPlatform.com](http://therapidplatform.com)

Adding an accordion:

1. Edit a Page/Post and type this shortcode somewhere in the body:
    [rp_accordion title="Hidden Text"]This is my hidden text.[/rp_accordion]
2. Publish, then visit the Page/Post to see your new accordion in action
3. That's it! Documentation and examples can be found at [TheRapidPlatform.com](http://therapidplatform.com)

### Rapid Settings Quickstart

The included sample config provides a quick demonstration of how to add your own custom settings to the WordPress admin backend.

Activating the sample config:

1. In the Rapid Platform plugin's root directory, rename the rapid-config-sample.php file to rapid-config.php
2. Visit the WordPress admin dashboard and the sample settings will be initialized
3. Visit the Rapid Settings menu to observe the sample settings

Feel free to modify the rapid-config.php file to create your own settings in the WordPress admin backend. You can change the rapid-config.php file(s) at any time and WordPress will initialize your changes the next time you visit the admin dashboard. The rapid-config.php file can be copied or moved into a (parent/child) theme's root directory, allowing that theme to incorporate its own independent set of options when the theme (and Rapid Platform) are activated.

Roadmap / Requested Features
----------------------------

### Component Manager

Rapid Platform is an all-in-one/multi-task plugin. It should allow the admin to turn off certain components that aren't needed to speed up load times and reduce overall bloat.

### Fully embrace markdown

* Wait for WP native support, or implement via open-source lib?
* Authors/publishers need a better workflow and editor, bottom line!!! We don't want authors/publishers having to fiddle with code. Average Joe needs a good workflow, and what could be easier than markdown?
* Authors/publishers should have the ability to mix shortcodes with markdown and this should be easy to learn because the syntax is similar. Through the use of a plain text editor, authors/publishers would have the ability to design highly advanced "application-like" functionality without digging into php templates or javascript code.
* A markdown + shortcode editor with drag/drop enhancements would be far more ideal than the hybrid TinyMCE editor currently in WordPress.
* The editor in WordPress is clunky. The Visual tab in the editor is not very visual because you only see a very basic hard-wrapped preview of your content rather than the real thing. The HTML tab in the editor is not very HTML because your elements will get re-parsed (and sometimes mangled) by WP/TinyMCE if you switch back to the Visual tab. It's just not cool when your HTML elements disappear.
* The Ghost blogging platform takes a similar approach to what we're hoping to achieve. Let's take it a few steps further and combine the real-time capabilities of Ghost's markdown with shortcodes and LESS!
* The "new" markdown + shortcode editor would replace instances of the TinyMCE editor throughout WordPress. This puts us in line with one of our other roadmap features: Rapid Edit.

### Rapid Edit

**Live editing is currently being developed in a side project I'm working on and will find its way into Rapid Platform once the first generation of live editing has matured. It's like a fancy HTML5 WYSIWYG (InnovaStudios, Aloha, Unify) without all the clutter and fuss.**

* Authors/editors (when given permission through the backend) should have the ability to view the website in their browser and make live edits to the content using specially tagged regions.
* It should work like this: An author/editor notices a typo in the Title of a Blog Post, so he turns on Edit Mode which creates an overlay on top of the live website, highlighing those specially tagged regions. From this point the author/editor can click on any of the highlighted regions to make a live edit, so he clicks the Title region and a textbox appears where he can change the Title of the Blog Post. After changing the Title, he clicks OK to view the change, and we store all changes in a "dirty-state" object. Finally, the author/editor can commit his changes which pushes the "dirty-state" object through a formatter/sanitizer, making any needed updates to the matching content in the database.

### Niche features and components

Without revealing too much about the unsaid future, there are currently plans to incorporate features specific to Real Estate, eCommerce/eStore, eSports, Digital Advertising, etc, some of which may become core components and others being  released as niche themes "built with Rapid Platform", depending upon the nature of the market and community. We hope that Rapid Platform will continue evolving towards a lean, full-featured, cross-platform, write-once run-anywhere site/app/prototype development toolkit.

More neat stuff goes here.
