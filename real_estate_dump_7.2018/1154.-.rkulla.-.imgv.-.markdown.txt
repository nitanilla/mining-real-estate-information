# IMGV

(*UPDATE: this project has been abandoned. It had a good run from 2001-2006*)

Imgv is a cross-platform image viewer with an opinionated interface - meaning that certain
features were added or are missing intentionally. Its main opinion is that screen
real-estate is most important and so the interface tries to stay out of your way. 

The viewer also cares about privacy and so it doesn't cache your images and it
even has the ability to temporarily 'hide' what you're viewing.

It also has very flexible viewing options, such as the ability to view 4
images at a time, and view/download from URLs.

![imgv-sshot1](https://cloud.githubusercontent.com/assets/244283/17833421/aeb93d1c-66d1-11e6-95d6-31284be48270.jpg)

## Requirements

- python 2.2 or higher
- pygame
- python-imaging (PIL)

The operating system doesn't matter as long as you have the above requirements.
It should work on Linux, Mac OS X, Windows, etc.

## Features
**Supported Files:** JPEG, GIF, PNG, TIFF, BMP, PCX, TGA, PPM, PNM, PBM, PGM, XPM, XCF, LBM, IFF, MPEG

**Movies Support:** View MPEG movies

**Costumization:** Edit "imgv.conf" to configure IMGV's interface and abilities to your desires.

**Command Line:** Ability to load image files from the command line.

**Histogram Support:** View an image histogram in color.

**Fullscreen Support:** View images in fullscreen mode.

**Play Lists:** Have collections of images. Files can be in any directory or drive on your system or even on the Web.

**Slideshows:** Create different types of slideshows.

**Hand Tool:** Drag images to move them around the screen

**Persistent Zoom:** Lock the zoom amount so that all images are auto-zoomed to that amount<

**Shuffle:** Dynamically randomizes the images, even across multiple directories.

**Search Filters:** Search for or filter out certain images.

**Typical Features:** Zoom-in/out. Rotate. Flip vertically/horizontally, etc.

**Multi-view:** You can view four images at a time (and even slideshow in this mode) 

**Exif Support:** On-the-fly viewing of Exif information (meta-data from images that came from digital cameras, scanners, etc) and detailed Exif viewing are available.

**Transitional Effects:** Effects currently include "fade in" and "melt". Ability to set multiple effects to run at the same time.

**External Editor Support:** Launch images into an external editor such as Adobe Photoshop for editing.

**Wallpaper Setting:** - Easily set your desktop wallpaper.

**Thumbnail Support:** View screenfulls of thumbnails and adjust their sizes.

**Extract Images from web pages:** View individual images from Web URL's or extract all images from a Web page. You can then manipulate the images and even download them.

**Multi-Directory Loading:** You can tag multiple directories to load all of their images at the same time.

**Subdirectory Loading:** Optionally load sub-directories too.

**Image Closing:** Remove an image from your current session without deleting it.

**Image Hiding:** Hides displayed images by blanking the window until a keypress or mouse-click. You can also password protect this feature.

**Image Details:** Shows an entire screen full of information about the image.

**ScreenSaver Disabling:** IMGV temporarily disables your screensaver when watching movies or viewing slideshows.

## Installing from Source

The easiest way to install imgv from source is to just run:

    $ sudo python setup.py install

If you don't have permissions to install to your global site-packages, or if you
simply don't want to, then you can install it locally by doing:

    $ python setup.py install --user

which will install it somewhere such as ~/.local. And you'll probably need to
manually add ~/.local/bin/imgv to your system $PATH.

To see where everything installed you can run it as:

    $ python setup.py install --record files.txt

and then examine files.txt.

You could alternatively use virtualenv and just run:
   
    $ python setup.py install

but I don't recommend that unless you're fine with having to also install the
dependencies into the virtualenv first, and creating a from ~/bin/imgv to
~/.virtualenvs/imgv/bin/imgv or similar.

If you don't have distutils, or if you don't want to install it via setup.py, 
you can always do it manually:

add /path/to/imgv/imgv to your $PYTHONPATH from the root of the package run:

    $ bin/imgv

or better yet, the script 'imgv' from the bin/ directory into a directory in 
your $PATH, such as ~/bin, or add /path/to/imgv/bin/ to your path, so you can
then invoke it as simply:

    $ imgv

The first time you run imgv, it will create the directory "$HOME/.imgv" and put
a sub-directory called "data" in it. If you want to use a different location for
the imgv home folder, then move $HOME/.imgv somewhere else and create an 
environment variable called IMGV_HOME. In linux this means opening your 
bash_profile (or the equivalent depending on your shell)
    
    $ mv ~/.imgv /whatever
    $ export IMGV_HOME="/whatever/.imgv"

You can also copy imgv.conf to the root of the IMGV_HOME directory to have imgv
read it from there from now on.

## Installing on Windows

If you're using MS-Windows and you unpacked imgv in C:\Program Files\imgv then 
search the internet for how to change environment variables in your particular
version of windows, or do it the old fashioned way and edit autoexe.bat:

    set IMGV_HOME=C:\Program Files\imgv

Reboot for changes to take affect.


## Usage

- Imgv also takes optional command-line arguments:

    $ imgv [directory|image|remote image]

  If you're in Windows and have the executable binary version "imgv.exe" Click on
  imgv from the start menu if it was installed there.  Or in a cmd prompt type:

    C:\"Program Files"\imgv> imgv.exe [directory|image|remote image|movie]

- When you right click in imgv a menu pops up. Simply click on what you
  want to do. (Clicking your middle mouse button will close the menu)

- Or you can use the keyboard to operate imgv press 'h' from inside imgv
  to get a list of keys supported and their functions. 


## Loading images from web sites

Imgv allows the loading of remote images by forming a name like:

    imgv http://www.site.com/bla.jpg

When imgv is running you can click the 'Open URL' menu option and enter a valid
URL for imgv to extract images from such as:

    http://www.site.com/  (you usually need that appended / for this to work)
    http://www.site.com/foo.html
    http://www.site.com/bla.jpg

## Playlists

In order for the play list feature to work you always must have a file named 
'playlists' in the data/ directory (the default).  If you want to create new 
playlists and/or edit them manually using your text editor you need to put the
name of the play list on its own line in the 'playlists' file and also create a
file with the name of the playlist. Make sure there are NO blank lines in either
file. I recommend only using imgv to handle all the playlist stuff but this way 
can be faster.

To create a new playlist manually:

    cd data/
    echo "new playlist name" >> playlists
    touch "new playlist name"
    
To add new images to a play list manually:

    cd data/    
    echo "/home/user/pics/bla.jpg" >> "play list name"

## Configuration

You can edit the imgv.conf configuration file to customize imgv.

If you ran setup.py then imgv.conf will be in your IMGV_HOME, e.g., $HOME/.imgv/

If you have used the Windows Installer from version 1.3.6 or below, then
it will be in the data/ folder where imgv was installed.

## Contact

If you have questions email me at: rkulla@gmail.com

IMGV's homepage is: http://imgv.sf.net/
