# AEA Denver Notes (December 11th-13th)

These are notes for all the sessions I attended at AEA Denver. The last session's (extensive!) notes were taken by [Marya](https://twitter.com/emdot)!

If you see typos or errors, feel free to put in a PR!

## 11 DECEMBER

### From Research to Redesign: An Unexpected Journey
#### [Jeffrey Zeldman](https://twitter.com/zeldman)

- "There's always something the web site can do for your customers."
- Design is not about chasing trends, but engaging with the customer.
- Research is good for giving you a plan down the road.
- Pixel-perfect should never have been our goal, and it shouldn't be now.
- Better to spend a few weeks figuring out what you need to make rather than losing years building the wrong thing.
- Research exposes blind spots and biases by involving outside perspectives.
- Long tail conversion: Small commitments begetting larger commitments.
- Don't ask for too much information. Good UX == low friction.
- If you need to ask for information, tell the user _why_ you're asking for it.
- Every website needs to answer the question "What's the call to action? What are users here for?"
- An embarrassment of riches without research is useless.
- "Where's the fold?" "The CEO's laptop!"
- Let customers know whether they're anticipating customer needs accurately.
- Stakeholder interviews reveal knowledge and build consensus.

### Digital Marketing Strategies for the Busy "Web Master"
#### [Sarah Parmenter](https://twitter.com/sazzy)

- We are still in the first 10,000 days of the web.
- We are still in the first 3,000 days of social media.
- 33% of jobs don't exist right now that will in 2020.
- We're not asking what we can do for people, we're saying "look at what I've got!"
- Are we chasing vanity metrics? (e.g., 20,000 more followers, posts per day, et cetera.) Case in point: Hit counters!
- We have to check out our personal bias in social networks.
- Check up and coming social media apps, and market early to those audiences.
- Video is the fastest way to build engagement.
- Use HTTPS.
- Mobile ready and performance.
- Starting January 10th: Google is going to penalize sites that have popovers.
- How do we bring people back? Discount codes on the spot, perchance?
- Marketers who use video grow revenue 49% faster than those that don't.
- Most video content is viewed on mobile, and the vast majority watch it without sound.
- To caption video easily: SRT Edit Pro-Make and Edit in the Mac App Store.
- Posts with hashtags performance ~12% better than those without.
- Most people will put their trust into peer recommendations rather than advertising.
- Free trial for https://lefty.io for influencers.
- Some networks don't make sense for every business.

### Obvious Always Wins
#### [Luke Wroblewski](https://twitter.com/lukew)

- Some design changes seem obvious in retrospect, but aren't so obvious at the time.
- Apple's Maps app's small iterative changes took time, research.
- Don't overwhelm new users with tons of features. Build sensible, usable interaction paths.
- Get close to the customer, and find out how they use the product.
- You can't listen to what people tell you, you have to get the whole story: You should _see_ people using products.
- Qualitative metrics are very different from quantitative metrics.
- Conduct survival analysis: 1) What did users do? 2) What of those actions correlated with them being around later? (surviving)
- Look for design "band-aids", i.e., unintuitive design features.
- Have confidence in the decisions you're making. Have the courage to experiment.
- "I cannot give you the formula for success, but I can give you the formula for failure - which is: Try to please everybody."
- Not "Data-driven decisions", but rather "Data-_informed_ decisions".

### Choose Your Animation Adventure
#### [Val Head](https://twitter.com/vlh)

- CSS is best for animations that have well defined state transitions. Loading/looping, interaction animations, loading states/repeating.
- CSS pros:
  - No external library.
  - Good performance without much effort.
  - Keyframes are reusable.
  - Adjust properties in media queries easily.
- CSS cons:
  - Access to a limited set of events.
  - You have to define animations entirely ahead of time.
  - You can't separate transform properties (currently).
- CSS + JS = 🙌
  - Helps to orchestrate transitions and animations.
- Rules of thumb for moving past CSS to JS:
  - Chaining more than three animations together.
  - If the animation needs to change dynamically at runtime.
  - Need to animate transform properties separately.
  - Physics or other complex structures are required.
