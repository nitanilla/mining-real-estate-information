# Like Clockwork Large Word Clock Design Files and Software

This repository holds the PCB/laser etch design files and Arduino code for my version of the word clock.

These PCBs and the laser cut glass faces are currently available via my store at: http://www.likeclockworkdesign.com/collections/kits/products/the-standard-makers-kit

The PCB measures 399x399mm and the glass faceplace measures 17"x17".

The PCBs are Arduino compatible and it runs the “Arduino on a breadboard” bootloader. The microcontroller is a Atmega328p (TQFP package) running at 8MHz that drives four 16x8 LED (512 LEDs) matrixes via four HT16K33’s. Time keeping is accomplished using a DS321 real time clock.  There is a linear power regulator on board to step down 9-12V input voltage to 5V. 

All unused Arduino pins are broken out to a pin header. Happy hacking!

The posted PCBs have been fabricated, assembled, and confirmed as working with the posted code.

*Upcoming Changes:*

The boards shipped ~~for the Kickstarter~~ going forward will have the following enhancements:
+ Addition of a footprint so that you can plug in standard Arduino shields. Done!

+ The ability to replace all ICs with prebuilt modules (Arduino Nano vs. Atmega328p, Adafruit matrix drivers vs. HT16K33s) for those who don’t want to drag solder tiny leads. Done!

+ Addition of a prototyping area to make use of all that extra real-estate. Done!

+ Addition of an Open Source Hardware logo. Done!

*Thanks to:*

+ The Kickstarter Backers
+ CERN for building KiCad and making it free.
+ Adafruit for their great libraries and making awesome breakout boards.
