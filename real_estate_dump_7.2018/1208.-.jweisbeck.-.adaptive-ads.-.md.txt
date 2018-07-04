Responsive ads
===

###About this project
This is intended to be a proof-of-concept for context-aware ad serving in a responsive web site. The 'context' we're concerned with is
a set of arbitrarily defined pixel width ranges. By comparing an agent's current viewport width to a set of contexts in a configuration
object we can select the most appropriate context, yielding a list of ad positions that suite the agent's current layout and environment.

We are using 24/7 RealMedia's Open AdStream (OAS) platform for this project's use case. Check with your ad vendor's implementation for any differences.

**More about this project**

1. **Why we're doing this.** In the pursuit of building effective responsive web experiences, accommodating the needs of advertising presents a few important roadblocks,
especially for sites with outdated habits around delivering ad services. Technically, the primary challenge is adapting the kind of creative served to correspond
with layout reflows that are controlled by a fluid grid and media queries. Open AdStream uses the discredited technique of loading assets with `document.write`, a javascript
method that can flush an entire page's contents on responsive web sites.
As a result, we propose making ad services **adaptive**, which means ads are delivered to adapt to the current page's state (which we call a context). Importantly, however, they don't *respond* on
browser resize. However, delivering adapted ads is a promising way to overcome the problem of using traditional ad services on responsive web sites.
2. What are the pros and cons
	* Pros
		* Enable responsive design, or serving an experience designed to look and work well across many devices from a single codebase
		* Non-destructive: the current ad structure is preserved. However, now it becomes one among many possible contexts
		* Presents new opportunities to use traditional online sales channels to target users of other devices, rather than assuming the risks of devising new product platforms to reach them.
	* Cons
		* The definition of contexts is dependent on browser width/screen size (we avoid touch/no touch flag)
		* Requires a culture shift to serve ads in a responsive environment
		* Selling ads with additional contexts could be potentially confusing to advertisers and creative agencies
3. How it works: For marketing, sales and product
	* Internally determined number and nature of contexts, which means business goals can define the contexts rather than outside constraints
	* Use four vectors to define a context, allowing a fair amount of scheduling control on pages
		1. Sitepage 
		2. Browser width range
		3. Context variable passed back to OAS for additional decision-making, probably informing the kind of creative used
		4. UA sniffing by OAS
	* OAS list positions are grouped by context. Organizations are responsible for determining the mapping of ad positions to a context, which includes a 'default' context that represents the most enhanced, or widest, layout experience.

4. How it works: Technical definitions
	* **Overview** - First, when the page begins loading, an agent's size is compared to a pre-defined default context. By 'default' we mean the widest breakpoint declared in the configuration object `ctx`. We realize that by declaring the widest context a default we aren't strictly abiding by the principle of mobile-first design. We are setting aside this question in early iterations of this project and we hope to address it soon. The comparison of browser `clientWidth` to the default context determines if we will use `clientWidth` or the device's lesser dimension as the final context measurement. The measurement works for the widest range of screen sizes, but doesn't attenuate the experience on desktops when browsers aren't maximized. Last, the `ctx` object is looped through and compared to the calculated screen size value. When a matching context is selected, it uses a property called `positions` to determine which group of OAS ad positions should be applied. The grouping of positions by context is an arbitrary determination driven by business goals. The page then continues to parse and OAS uses the context to set up and render those ad positions.
		* It is important to note that this solution does not reflow ads upon javascript's `resize` event or by media queries. This solution sets context once: when the page loads.
		* There is an option to hide ads should the viewport width change after the inital page load (not implemented yet).
		* **List Positions** - A master list of all the possible active positions would be stored in the page markup in a meta tag, looking something like this:
	`<meta name="oas-positions" id="oas-positions" content="HEADLINE2,ARTICLE,TOP,HEADLINE2,ARTICLE,FOOTER">`. The comma-separated list of positions would be administered on the back end.
	The page being served would acquire the list position from metadata. If no metadata existed for a particular page, acquisition logic would walk up the taxonomy and get
	list position metadata from the nearest ancestor. 
		* **Position context grouping** - The list position string in the markup is ordered to correspond to the groupings defined in each context. The grouping is positional. So,
	if the 'basic' context's positions are '2' - it will use the first two positions in the metadata list. contexts in between other contexts use the previous contexts as offsets for
	selecting the correct start position in the position string.
	* **Determining agent's context** - The following measurement is taken to determine the user agent's current available size: `screenSize = Math.min(win.screen.availWidth, win.screen.availHeight)`.
	This returns the smaller dimension of the user's available screen size. If the agent's clientWidth (the width of the viewport) is less than the default context's limit, We use the smaller dimension as a defensive move to avoid ads bleeding beyond the layout. While most users don't resize browsers on desktops, it is true that on phones and tablets, users change orientation much more frequently. This creates potential for out-of-context ads showing when a user re-orients his/her device. We use the smaller of the device's two dimensions to guard against this possibility.
	* In addition to building a contextual list of positions, this solution passes to OAS the name of the context as a query variable. This can be extremely useful in the OAS ad scheduling administration. It allows administrators to serve different creative to the same position across different contexts.

This project was inspired by a blog post written by Robert Flaherty at RavelRumba, <a href="http://www.ravelrumba.com/blog/responsive-ads-real-world-ad-server-implementation/">here</a>.

For further reading about viewports and measuring screen real estate, see <a href="http://www.quirksmode.org/mobile/viewports.html">PPK's illuminating post</a>.