- JS is great at:
  - More complex animated interactions.
  - Narrative or immersive animation.
  - Dynamic state transitions.
  - Great for drag and drop interactions.
- Vanilla JS or a Library?
  - Vanilla: requestAnimationFrame
  - A Library: Makes vanilla animations much more manageable.
  - Libraries:
    - GSAP (29 KB) IE8+, SVG, morphSVG, Draggable, $$
    - Velocity (14.4 KB) IE8+, Drop-in for jQuery, MIT/Free
    - Anime (4.7 KB) IE10+, Very lightweight, MIT/Free
- SVG is good at
  - Animated illustrations/icons/logos
  - Animated infographics and data visualization
  - Fluidly scaling, responsive animation
  - Mushy/malleable stuff!
- SVG can be animated in three ways:
  - SMIL (on the outs)
  - CSS
  - JS
- Performance
  - Render flow: Style -> Layout -> Paint -> Composite
  - csstriggers.com (determines how each property hits the render pipeline).
  - Paint flashing in Chrome can reveal non-performant animations.
  - Firefox will tell you if certain animations are/are not hardware accelerated.
  - CSS isn't impacted by the main thread.
  - JS is imperative, and only aware of the current frame.
  - Hardware acceleration isn't a given with JS.
  - SVG is not hardware accelerated.

### Graduating to Grid
#### Rachel Andrew

- Grid is shipped in all major production browsers (~75-80% global support).
- CSS fundamentals: Cascade and Inheritance on MDN.
- You're faking a grid when you use floats and flexbox.
- `max-content`/`min-content` properties upcoming for dictating element size based on content.
- Flexbox is starting from `max-content` and taking space away. Grid starts at `min-content` and adding space.
- `fit-content` puts limits on `max-content`.
- `minmax` means you can specify a minimum and maximum. `auto` for maximums restricts track size.
- Everyone wants everything to be simple, but incredibly powerful. Grid is complex, but is highly capable. And you don't need to learn all of it at once, but rather incrementally.
- Names can be designated for grid tracks in the `grid` declaration in bracket notation e.g., `[content-start]`.
- `grid-area` is a shorthand for four other properties.
- Old CSS in your project doesn't stop you from using the shiny and new. You can take baby steps into using the new stuff.
- Don't forget that the older stuff has its uses.
- Off-the-shelf frameworks are designed to solve _generic_ problems.
- Come up with layout utilities that solve _your_ problems.
- Many browsers without support for grid are mobile browsers, often used by countries with poor infrastructure.
- Stop looking for polyfills and shims. Don't push JS on low-end devices in emerging markets.
- Use a feature query (`@supports`) to ask if the browser supports a feature before using it.
- Don't create cools things just for rich people. Make the web available to everyone.

### Designing with Grid
#### Jen Simmons

- Our medium is not done. Layout on the web is _evolving_.
- A lot of layout on the web is very symmetrical and predictable. It keeps happening that way because we download some framework that prescribes layouts for us.
- Design layout palettes in addition to other design elements (e.g., color and typography palettes).
- We're leaving the age of framework layouts in the next few years.
- Grid won't kill other stuff like flexbox and floats. We're going to keep using them when we need them.
- Explicit vs. implict layout in grid.
- Explicit: Defining the number of columns/Place items specifically.
- Implicit: Leaving it up to the browser
- Grid: We have ROWS, something we haven't had in CSS.
- Tracks don't have to all be the same size.
- Content can be sized by the size of a track, _and_ vice versa.
- We can mix and match units for grid track sizes.
- You can use grid to line things up. Or not.
- Great book: Graphic Design the New Basics.
- Asymmetry is really rare and effective on the web.
- Overlap: We see it all the time in print media. Grid makes it way easier to overlap elements.
- Firefox Nightly has a bunch of awesome new tools!
- The viewport: We can build complex stuff that is unveiled as the viewport reveals it. It's a long, skinny (or wide) vertical space.
- Storyboards: We can design parts of the page, and storyboard what the viewport will reveal as the user scrolls.
- We have the tools to design for all four edges of the screen, not just the top and left edges.
- Framing: Is there a language specific to the web that helps us talk about how we frame layouts?
- We can leave space in our layouts! The most important tool of layout management is _white space_.
- Verticality: We're going to be able to accommodate vertical layouts, especially useful for cultures with languages that lay out text vertically. What _does_ it mean to design in a vertical space?
- The web is a bunch of boxes in vertical spaces.
- `fr` unit = fraction. `fr`s are great for letting CSS decide what to do with the space that remains in a given track.
- `minmax` can be used to establish layouts that will size tracks to minimum and maximum bounds with _any_ kind of units (`ch` driven tracks, anyone?).
- "Pixel perfect" is out the window.
- We are programming the flexibility model.
- Creativity: Grid allows us to be creative and break away from boring frameworks that prescribe layouts.
- Time to play. Time to learn.

