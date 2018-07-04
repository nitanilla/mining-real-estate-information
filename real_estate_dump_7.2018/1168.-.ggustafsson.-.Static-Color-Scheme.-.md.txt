Static Color(less) Scheme
=========================

**"The best color(less) scheme for Vim in the world!"** ™

![Preview 1](https://github.com/ggustafsson/Static-Color-Scheme/raw/master/Extras/Preview1.png)

![Preview 2](https://github.com/ggustafsson/Static-Color-Scheme/raw/master/Extras/Preview2.png)

Q & A
-----
**Q: Is it really colorless?**

**A:** Nope, Vim interface elements etc have color but when it comes to syntax
coloring only comments gets some extra love.


**Q: Why NOT use thousand syntax colors?! ARE YOU INSANE?**

**A:** Possibly. Syntax colors are taking over the world and it is time to say
no before it is too late!

Syntax colors can be beneficial from a orientation and syntax error
highlighting aspect but at the same time it also makes readability worse
(darker colors etc) and it distracts you from truly learning the syntax of a
language.


**Q: Why are colored comments OK you hypocrite?**

**A:** While comments are indeed very important they are still second class
citizens compared to real code so it should not take attention away from it. It
can also make orientation easier, for example because of commonly added
descriptive comments above functions etc.


**Q: This is so stupid! I can't read my code without color everywhere!**

**A:** Not a question but OK... You need a fixed width font that has good
readability and works good for code. One of the very few that doesn't suck is
[Inconsolata](http://www.levien.com/type/myfonts/inconsolata.html). 16pt if you
got the screen real estate to spare, otherwise 14pt. End of story.

(Consolas might look much better than Inconsolata on Windows systems)

Installation
------------
Download the **static.vim** file and put it in **~/.vim/colors/** and run
**:colorscheme static** within Vim (add line to **~/.vimrc** or **~/.gvimrc**
if you want the setting to stick).

Static works great with [Pathogen](https://github.com/tpope/vim-pathogen) so if
you are already using it you then you can put this whole Git repository under
**~/.vim/bundle** for a hassle free installation.
