============================
ZenPacks.common.mib_browser
============================


Description
===========

This is Kells Kearney's ZenPack.community.mib_utils ZenPack, updated to work with Zenoss 3.  It has been tested 
with Zenoss 3.1 and with Firefox 3.6.13 and 4.0b12.  No functional enhancements have been made and the testing 
emphasis has been on the MIB Browser functionality, rather than any other features.

This ZenPack does NOT work with Zenoss 3.2.x.

Components
==========

The main MIBs menu has a new left-hand menu for MIB Browser which bring up Kells's original MIB Browser code.  Any MIB that has been loaded into Zenoss using the standard features, can be explored.

 

Little magnifying  glass icons appear in front of every MIB file, and if you click the  magnifying glass it brings up a tree-based browser (ie one that  understands the OID hierarchy, so that the OID x.2 follows x.1, not  x.11). (It also loads a popup, so if you don't allow popups from your  Zenoss server, you'll need to enable them, close down the new windows  and try it again. A popup window is used so that you can expand the tree  window to be as large as you like and still be able to view the  contents of the OID.)

The MIB browser is split up into three sections:

    A menu bar showing when the MIB was last loaded
    A set of tabs which will allow you to set different options.
    A MIB tree, which has two roots: Nodes and Traps

The  menu bar shows the last time that the MIB was loaded from the Zenoss  server.  There are currently five tabs available:

    Info: where information about the MIB can be changed, such as the MIB specification language, the description and the contact.
    Lookup: where you can lookup information about an OID using either its name or  its numeric form. After you hit return or change the focus on the window  the results will be displayed on the screen. (NB: snmptranslate must be  in the zenoss user's path for this to work.)
    Test settings: Enter the SNMP version 1 information into this tab and then when you  right click on a node or trap you can query this device starting at that  OID.
    SNMP: Provides background information about the Simple Network Management protocol
    Hide Tabs: Sometimes the screen real estate is important, so this provides a way to reclaim that space.

The  MIB browser shows you the description and other information about the  MIB, and there are two trees which you can select from the MIB: Nodes  and Traps. Any information not in the MIB (ie traps) will make part of  the tree stop at the root (ie Nodes or Traps). You can expand or  contract any portion of the tree that you wish, and the information  about any node that you select will appear in the OID popup window. If  you hover over a node, the truncated description of the OID will appear  in the tooltip.

By right-clicking on a Node or a Trap, you can  select a menu item to bring up a new pop-up window which will run a SNMP  version 1 snmpwalk on the defined test device and display the output  starting from the OID that you've hovered over.

Other details: Two extra routines are provided to make exploring Zenoss in XML a little easier: showXML and showMibasXML.

showXML:  This can be tacked on to the end of almost anywhere in the /zport  hierarchy and it will show you what the XML will look like if the data  were to be exported to disk. This tool allows you to gain a better  intuitive understanding of how the Zenoss XML files will actually  appear. The output is XML, so it relies on your browser's native  XML-handling capability to show you the XML tree and allow you to  navigate that tree.

showMibasXML: This is like showXML,  except that it only works from inside of the /zport/dmd/Mibs/mibs  hierarchy, and it outputs the XML file in a similar format to what  smidump produces. (smidump is the tool Zenoss uses to turn MIB files  into Python code, which is then introduced into the Zope database.)  Additionally, the XML tree of nodes and traps is produced sorted by OID.  For reference, a much smaller and easier to code version that doesn't  sort by OID (which is required for the browser) is included in the skins  directory of the ZenPack.


Limitations
===========

Zenoss doesn't store enough information  about the MIB to be able to recreate the MIB (eg import declarations are  missing). This means that any MIBs stored in Zenoss cannot be exported  to a file and used for other operations (eg download to a desktop or use  the MIB to create a graphical MIB tree in SVG using smidump -f svg).

Only  supports browsing MIBs that are stored in Zope, *not* all of the MIBs  that are stored on the Zenoss server. (Possibly to be examined. This  would probably involve running smidump over the MIB and then doing some  XSL modifications (minor modifications to structure and possibly a MIB  sort function) to produce acceptable output)

Only supports SNMP v1 snmpwalks. (To be examined)

This ZenPack does NOT work with Zenoss 3.2.x.

Requirements & Dependencies
===========================

    * Zenoss Versions Supported: 3.0, 3.1.x.  NOT 3.2.x
    * External Dependencies: 
    * ZenPack Dependencies:
    * Installation Notes: zenhub and zopectl restart after installing this ZenPack.
    * Configuration: 

Download
========
Download the appropriate package for your Zenoss version from the list
below.

* Zenoss 3.0+ `Latest Package for Python 2.6`_

Installation
============
Normal Installation (packaged egg)
----------------------------------
Copy the downloaded .egg to your Zenoss server and run the following commands as the zenoss
user::

   zenpack --install <package.egg>
   zenhub restart
   zopectl restart

Developer Installation (link mode)
----------------------------------
If you wish to further develop and possibly contribute back to this 
ZenPack you should clone the git repository, then install the ZenPack in
developer mode::

   zenpack --link --install <package>
   zenhub restart
   zopectl restart

Configuration
=============

Tested with Zenoss 3.1 

Change History
==============
* 1.0
   * Initial Release 
* 2.0
   * Updated Kells original ZenPack to work with Zenoss 3.1.x
* 2.1
   * Transferred to new github methods

Screenshots
===========
|mib_browser_2.0_zenpack_screenshot|


.. External References Below. Nothing Below This Line Should Be Rendered

.. _Latest Package for Python 2.6: https://github.com/jcurry/ZenPacks.community.mib_browser/blob/master/dist/ZenPacks.community.mib_browser-2.1-py2.6.egg?raw=true

.. |mib_browser_2.0_zenpack_screenshot| image:: http://github.com/jcurry/ZenPacks.community.mib_browser/raw/master/screenshots/mib_browser_2.0_zenpack_screenshot.jpg

                                                                        

