LuneOS Web Browser
==================

Next generation web browser.

Summary
-------
The LuneOS web browser, which will be the default web browser for the WebOS Ports LuneOS project. 

Description
-----------
The LuneOS web browser is built completely in QML on top of Qt WebKit and enables the user to browse the web.

Prerequisites
-----------
The LuneOS web browser uses luneos-components, make sure to have these available, you can get them at http://github.com/webos-ports/luneos-components

Features
-----------
Features:

1. Loads pages.
2. Creates browser history.
3. Private browsing feature via Tweaks (doesn't create history).
4. Ability to add bookmarks.
5. Can go back and forward.
6. URL prediction based on browser history & bookmarks
7. UI similar to legacy 3.0.x browser.
8. Support for both tablet (landscape) and phone (portrait) layout.
9. Custom UA strings in order to improve compatibility with websites.
10. Show/hide vkb using button which can be enabled in Tweaks.
11. Launching via Just Type :)
12. Has a settings page
13. Multiple tabs

Known bugs
-----------
Known bugs:

1. <s>After closing bookmarks/history/downloads panel, tapping on URL bar doesn't bring up Virtual Keyboard.</s>
2. <s>URL suggestions only looks in browser history, not in bookmarks yet.</s>
3. <s>Bookmarks panel is empty on loading.</s>
4. <s>Search doesn't always work yet.</s>
5. <s>Various layout and rendering issues.</s>
6. <s>Page gets added to browser history, even when not loaded (for example when there's no network connectivity).</s>
7. <s>Progress bar doesn't always behave properly.</s>
8. <s>Share dialog not working yet.</s>
9. <s>Cannot select cursor location in URL bar</s>
10. <s>Dropdown for search engine in Settings not working yet</s>
11. <s>Tapping on App Menu when visible doesn't hide it.</s>
12. <s>Authentication dialog doesn't look good on N4</s>
13. <s>Error message is not correct when no network connection is available.</s>
14. <s>Selection markers are not displayed at the correct location for long URL's. </s>
15. <s>Long URL's running behind stop/reload icon on address bar. </s>
16. <s>Text in addressbar needs some spacing. </s>
17. <s>Opening URL's 1 and 2 via luna-send will open URL 1 twice.</s>

To do:
-----------
To do:

1. <s>Add FocusScope to addressBar to see if that solves the VKB focus issue.</s>
2. <s>Fix the creation of browsing history for only properly loaded pages.</s>
3. <s>Add bookmarks in URL suggestions as well.</s>
4. <s>Create settings page to replicate settings from legacy.</s>
5. Add additional browser Tweaks (look at legacy to see what's interesting). 
6. <s>Add launch parameters + handling</s>
7. <s>Add icons for bookmarks (investigate legacy's handling).</s>
8. Add "search in page" See http://developer.blackberry.com/native/documentation/cascades/ui/webview/loadingwebcontent.html
9. <s>Add select, copy & paste where possible</s><i>Completed for address bar, available in nightlies</i>
10. <s>Fix share dialog</s><i>Available in nightlies</i>
11. <s>Flexible User Agent implementation, see Ubuntu approach.</s>
12. Add possibility to delete individual bookmarks/history/download items (swipable or otherwise).
13. Investigate search suggestions to see if those are possible from QML with our luna calls.
14. <s>Add possibility to edit bookmarks.</s>
15. <s>Add authentication dialog.</s>
16. Add password manager.
17. <s>Add cookies support.</s>
18. <s>Look into https everywhere (probably need to use sqlite DB created by https://github.com/EFForg/https-everywhere/tree/master/utils because to use 16000 XML files is a no-go).</s> SQLite DB is now provided, need to add logics to update URL before loading
19. Confirmation dialog for Clearing Downloads.
20. <s>Further make the preferences actually do something in the app.</s>
21. Make separate layouts for phones (portrait) and tablets (landscape) due to limited real estate in portrait mode, we want to reduce the number of buttons and find a solution for thos.
22. <s>Fix layout of address bar on TP. Anchoring seems off a bit sometimes</s>.
23. <s>Add scroll bar and style it webOS-y.</s>
24. <s>Clean up code and make separate QML files for components.</s>
25. <s>Add additional share options, based on check to see if certain app is installed?</s><i>Shelved for now, pending a "Sharing Manager" implementation</i>
26. Add divider for History items (as per legacy)
27. <s>Add "Input"->"File" support</s>
28. <s>Add further experimental support (minimal fontsize, viewport, device pixel ratio etc)</s>
29. Add Download Manager implementation

## Contributing

If you want to contribute you can just start with cloning the repository and make your
contributions. We're using a pull-request based development and utilizing github for the
management of those. All developers must provide their contributions as pull-request and
github and at least one of the core developers needs to approve the pull-request before it
can be merged.

Please refer to http://www.webos-ports.org/wiki/Communications for information about how to
contact the developers of this project.

