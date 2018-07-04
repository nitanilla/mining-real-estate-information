# Real Estate monitor
A front-end tool for a popular German real estate website

![Screenshot](screenshot.png?raw=true)

# What?

Searching for a flat is a pain in the ass. Especially if the only popular online datatase is plagued by fake data, duplicates and lacks sane filtering features. Basically this leaves no choice but to write an own little tool that parses HTML pages and keeps it's own database, with filtering and stuff.

# Usage

1. Compile in debug
1. Create requests.txt in Downloader\bin\Debug
1. Goto [that website], make a search, copy the URL of the first page of results into requests.txt. Should look like this: https://www.thatwebsitename.de/Suche/S-T/Wohnung-Kauf/Umkreissuche/Berlin_2dMitte_20_28Mitte_29/10115/226453/2513307/Invalidenstra_dfe/-/20/2,00-/-/EURO--300000,00?enteredFrom=one_step_search
(optional: several requests supported, separated by newline)
1. Run GUI, hit Update, wait til it downloads stuff, enjoy!