---

## 12 DECEMBER

### Prototyping: The Scientific Method of Business
#### [Daniel Burka](https://twitter.com/dburka)

- "What keeps you up at night?" - A good question to ask other people in your business org.
- Designers are not working on solving internal issues (e.g., procurement, hiring). Where is design really effective?
- Design done right can be the scientific method for business.
- "Inklings": Rough-edged ideas that are not well formed, things that we argue about in meetings.
- How do we test hypotheses? We argue about them, and guessing about what customers want.
- Test several ideas and measure them, we'll at least get directional feedback on what ideas hold merit.
- Basement lab: Help your team see their own inklings.
- If a picture is worth a thousand words, a prototype is worth a thousand meetings.
- All you need is you to get started in the basement lab.
- Start prototyping, and when you have a prototype, bring it back to the meeting. It's something you can _show_ people.
- Prototypes are throwaway interfaces. They're a starting point, or something to invalidate what you once _thought_ was a good idea.
- High school science lab: Prototyping level 2, instead now you test with real customers.
- Industrial grade science lab: Prototyping level 3, a master class is creating a prototype with intention as a group.
- Day 1: Gather a sprint team, create time pressure, find the right challenge.
- Day 2: Find more than one solution. No group brainstorms: Group brainstorms are resolved by the loudest voice in the group.
- Day 3: Make good, quick decisions. No design-by-committee. Entertain risky ideas.
- Day 4: Prototype.
- Day 5: Research.
- Gather the right team, create time pressure, and conduct quick, credible research.
- Step by step instructions: http://gv.com/sprint

### Story First: Crafting Products That Engage
#### [Donna Lichaw](https://twitter.com/dlichaw)

- If you want to engage your audience, you have to have an engaging story.
- Story 101: Beginning, middle, end. This timeline has a narrative arc, dotted with plot points.
- Exposition: The beginning, where the main players are introduced. Possibly foreshadowing of something on the horizon (the problem).
- Rising action: Things get exciting, working toward a climax.
- Crisis: The point of no return. Will the crisis be averted?
- The Climax/Resolution: Crisis has been averted. The problem has been solved.
- The Denouement: Calming down, and everything is normal. The main players have grown and developed. Or a chance to continue the story (a serial narrative).
- The same narrative parsing we use to understand movies/series is the same as the narrative we used to understand the photograph.
- Life is a story. You are the hero.
- Who is your user and their big goal? What is their problem? What is your product name and market category? What is the competition? Why might they not want to adopt your product? Promise value/competitive advantage. What is the takeaway we want people to think or feel about our product? And again, what is their big goal? Has that goal been met?
- Unboxing is exciting, and is part of the product narrative arc.
- App sign-up flows are great examples of narrative arcs for users.
- The climax just needs to be nearest towards the end of any user flow. (I purchased the socks.) The resolution? (I got the socks.)
- The product narrative arc: Goal -> Problem Incentive CTA -> Flow -> Impediment (Sign up, payment, funnel drop-off, mental hurdles, boredom, lack of value, usability) -> Solve Problem/Experience Value -> Finish the flow/wrap it up. -> Goal met!
- Arcs give us a sense of time, and the ability to project what might happen.
- Our brains are activated when we recognize the narrative arc happening before us.
- Once you have a story, you can start developing it and testing it.
- Visualize the narrative arc by prototyping. Sketch it out. Illustrate the arc and all its plot points, and that will help you realize if the story is worth telling.

