# N Things I Wish I Knew About Programming Before I Started Programming

### 1. Style Matters
The minute that you can write code is the second you should be worried about style.

In Kindergarten, you learned how to write letters. Did you just scribble out anything that looked vaguely like letters? No. You were given a workbook and you traced letters to match what they should look like because there are standards to what they should look like.

Similarly, by adhering to a disciplined style, your code will be easier to read. When you encounter a problem, your consistent style will make it more obvious when something is amiss. Even more importantly, if you ever need help and have to show your code to someone else, make it as easy as possible for them to help you. Looking at other people's code is hard enough. Looking at other people's poorly styled code is frustrating and makes it harder to help you.

### 2. Talk It Out
Verbalizing your problems can reveal your errors.

Sometimes I feel that I think in a language that only I can understand. When I get stuck I feel like I'm cornered and don't know where to turn. Since I do my best coding alone at home, I can't easily ask for help. I have found one of the best remedies was to merely speak my thinking process aloud to myself. The conversion from my unique mental language to spoken English, and then translating it back to my mental language after reconsuming the logic has often made me realize that logic was nonsense.

A similar phenomenon is called [Rubber Duck Debugging](http://pressupinc.com/blog/2014/06/psychology-underlying-power-rubber-duck-debugging/). Imagine that you're explaining your code to a completely ignorant rubber duck. You will be forced to slow down your thinking and explain it in a way that takes no knowledge for granted, revealing a mistake you might quickly gloss over. This also applies to teaching others in order to reinforce your own knowledge. By slowing down and explaining every single step you have to think about the problems in ways that you don't otherwise think of when using your own mental processes.

### 3. Comment As You Go
When you write a non-trivial piece of code, take a second to write a small sentence about what it does.

This ties into tip number 2. If you build something that requires more than a glance to the average coder, leave a comment. Have the reader read a plain English description of your logic rather than forcing them to trace the steps. If you ask someone for help on some of your code, they are going to be more lost than you. Leaving comments is like leaving the next person breadcrumbs to navigate through your forest of code.

Sometimes, you're going to be the next person that has to look at your code. Do you want to look at your own undocumented code to figure out what the heck you were thinking 7 months ago? Why would you do that to yourself? Do yourself a favor. [Leave a note.](http://media1.mic.com/site/article-items/2739/1_gif.gif) It's like leaving a present for your future self. Future-You will be happy you did.

### 4. Computer Science is Essentially Applied Mathematics
Strictly speaking you won't use much advanced math when programming, yet having an advanced math background allows you to be a better thinker when you face a problem.

Intricate logic, algorithms, and recursions are at the root of every program which require very abstract thinking. Having a strong foundation in math stretches your mental capacity to visualize and keeps you disciplined in your methods. Conceptualizing the ideas of limits, the puzzle solving of integration, and the testing of infinite series all prepared my mind for highly abstract programming.

I would go so far as to say that those that are poor in math are the poorest programmers. If you are self-admittedly poor at math, then you should remedy that or reconsider your path.

### 5. Work Top-Down (Think First, Code Later)
> Bad programmers worry about the code. Good programmers worry about data structures and their relationships.
> Linus Torvalds, developer of the Linux kernel

Design your algorithms first at the highest level, i.e. explain in English each step on your path to the answer. Then, translate your English into more mathematical, logical operations via flow charts. Then finally, you can translate your logic into code.

Coding should be the last thing you ever do with your program. If you can envision your data structures and work flow in your head and on paper, then creating the code will be the easiest part. 

### 6. Programming Takes Time; Start Early
When you first face a problem, your vision is limited to the surface. There are problems beneath the surface that you cannot even imagine until you actually get your hands on it. Affording yourself downtime allows you to digest unexpected problems.

The importance of starting early cannot be overstated. On the path to the solution you may find that your first draft algorithm is returning bad results, or you don't actually know how to use some feature, or you find an edge case you have no idea how to handle. I guarantee that you will always hit a bump in the road in development and it will derail your projected finishing time. If you decided to make your program 2 days before it's due, then your back is completely against the wall. If you started working on it 2 weeks before the due date then, you have many days to step back from the project and ponder on the strange occurrence.

When you step back from the project, a funny thing happens. By freeing your mind of burden for a while, you can come back to the project with clearer eyes, and from a new perspective. You can come back to see that you were actually calling methods on a NULL node (instead of the node that points to a NULL node) which caused you six plus hours of seg faults and headaches (true story). Sometimes it doesn't even take that long have a flash of brilliance. I cannot recall how many algorithms I've solved in that strange hinterland between wake and sleep.

### 7. Revision Is A Gift From You To Yourself
> Michael's Conjecture: Any human at time T is more intelligent than he or she was at time T-n, where n is a length of time greater than zero.

> Proof(?): Assume towards contradiction that a human at time T is less intelligent then he or she was at time T-n. Therefore, the human is discarding knowledge, or the mind's intellectual capacity is shrinking, or that there is an upper bound on a person's intelligence. Therefore, one becomes more dim over time. This assumption contradicts the idea that knowledge and experience can be collected over time and thereby cause ones mental capacities to expand by virtue of what has been learned. Because the assumption leads to contradiction, we must conclude that the original proposition is true. QED(?)

In conjunction with number 6, if you allow yourself excess time to ponder your project, then you will have time to revise. By my conjecture, the person who revises your work (i.e. you) will be smarter than the person who wrote it (i.e. you). You will be able to look over your work with keener senses than they were at the time of construction.

### 8. Draw a Picture
> "When you don't understand the problem, draw a picture. If you still don't understand it, draw a bigger picture"
> Alexey Nikolaev, Adjunct Lecturer at Hunter College

Early on in coding, looping through arrays is a difficult concept to understand. Anytime I had trouble I would draw what my array should be and I simulated what the computer was doing at any given moment. Look at position zero, do your thing, then increment until the end. I often spoke out my actions aloud in the rubber duck debugging fashion to listen for inconsistencies.

I do this to this day especially when working with trees. They are absolutely not easy to keep track of.

### 9. Screen Real Estate
When you begin to have 3+ files in a single project, having more monitor space to place your code, input files, output files and other documents helps you visualize all your work. I am fortunate enough to have my desktop connected to 2 monitors, 24" and 20", which allows me to work on multiple files at once, as well as keep my textbook open, and a window for browsing stackoverflow and facebook. A second monitor is well worth the investment.

On the opposite end, this is why I don't enjoy programming on my laptop. Thirteen inches of screen space is horribly limiting, even if it is retina display.

If you are unable to obtain a second monitor, see if your operating system is capable of "workspaces". These are essentially virtual multiple monitors. The only issue here is that you can only view one virtual "workspace" at a time. MAC OSX and Linux operating systems are capable of this feature. Microsoft recently enabled this feature (finally) for their latest Windows OS release, Windows 10.

**Update 12/19/2016:** *I bought a MacBook Pro 13" and got [window organizing software](https://github.com/fikovnik/ShiftIt) which allowed me to maximize screen real estate within 13" and using the aforementioned virtual workspaces. It's still nicer to work with several large monitors, but programming on a laptop isn't as painful as it was on my Windows 8 laptop.*

### 10. Use An IDE
Hardcores will disagree with this one. I started out learning trivial coding on VIM and it was fine. Once I needed to make non-trivial algorithms, I began to use Visual Studio. I found it incredibly helpful for the IDE to sense my errors without having to compile every time, and then take me to the exact line that the error occurs. When I started to have 3+ files in my project, it was helpful that the IDE kept track of my variable and method names across files. Tab auto-completion removes the chances of making typos. I was able to set a guideline at 80 characters which then forces wordwrap.

I know that a lot of these features can be found in most text editors, but the biggest help was to be able to compile, debug and run in the same window with just the touch of a few buttons. This is what sets it apart.

**Update 12/19/2016:** *I personally stopped using IDEs midway through CSCI 335 because I bought a MacBook Pro and found that I can be much faster by simply using text editors and the terminal. However, that speedup is only a convenience with a higher degree of skill and experience with the command line and programming in general. I no longer needed to features of the IDE as a safety net.*

*Certainly there are benefits to the IDE for beginners, but it becomes cumbersome when the build process becomes more complex, such as with templating (you must not build the object files since they are already included in the headers), or creating alternate main functions for testing. I'll only use an IDE for truly large projects that need tools to aid with organization or collaboration, like when I did my CSCI 340 project in Python, I used PyCharm.*

### 11. Abandon The Mouse (as much as possible)
This may sound trivial, but the motion to shift your right hand from the home row to the mouse is costing in both time and health. By using the arrow keys, home/end/pgup/pgdn, you are saving time on an action that you will do hundreds of times per hour. I've also found that the most strain on my wrists have come from the mouse, not the keyboard.

To help ease the transition into keyboard-only, go to your keyboard settings, and set your key repeat delay to minimum time, and key repeat frequency to maximum. This makes navigating a text file with the arrow keys much more bearable, and just as precise as the mouse, if not more so.

Study the shortcuts of your IDE or text editor. While it may seem like you are wasting time looking up shortcuts, those seconds that you save quickly add up, and it definitely becomes worth it in the long run.

### 12. Keyboards and Typing
While I'm talking about keyboards, I highly suggest you invest in an ergonomic style keyboard since you'll be using it at least 8 hours a day. It is much more comfortable to have your wrists angled. I've been using them for about 10 years now and will never buy a straight keyboard again.

Learn [Touch Typing](https://www.wikiwand.com/en/Touch_typing#/Advantages). Learning how to type will alleviate pain in your neck because you'll never need to look down at your keyboard, then back up to your monitor, as well as pain in your wrists because you'll be moving less. Moving parts have more wear and tear than those that are static.

You'll be sitting down for hours on end now that you're going down this path, take care of yourself. Spend a little extra money to make your life easier.

Many programmers swear by the use of mechanical keyboards, as oppossed to the rubber dome model keyboards. This is obviously personal preference, but you should at least take them into consideration.

### 13 through N To be continued...
