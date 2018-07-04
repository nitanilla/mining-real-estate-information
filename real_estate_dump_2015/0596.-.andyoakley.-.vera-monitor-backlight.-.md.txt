vera-monitor-backlight
======================

It's nice to have three monitors for a lot of screen real estate but the lights from the screens can often be overwhelming, especially at night. I installed a [3 x 10-inch LED strip](http://www.amazon.com/gp/product/B004DBU1O2/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B004DBU1O2&linkCode=as2&tag=andyoaklecom-20) behind the monitors which give a nice ambient light behind the screens.

This simple app runs in the background and watches system monitor state in Windows 8+. When the monitors turn off, it sends a command to Vera to turn off the light. When the monitors come back on, the backlight is turned on again.

Tested with a [VeraLite](http://www.amazon.com/gp/product/B007005364/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B007005364&linkCode=as2&tag=andyoaklecom-20) home automation controller. You will likely need to change the `IP address` and `DeviceNum` parameters in the `OnUrl` and `OffUrl` variables to match your setup.
