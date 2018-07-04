jqFullScreen
============

jQuery plugin for HTML5 FullScreen API

Most browsers/os have the ability to enter a fullscreen or kiosk mode for a while now. Basically the chrome UI vanishes 
and the content is alone takes up the entire real-estate of the displayed screen. Going a step further to control the 
content displayed in the full-screen programatically becomes very powerful. Thanks for W3C to comeup with FullScreen API 
specification and Chrome/Firefox to adopt them quickly.

W3C FullScreen API proposal: http://dvcs.w3.org/hg/fullscreen/raw-file/tip/Overview.html

In short, jqFullScreen provides an easy way for web content to be presented using the user's entire screen. Anyone, 
using jQuery should be able to just include this in thier page and it should work.

Usage:
=====

Browser Support: Safari 5.1+, Firefox 10+, Chrome 15+


/****** Convenient Methods *******/

$("#div-for-fullscreen").enterFullScreen();   
-----
// Make div-for-fullscreen htmlEl enter into full-screen mode


$().exitFullScreen();       
------
//document exits full-screen mode


$("#div-for-fullscreen").onFullScreenChange(handler)  
----
//Fire on full-screen mode change



/****** Static Helper Methods *******/

$.FullScreen.isSupported()  
-----
//Checks if the browser supports FullScreen API


$.FullScreen.enter(htmlEl)  
----
//Lets htmlEl to enter full-screen


$.FullScreen.exit()     
------
//document exits full-screen mode


$.FullScreen.isEnabled()
-----
//Figures out if the browser is in a state that would allow full-screen

$.FullScreen.isActive()     
-----
//True, if document is currently is full-screen mode

$.FullScreen.getActiveElement()  
-----
//Returns the element thats currently in full-screen mode

$.FullScreen.onChange(htmlEl, handler)   
-----
//Fires handler when htmlEl enter/exit full-screen mode


Presentation :
============

:fullscreen psuedo class is added to the html element once in full-screen mode.

div:fullscreen{    //W3C proposal

  height: 100%;
  
  width: 100%;  
  
}

div:-webkit-full-screen {     //WebKit

    width: 100% !important;
    
    height: 100% !important;
    
}

div:-moz-full-screen {        //Mozilla

    width: 100% !important;
    
    height: 100% !important;
    
}	

//Helper classes to show/hide elements when in full-screen mode

:fullscreen .hide-onfullscreen {

	display: none;	
	
}

:-webkit-full-screen .hide-onfullscreen {

    display: none;
    
}
:-moz-full-screen .hide-onfullscreen {

    display: none;
    
}

:fullscreen .show-onfullscreen {

	display: block;
	
}

:-webkit-full-screen .show-onfullscreen {

    display: block;
    
}

:-moz-full-screen .show-onfullscreen {

    display: block;
    
}


W3C standards indicate that :fullscreen and ::backdrop pseudo-class names when in full-screen mode. No browser is yet to implement :backdrop 

Note:

1. The z-index property has no effect in the top layer.
2. It is rendered as an atomic unit as if it were a sibling of the root element.
3. It is not rendered if it, or an ancestor, has the display property set to none.
4. Its containing block is the initial containing block.
5. Unless overridden by another specification, its static position for left, right, and top is zero.

References:

https://developer.mozilla.org/en/DOM/Using_full-screen_mode

http://dvcs.w3.org/hg/fullscreen/raw-file/tip/Overview.html#::backdrop-pseudo-element


