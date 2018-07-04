# Edison
My adventures with the Intel® Edison, using [SparkFun](http://www.sparkfun.com/) Blocks.

## Table of Contents
  * [Edison](#edison)
    * [Table of Contents](#table-of-contents)
    * [Introduction](#introduction)
      * [Me](#me)
      * [The Edison](#the-edison)
      * [My First Project](#my-first-project)
    * [Project(s) 0: SparkFun modules](#projects-0-sparkfun-modules)
      * [Project 0.0: GitHub repository](#project-00-github-repository)
      * [Project 0.1: SparkFun library](#project-01-sparkfun-library)
      * [Project 0.2: 9DoF demo](#project-02-9dof-demo)
      * [Project 0.3: Pong demo](#project-03-pong-demo)
      * [Project 0.4: PWM demo](#project-04-pwm-demo)
      * [Project 0.5: GPIO demo](#project-05-gpio-demo)
      * [Project 0.6: Button module](#project-06-button-module)
      * [Project 0.7: ASCII program](#project-07-ascii-program)
      * [Project 0.8: UART module](#project-08-uart-module)
        * [UART Hardware](#uart-hardware)
        * [UART Software](#uart-software)
        * [Confirm the GPS talks](#confirm-the-gps-talks)
      * [Project 0.9: GPS module](#project-09-gps-module)
    * [Project 1: GPS program](#project-1-gps-program)
      * [GPS Hardware](#gps-hardware)
      * [GPS Software](#gps-software)
        * [GPS Buttons](#gps-buttons)
        * [GPS Summary screen](#gps-summary-screen)
        * [GPS NMEA screens](#gps-nmea-screens)
        * [GPS Diagnostic screens](#gps-diagnostic-screens)

## Introduction

### Me
I am an Australian (which explains my spelling, with all those extra 'u's, and 's's instead of 'z's!) that has been programming embedded devices in C and C++ for decades, and have been amazed as the technology has shrunk to allow ever-smaller devices.

I started working with GPS when there were only three GPS satellites in the sky, so I'm familiar with most of the concepts - including the NMEA-0183 protocol used by most of the GPS receivers out there. The problem was that all of the code that I had developed for the company I then worked for still belonged to them - I had to re-create the code for me to use all over again!

(Note: I am not affiliated in any way with SparkFun - except as an enthusiastic customer!)

### The Edison
When I first saw the Edison on the [SparkFun](https://www.sparkfun.com/categories/272) website, its small size and powerful features made it an ideal hobbyist developer platform for me.

![The bare Intel® Edison](Images/Edison.png)

I've placed an Australian $2 coin (20.5mm, which is halfway between a US penny and nickel, albeit thicker) as a size comparison.

I immediately ordered one with a number of Blocks:
* The [Starter Pack](https://www.sparkfun.com/products/13276), containing:
  * The [Edison](https://www.sparkfun.com/products/13024) itself;
  * A [Base Block](https://www.sparkfun.com/products/13045), to allow Console and USB connectivity;
  * A [Battery Block](https://www.sparkfun.com/products/13037), for power away from the computer;
  * The [GPIO Block](https://www.sparkfun.com/products/13038), for General Purpose Input/Output;
  * A [Hardware Pack](https://www.sparkfun.com/products/13187), to keep the Blocks together;
  * A [USB micro-B Cable](https://www.sparkfun.com/products/10215), to connect it to my development PC.
* A [Sensor Pack](https://www.sparkfun.com/products/13094), containing:
  * An [OLED Block](https://www.sparkfun.com/products/13035), for portable display purposes;
  * A [microSD Block](https://www.sparkfun.com/products/13041), for removable storage purposes;
  * A [9 Degrees of Freedom (9DoF) Block](https://www.sparkfun.com/products/13033), for positional purposes;
* A [Pulse-Width Modulation (PWM) Block](https://www.sparkfun.com/products/13042), to drive motors;
  * A [number](https://www.sparkfun.com/products/9065) of [different](https://www.sparkfun.com/products/11965) [motors](https://www.sparkfun.com/products/10189);
* A [UART Block](https://www.sparkfun.com/products/13040), for direct (non-USB) serial communications;
  * A [GPS Module](https://www.sparkfun.com/products/13740), for something to communicate with.

[This kit](https://www.sparkfun.com/products/13742) would have been nice, but it wasn't available yet!

### My First Project
The ultimate aim for my first project was to make a tiny GPS, displaying on the OLED screen the current time (according to GPS), and my current position, speed and course. When I realised that the OLED Block came with buttons and a joystick, I saw that the program could be interactive - I could add extra 'screens' for debugging and delving into the data that the GP-20U7 GPS device was providing.

## Project(s) 0: [SparkFun](//github.com/sparkfun) modules
The first thing I wanted to do before embarking on my project was to become familiar with Intel®'s version of the C++ development environment Eclipse, and the Intel® libraries. SparkFun also provided modules for some of their Blocks, so I needed to familiarise myself with those as well.

### Project 0.0: [GitHub](//github.com/JohnBurger/Edison) repository
So before doing anything, I needed to collect all the SparkFun-provided libraries into one place, so that I could tailor them as needed for my requirements.

SparkFun already used GitHub for version control and to distribute their libraries and examples, so it was an easy job to collate them all into my own Git repository ([this one!](.)). I did want to maintain the link back to the original files though, so I worked through Git's (sometimes arcane) concepts to find out how. Of course, I then moved things around within my own repo, making it difficult to simply Pull future updates from SparkFun's repo. Ah well! I'll work through that when and if it becomes an issue...

### Project 0.1: [SparkFun](SparkFun) library
Once I had all the relevant files in the right place, I could compile a SparkFun library (libSparkFun.a) for inclusion with all my future projects - including into the demo programs that SparkFun provided.

### Project 0.2: [9DoF](9DoF) demo
To understand the Eclipse development environment, and ensure I could link with my new SparkFun library, I used SparkFun's 9DoF example program and modified it to work with a library rather than co-located code. That went together fairly easily - and now I had a handle on how to do it for other projects.

### Project 0.3: [Pong](Pong) demo
The OLED Block has a demo Pong program to show how to write to the screen and read from the buttons. Since my project would want to do both those things, this demo program was my second candidate for modification to use my SparkFun library.

This was the first time that I found a conflict between the pins used in the various SparkFun Blocks - the OLED Block's joystick and the GPIO Block share common pins, making the joystick and buttons unreliable.

```Note to self: don't use the OLED Block and GPIO Block together.```

### Project 0.4: [PWM](PWM) demo
The PWM Block also has demo code, since the Block adds new PWM ports rather than using the Edison's native ones. The Block's circuit board with the GPIO pins stick out past the side of the Edison Block stack, so to be able to connect the motors and external power I soldered [these pin headers](https://www.sparkfun.com/products/116) to the holes.

![PWM Block, with pin headers](Images/PWM.png)

I was able to quickly test the code with some LEDs to prove that everything worked.

### Project 0.5: [GPIO](GPIO) demo
The GPIO Block only has a demo program - there was no SparkFun-provided library code, since Intel®'s "mraa" library already has all the requisite functions.

The GPIO Block pins also stick out the side of the Edison stack, but this time I wanted to connect [hookup wires](https://www.sparkfun.com/products/11026) to the pins, and I have far more male-to-male hookup wires than male-to-female ones. So this time I instead soldered [these socket headers](https://www.sparkfun.com/products/11417) to the holes. I used two Kits, because they only came with one 10-pin header each - but I used the included 6-pin header to great effect with the UART Block [below](#project-08-uart-module)!

![GPIO Block, with socket headers](Images/GPIO.png)

Some smart cookie at SparkFun decided to use the opposite side of the stack from the PWM Block, so that the two didn't interfere with each other!

![GPIO and PWM stacked](Images/GPIO\ \&\ PWM.png)

### Project 0.6: [Button](SparkFun/Button) module
Although the [Pong demo](#project-03-pong-demo) showed how to use the buttons on the OLED Block, I realised that to provide debounce it went into a tight loop when polling the buttons, looking for the initial press. This works when the program (or thread) isn't doing anything else, but to use the code I had to either:

1. Use the code as-is, but write a threaded program (it had to process the GPS messages as well as the buttons);
2. Modify the code to provide a `Poll()` function to the rest of the program.

While most of the code I've written professionally has been threaded, for my ultimate first project it seemed overkill so I went with option 2. - but added some smarts, including auto-repeat.

### Project 0.7: [ASCII](ASCII) program
The SparkFun-provided OLED Block display library came with a number of fonts that can be selected. I wanted to see what they looked like, to design my project's screens. Above all I hoped that one (or more) of the fonts included the degree symbol (º) so that I could show my Lat/Long correctly - or whether I'd have to alter the font file or draw the circle myself.

So for my first actual, from-scratch program I decided to write a program that displayed the fonts, using the OLED Block's buttons for interaction - and to test the new Button module!

The program starts by selecting the first font, then going into a loop:

1. Display as many characters of the current font as possible;
2. If there's room on the display, also display the Hex code of the top-left character - so that I know what to code for special characters;
3. Wait for a button press:
  * Up/Down: scroll to next/previous row;
  * Left/Right; scroll to next/previous character;
  * Button A: show next font;
  * Button B: quit

![5x7 font](Images/Font\ 5x7.png)
![8x16 font](Images/Font\ 8x16.png)
![7-segment font](Images/Font\ 7-segment.png)
![Large number font](Images/Font\ Large\ Number.png)

Nice fonts - and the default 5x7 font had the degree symbol! From my DOS-programming days, it looks like it's what is often referred to as the "OEM Font" character set.

### Project 0.8: [UART](SparkFun/UART) module

#### UART Hardware
The UART Block is designed to connect to devices that interface using asynchronous serial communications - I'd have said "RS-232", "RS-422" or "RS-485", but these include electrical specification (such as ±3-12V or differential signalling) which this Block does *not* adhere to. If a suitable level converter is connected, this Block can implement any of the above standards - the actual serial protocol on this Block is the same with all of them.

But luckily the GP-20U7 GPS module that I got *also* isn't RS-232 or any of the others: it's TTL (0-5V), so I can actually directly connect it to the UART Block - or at least I could if it had the correct connector. Easy fix: cut off the tiny one and [crimp on](https://www.sparkfun.com/products/8100) a [0.1" 6-pin housing](https://www.sparkfun.com/products/retired/8099) with the wires in the correct places.

![GP-20U7 connector](Images/GP-20U7.png)

Only, the UART Block's pins do not project past the edge of the board, and the connnector is too thick to fit between two Blocks. That's OK - the 6-pin socket header I got in [this](https://www.sparkfun.com/products/11417) kit for the [GPIO Block above](#project-05-gpio-demo) does fit - and I can snip the Ground pin to indicate which way around to connect any devices!

![UART](Images/UART.png)

Note that the switch has been moved from the default `Console` position to the `UART1` position - I don't want to interfere with the normal Debug port.

#### UART Software
The default Linux code for handling serial communications assumes that on the other end is a person typing lines of commands for a shell program to process and display the results for. It offers numerous editing options and lots of smart processing - and only delivers the final line that the user pressed &lt;Enter&gt; on to the (patiently waiting) program.

The GPS unit does indeed send lines of text, but doesn't use any of the editing commands, and my program can't hang around waiting for the next message - the user might have pressed a Button! So, as with the [Button module](#project-06-button-module) above, I can either use a threaded approach to this interface, or put the serial driver into a 'raw' block mode - and write my own end-of-line detection code.

I decided on the latter approach - maybe I'll convert it all to a threaded model in the future.

#### Confirm the GPS talks
This is easy: connect the GP-20U7 to the UART Block (switched to the `UART1` mode rather than `Console`), and enter the command

```cat /dev/ttyMFD1```

Use `<Ctrl><C>` to quit the stream of characters - after noting that it sends a burst of lines every second.

### Project 0.9: [GPS](SparkFun/GPS) module
Most GPS devices send their data to the computer over serial lines using the [NMEA-0183](https://en.wikipedia.org/wiki/NMEA_0183) protocol. This is an ASCII protocol, so is human-readable (human-*understandable* however takes practice...). Many GPS units are configurable by the computer sending commands as to which NMEA messages should be sent. The GP-20U7 module I got, however, transmits a default set - and (out-of-the-box) doesn't have a Receive wire to receive commands to change this. No matter: the default set does everything I want!

I ended up finding a reference for the [protocol](https://www.sparkfun.com/datasheets/GPS/NMEA%20Reference%20Manual1.pdf) on SparkFun's website - which allowed me to parse some errors that I saw...

## Project 1: [GPS](GPS) program
I now have enough components to be able to assemble the whole project!

### GPS Hardware
Let's see: I'm going to need the Edison, something to power it (Battery Block), the UART Block, and the OLED Block... Uh oh!

The Edison is designed to be at one end of the stack of Blocks. The OLED Block, with its display and buttons, is designed to be at the opposite end of the stack. The problem is that the Battery Block also by default wants to be at the opposite end - so I had to peel the battery off the Block. Luckily SparkFun still put a Block connector under the battery, and it all fit together nicely:

![GPS Stack](Images/GPS\ Stack.png)

Note that the Edison itself is out of view between the stack and the battery.

### GPS Software
And this is what the running program looks like (I'm outside for a good view of the satellites):

![GPS Summary](Images/GPS.png)

### GPS Buttons
The program offers a number of screens that can be scrolled through by the OLED Block's joystick. As GPS information is received, the current screen is automatically updated with the latest information - which could be blank if not enough satellites are currently visible!
* To 'freeze' or 'unfreeze' the current data set, press Button A.
  * The display will be inverted, to show that the data is 'frozen'.
  * The screens can still be scrolled through to see the data at that instant in time.
* To quit the program, press Button B.

### GPS Summary screen
When the program starts, a Summary screen is shown that cherry-picks various fields from various GPS messages to tell you some relevant information (see screenshot [above](#gps-software)):
* The number of Satellites being used for tracking, from the number currently visible;
* The current UTC time;
* The current heading; (I'm stationary, so Heading is blank)
* The current speed;
* The current Latitude and Longitude (in degree-minute-second form)

Note that if the GPS module has only recently been connected or powered on, then it may take a couple of minutes of good visibility of the sky to get some initial fixes. Until then, the 'mask' of the various fields will be displayed empty. 

### GPS NMEA screens
By scrolling down, the details of the various last-received [NMEA-0183](https://en.wikipedia.org/wiki/NMEA_0183) messages are displayed. The message designation is provided in the top left corner.

![Satellites in view](Images/GSV.png)

Many screens don't have enough real estate to display all the data - scroll right and left on these screens to see more. To provide context, note that many 'side' screens repeat the main data.

### GPS Diagnostic screens
The last screen shows the total number of NMEA-0183 messages received, and how many `INV`alid, `UNK`nown and `CHK`sum-errored messages there were. Scroll right, and the next screen breaks down how many of each NMEA-0183 message type were received, and how many were in error.

![NMEA Message count](Images/NMEA.png)

(Caught mid-update, with one GSV message received in error!)

----
With many kudos and thanks to:
* @jimblom for the OLED libraries;
* @mhord for the GPIO, PWM and 9DoF libraries.