### The Last Ten Percent: When and Where to Add Polish That Matters
#### [Cassie McDaniel](https://twitter.com/cassiemc)

- 1. Why would we polish product?
- 2. How do we add that polish?
- 3. Does it matter if we add the polish?
- "The details are not the details. They make the design."
- We're in search of work that reflects the beauty we want to see in the world.
- Polish not only takes time, but a willingness to iterate and change what you did before. It means you've got to _stick with something_.
- If you're just copying something, you're not learning anything new. Start with the original idea and iterate on that to get something original.
- It's hard to get to the simple and obvious, but it's worth the journey.
- Critique is one of the most crucial tools as a designer.
- Surround yourself with people who will challenge your best work.
- We can collaborate with specialists to create really valuable work.
- Don't let perfection be the enemy of done.
- Iterate -> Balance -> Simplify -> Apply -> Work in a team.
- We will always be needed to make something more bespoke or human. It's the details that humans add that give an impression of something being, well, human.

### The Joy of Optimizing Images
#### [Una Kravets](https://twitter.com/Una)

- Images on the web affect all of us.
- Performance is a user experience problem. We need to take responsibility on every level.
- The average single JPG is 2.5x than the average JS file.
- The average iPhone 6 photograph is 2.5 MB. Waaaay too big.
- We take images without thinking about the cost: Irresponsible images! It becomes a problem when we cram these down the pipe to users.
- 19 seconds is the average load time for sites over 3G.
- Mobile site loading within 5 seconds had sessions lasting 70% longer.
- 53% of visits to mobile sites are abandoned after 3 seconds.
- People don't have patience for slow sites anymore.
- Most emerging markets/developing nations have yet to join the web.
- Most developing nations have poor infrastructure and slower devices.
- Access to information should be a basic human right. Performance addresses this.
- You can't be a web performance expert without being an image expert.
- Different formats are suitable for different types of content.
- Guetzli compression for JPEGs, which is a psychovisual optimization.
- General guidelines: 80% is a good maximum.
- WebP is a promising "new" format (it's been around for a while, but is gaining prominence).
- You can convert to WebPs using ImageMagick.
- Use the `<picture>` element to fall back to WebP.
- Use the `<video>` element to fall back to WebM.
- FLIF for responsive imagery sends multiple encodings in one file.
- Automate image optimization.
- ImageOptim is a great GUI program.
- SVGOMG, a web GUI for SVGO.
- Manually blur out unimportant parts of the image to save data.
- Use blurry placeholders for lazily loaded images ("blur up").
- Greyscaling reduces image size.
- CSS blend modes can liven up images and save data.
- Reducing contrast to reduce color space, which reduces file size: Start with image, remove image contrast, add contrast back in as a CSS filter.
- Manually tune GIFs in Photoshop to squeeze more bytes.
- Alternatives to GIFs: Videos.
- Leverage cache to keep media in caches longer.
- Inspect the `Accept` header to send WebPs on the server side.
- Compress SVGs using gzip/Brotli.
- Challenge the idea that 2x for Retina is always the "right" way to go.
- Consider your image format, and use `<source>` `media` attributes to send properly sized images.
- Find balance for users. It's all about user experience.

### The Case for Progressive Web Apps
#### [Jason Grigsby](https://twitter.com/grigs)

- The goal of progressive web apps (PWAs) is to provide the fastest possible experience, balanced with offline capabilities and native app-like features.
- Any site can be a PWA if they switch to HTTPS, add a manifest, and a service worker.
- PWA banners seem to convert 5-6x more than native app install banners.
- Installing native apps is onerous.
- A PWA is installed once the site is visited. Because the PWA is _just your site_. Adding to home screen and other features are the cherry on top.
- Progressive web app stores will eventually become a thing.
- SEO benefits of PWAs. Bing will highlight PWAs in Bing search results. There's a good chance PWAs will receive similar treatment in Google searches.
- Not every customer will have your app installed. PWA !== Native app.
- Mobile web audiences are 3x the size and growing 2x as fast as app audiences.
- PWAs === HTTPS by default.
- HTTPS means access to things like HTTP/2, Service Workers, Brotli.
- PWAs utilize application cache for performance.
- Your customers might benefit from an offline experience.
- Push notifications (maaaaybe).
- Manifests are simple JSON documents.
- PWAs are outperforming native apps.
- pwastats.com keeps track of case studies for PWAs.
- Platforms that don't support PWAs don't break the experience, even if things like service workers aren't supported.
- PWAs force developers to operate in a performance-first mindset.
- Display modes help us control what parts of the browser chrome we see.
- The `display-mode` media query can help us determine what display mode a PWA is in (e.g., `standalone`, `fullscreen`.)
- App shells mean first paint happens quickly.
- Cache recently viewed content for offline use.
- Push notification etiquette: Don't. Immediately. Prompt. For. Push. Notifications. People are annoyed by this.
- Build a PWA and see if it makes sense for you!

### 10 Things You Can and Should Do With SVG
#### [Chris Coyier](https://twitter.com/chriscoyier)

- SVG = Vectors. Other formats are pixels.
- You can use it in any way you use other images.
- SVG is a syntax. You can look at it. You can read it. You can change it in a text editor.
- Kind of like `<html>`, only it's `<svg>`. It's familiar.
- Animatable and scriptable.
- Resolution-independent.
- Quite accessible.
- 1. Charts and graphs
  - Nivo for React-generated SVG charts.
- 2. Shape morphing
  - GSAP + morphsvg
  - CSS is good at morphing, too.
- 3. Line drawing
- 4. Animate your interface
- 5. The best icon system ever.
- 6. Do art.
- 7. Diagrams
- 8. Headline lockups
- 9. SVG in the real world.
- 10. Explain your product.

---

## 13 DECEMBER

### Mission Possible: Stakeholder Alignment
#### [Kristina Halvorson](https://twitter.com/halvorson)

- Alignment is agreement or cooperation among a group with a common cause.
- Alignment is also a position of agreement and alliance.
- The absence of alignment is conflict.
- Alignment happens before conflict. It can't always prevent it, but it can ameliorate it.
- Don't stop aligning.
- 4 primary reasons for conflict are a lack of alignment on values, goals, methods, and/or facts.
- Belief is context-dependent. Has been shaped by our experiences.
- Values are concepts that transcend context. They shape our behavior.
- Be clear on goals.
- Good goals must be specific, measurable, attainable, relevant and time-framed.
- What is the method behind making a decision?
- Roles in decision making: Owner, sponsor, manager, product team, SMEs, everyone else.
- Facts: What are the relevant facts in product design? What assumptions are we comfortable moving forward with?
- Stakeholder interviews lay the foundation for alignment along the way.
- Purpose statement: Describe what the point of the projet is.
- Maintain a mutual understanding of what's important and why: Joint objectives, joint commitments, joint resources, joint risks.

### Performance as User Experience
#### Aaron Gustafson

- Good design is problem solving. Bad design is just window dressing.
- Our job is to remove friction from people trying to accomplish tasks.
- Poor performance is friction.
- A 1s delay in page load can reduce conversions by about 7%.
- Rendering delays can occur as JS and CSS are loaded.
- Reduce your overhead.
- Only include the assets you actually need.
- Optimize everything.
- Think about when we load assets.
- Only load assets that add value.
- Native features are effectively free.
- Use system font stacks where reasonable.
- If you need a custom font: subset, subset, subset.
- Only include the assets you actually need.
- Great tools can possibly be overkill. Use the right tool for the job.
- CDNs are great, but not bulletproof.
- `dns-prefetch`, `preconnect` for masking connnetion latency.
- `preload` for important assets.
- Breakup for managing media queries.
- Precompress assets for maximum speed.
- Think about _when_ we load assets.
- Consider _how_ we load assets.
- Not every article needs a picture.
- If you can avoid using an image, do it.
- If you need an image, choose the best format.

### Evaluating Technology
#### [Jeremy Keith](https://twitter.com/adactio)

- With technology, we can imagine what we want to exist in the world and take steps to make that happen.
- Technology is a human being augmented by hardware.
- The hardware starts become less and less important as the software matures.
- "Humans are allergic to change." - Grace Hopper
- The web was built on existing standards: HTTP -> TCP/IP, URLs -> DNS, HTML -> SGML.
- Fault tolerance in HTML is not an accident, it is by design.
- Content can degrade gracefully in older browsers.
- https://principles.adactio.com
- Goals (Declaration of Independence) Principles (Constitution) Patterns (The Law)
- Ask "how well does it work?" But also "How well does it fail?"
- CSS shapes and service workers are good examples of something that works well, but also _fails_ well when they are unsupported.
- Literally anything could and should be a PWA.
- Who benefits from all of this technology? Developers and/or users.
- Don't use solutions that benefit the developer at the expense of the user.
- Outward vs. inward technologies. Outward technologies (e.g., React) impose a tax on the user.
- The fallacy of assumed competency: If a large company is doing something, it must be good.
- Abstractions are fine (but ensure abstractions don't hurt the user).
- What are the assumptions in the technology? Does the philosophy of this tool match my own? If so, you can work quickly. If not, it's punitive to progress.
- We should be able to adopt technology at a reasonable pace. As needed.

### Where Accessibility Lives
#### [Derek Featherstone](https://twitter.com/feather)

- We have to work as a teamwork! We're not... afraid! 1... 2... 3... GO!
- Accessibility lives in people, process, and tools.
- Step 1: Set a goal.
- We should not be thinking about "perfect." That word carries connotations of something absolute and finished, and that can make people feel that the thing is unachievable.
- We should focus instead on "better." It should be where we're headed with this. We need to approach accessibility as a constantly evolving pace.
- Step 2: Start and learn quickly.
- Try to fix what you can this week, and then figure out what's left and how long it will take to do the rest.
- Step 3: Research and create a plan.
- Research: Work with real people with disabilities.
- Until we see how things work for real, we don't know how it will actually behave.
- Fix keyboard and forms issues first. Keyboard issues potentially affect everyone.
- Priorities: Highest business value, high impact/lox complexity, highest risk pages, can we solve other accessibility issues, too?
- Create your standard. It should always evolve to get better. Document those standards.

### Design for Real Life
#### Eric Meyer

- It's easy to break huge products that have immeasurably terrible effects.
- Algorithms can unintentionally be cruel.
- We tend to look at users as an undifferentiated sort of mass. People like us. They're not all like us, though. They have different experiences.
- Some people love chocolate. Or donuts. Some people don't. Some people can be hurt by those things. But that is not a problem to be solved.
- Unconscious biases can cause unintentional behavior.
- Error/compliance copy should be straightforward. Don't jerk frustrated people around.
- Processes shouldn't be punitive (don't make poeple fill out tons of paperwork if they might be in a crisis.)
- Don't insult users or unjustly accuse them in your copy.
- Don't harm people with your apps (e.g., Pokemon Go directing people into minefields).

### Measuring the Customer Experience
#### [Gerry McGovern](https://twitter.com/gerrymcgovern)

_Thanks to [Marya](https://twitter.com/emdot) for taking these notes!_

**Navigation is the main problem have with your web sites**
- Consider that it isn't good if people who are traveling down the highway are focusing on the navigation.
  - Insinuates that your hints/directions/signs aren't big or obvious enough.
- If customers focus on web navigation, is that good?
- Why are people hitting your navigation?
- Statistics can give us insight, but we don't know if spending a lot of time in the navigation is good or bad it's good or bad.
- We need to conduct usability studies to connect the what to the why.

**What should you do?**
1. Identify the expected customer journey (identify the path to specific information).
2. Test with real users how they get to that content (is it a completely different path? Could they find the information?)

**Example: An Irish person visiting Canada and needing visa information**
- Company mapped out that customer would go IMMIGRATION -> VISIT -> CLICK "eTA".
  - Assumed customer would know what "eTA" is
- Actual person went to TRAVEL and got stuck because there was no link/information for out-of-country visitors.
  - Actual person didn't consider their short trip immigration.
- The company's navigation has two core components
  - Travel to and travel from - run by two separate departments.
  - Gerry's team got the two departments together (they never spoke before), and now they have a TRAVEL -> VISIT CANADA journey.
  - Extra win: Collaboration across silos and divisions can happen when departments understand the problems that their users are having.

**Considerations**
- What are you putting in your most valuable real estate?
  - Most people take up the most valuable real estate (nearer top of the page) with worthless imagery. (Gerry wonders if there is a Department of Useless Images and if this is where all of the worthless imagery is obtained; he also posits that with every useless image, you must have useless content). Gerry would like you to stop doing this.
- "Your web site is not a murder mystery!"
  - We don't want a Steven Spielberg experience - we just want the information.
  - Make the links obvious.
  - Make sure you are linking to worthy content on real pages (he used an example of infinite loop
linking).

**Why do these navigation problems happen?**
- This happens because we never observe and measure real people using our things.
- We don't understand the core underlying problems and how we can solve them.
- We often fall into the trap of using fancy tech for fancy tech sake.

**Example: Find a passport Service location**
- 2014 - 93% success rate
- 2015 - 53% success rate
- 2016 - 100% success rate
- In 2015 they instituted a fancy map that looked good, but that didn't actually help the user. It added useless.
information that the user then had to wade through and drastically lowered the success rate. After realizing this problem, the company went to a more direct approach, lost the fancy and ended up with a perfect success rate.

- Take away: Sometimes you can be too clever. The shiny thing might not be the right thing. Instead, use smart solution. Pushing boundaries often is just pushing people's limits in patience.

**Second example: Norway Health**
- People just wanted to find out about cancer.
- Instead they showed fancy body graphic and forced people to point to location of their cancer in the graphic.
- Solution: focus on the core information people need.
- When they stopped asking for money and they focused on cancer, people started to give them more money. Solve the customer's problem and they will solve your problem.

**What should you do?**
1. Figure out the critical tasks and measure the success rate and how long it takes a user to complete task.
2. Bring up success rate as high as possible and you reduce the time as low as possible.
3. Outcome: Customers will buy more and be more loyal.

**Time**
- Save people time.
  - If you can make it easier, simpler, you can create powerful value.
  - Effective not in seconds but in hundreds of milliseconds.
    - 100ms customer experience is affected.
    - 1 s people are getting annoyed.
    - 3 s people just move away.
- It's not just physical performance; most of the time is wasted when you arrive at the page - stupid images and content.
- What takes time?
  - Time to download.
  - Time to read and use the page itself.
- Time is also relative.
  - What was fast 10 years ago is slow today.
  - e-commerce perceived okay time periods.
    - 2000 - 1 week.
    - 2010 - 2 days.
    - 2017 - 1 hour.
- Task Performance Indicator.
  - Reduce and manage that time.

**How to Do This**
1. Choose tasks
  - a. There are 8 - 12 core tasks in any environment.
  - b. No more than that, regardless of organization (see Top Tasks).
  - c. If these core tasks aren't working well, they have a major impact on the customer experience.
  - d. If you can understand this you can understand if it's working.
2. Get customers you are going to measure
3. Measure.
  - a. To deliver reliable metrics you need 13-18 people.
  - b. 3-8 can show you a core problem, but you won't be able to put a number on that problem.
  - c. 15 people you will get stable metrics of success and time.
4. Measure again in six months, to show improvements.
  - a. Every six months, measure same tasks
  - b. Repeatability and consistency will help inform you.
  - c. Powerful way of understanding if the environment is improving.
5. Create good task instructions.
  - a. Start with an answer. Don't start with task area. Go more into it...
  - b. "Compare countries" <- no. "Did more people die of x in Canada or France in 2004"
  - c. How did they get the answer - where did they go, how did they get there (did they get there).
  - d. Representative and typical.
  - e. This isn't an exam - you don't have to come up with something difficult - instead, something that should be easy to do!
  - f. Bad example "Find the maternity leave policy" (they could simply google this).
  - g. Good example: "Your colleague is pregnant. How many months can she take off?" (there are no hidden clues in the construction of this task request).
  - h. 20 words or less (30 words max)
    - i. You don't want them to have to go back to re-read - it will obstruct natural flow.
    - ii. Instead, embed the question into their short-term memory.

**Creating the Customer Journey**
1. Create the expected journey - what you think they will go on.
2. Then measure it - did your expected journey match the actual journey?

**Establish a target time**
1. You need to have an idea for how long this will take.
2. Perhaps from the customer journey.
3. Well, how long does it take on amazon? On top web sites?
4. Without a target, you can't measure it.

**Run the Test Remotely**
1. Remote is faster, cheaper and better for lab based testing.
2. Use WebX, Skype, or Gotomeeting.
3. Better if they are at home.
  a. Artificial environments cause people to behave artificially.
  b. Away from home creates false patterns.
4. Remote testing at least you aren't there and they are in their own environment.
5. You can test far more people, regularly, cheaper, better.

**User Testing Required Skills**
- Empathy - double edged sword (key skill is to shut up and not give hints).
- Analytical - that you see the patterns.
- Don't speak during the test – be clear with instructions before they start and then _BE QUIET_.
  - Be invisible.
  - Test your remote set up beforehand - your typing can be really loud and disrupt.
  - Instead - mute yourself so they don't hear anything.
  - Create an environment where they feel you're not there.
- Don't ask them to speak their choices outloud - this causes them to behave differently.
- Just behave your normal way - no guidance, no hints.

**Important Information to Convey to Your Users**
- You'll need to spend time to convince them.
- We are not measuring you.
- We are measuring the app and the web site.
- "If you want to give up, please give up" - we will learn more if you do your normal actions.
- We learn more from the failure points.
- Do they succeed or do they fail? Get the answer from them. They must give you the answer.

**What to pay attention to**
- Measure: how long did it take?
- Observe patterns (professional), not exceptions (amateur).

**Remember**
- Testing is not entertainment for you – you will be/should be bored.
- Leave the weird people alone. I know it's boring, but that is what delivers the value.
- Take advantage of video - great!
o Show the video - great for management; powerful; gets the truth/point across.
- Combine with data and that is the biggest change agent.
- Creates great momentum.

**Analyzing and presenting the two key metrics**
1. How do we increase success?
2. How reduce time?

**Manage the outcome not the input**
- Digital is about measuring what the customer does
- Stop measuring organization; instead, measure time to complete a task.

**Example**
- Try to hide the true intent of the task.
  - Let's say you just want to see if people can find a document and download it.
  - Hide the true intent of the task by creating this kind of task: "Find header on page 73 of Document X."

**What was the problem?**
- It's always confusing menus and links.
  - A link gives a promise. If most links were married, they would be divorced because they don't keep their promises.
  - The link should always be the destination not the format.
  - It's always the thing that you want.
- Biggest failure occurred because links are in the middle of the text !!! (Whoa!)
  - People get confused.
- Link isn't named clearly enough.
  - Naming of the thing is important.

**Truth**
- If you understand the problem and fix this task, you will probably simultaneously fix it for hundreds of tasks.
- You could fix thousands of problems.
- Most of this stuff you would never understand/discover if you didn't observe it.
- We don't see the simple issues bc we don't observe customer behavior.

**Outcomes**
- Went from 75% failure to 100% success!!!
- Not be redesign - just by fixing simple issues

**Key to Navigation, Part 1.**
- People - see the journey from the POV of the thing that they have. The journey is from the object. The journey will begin with the object and then look for troubleshooting. (<- !!!!)
- iPhone battery problem?
  - People will go iPHONE -> TROUBLESHOOTING (not TROUBLESHOOTING -> iPHONE).

**Key to Navigation, Part 2**
- Look for overall patterns.
  - These often affect multiple tasks
- People think in countries or topics.
- Models (two dominate patterns) will repeat

**More Keys to Navigation**
- Nobody looks in the right-hand column (that's why we called it "Don't Miss") (ha. Won't make any
difference.)
- Simplify - remove, take away - anybody can add
  - Glut is the core challenge of digital.
  - It takes a real professional to remove!!!

**TL;DR:**
- What was impossible to change became possible once you show the data.
- Identify the 8 - 12 top tasks.
  - Gerry never found an environment that was more
- Measure with real people over time - six months, 12 months
  - Compare performance of the changes you are making
- We need to understand what is working and not working.
- Measure, improve.
  - Measure again.
  - It's endless!
