# Web Scraping

## Learning Objectives

- Explain what an API is
- Explain the necessity of web scraping in place of using an API
- Use CSS selectors to target different elements on an HTML page
- Use BeautifulSoup to fetch an HTML page and parse its contents

## Data Science and the Web

There's a whole bunch of information available on the web that we can use to parse
and extract meaningful data from. Today, we'll focus on how to retrieve data that
is not already formatted in a machine-readable way.

## HTTP

Whenever you visit a website, you're requesting a document using the HTTP protocol.
HTTP stands for Hyper Text Transfer Protocol.

Today we're going to:

- use python to make an HTTP request to some resource on the web
- parse the response's contents
- organize the contents in a data-science friendly way

## Intro to APIs

In an ideal world, all data on the web is available via a programatically accessible
interface - an Application Programmer Interface

**Basically, an API is a service that provides raw data for public use.**

API stands for "Application Program Interface", and technically applies to all of software design. However, since the explosion of information technology, the term now commonly refers to web URLs that can be accessed for raw data.

APIs publish data for public use. As third-party software developers, we can access an organization's API and use their data within our own applications.

**Check out these stock quotes...**

* [http://dev.markitondemand.com/Api/Quote/json?symbol=AAPL](http://dev.markitondemand.com/Api/Quote/json?symbol=AAPL)
* [http://dev.markitondemand.com/Api/Quote/json?symbol=GOOGL](http://dev.markitondemand.com/Api/Quote/json?symbol=GOOGL)

### Why Just Data?

Sometimes thats's all we need. All this information, from all these browsers and all these servers, has to travel through the network. That's almost certainly the slowest part of the request cycle. We want to minimize the bits. There are times when we just need the data. For those times, we want a concise format.

## What is serialized data?

All data sent via HTTP are strings. Unfortunately, what we really want to pass between web applications is *structured data*, as in: native arrays and hashes. Thus, native data structures can be *serialized* into a string representation of the data. This string can be transmitted, and then parsed back into data by another web agent.

There are **two** major serialized data formats:

* **JSON** stands for "JavaScript Object Notation", and has become a universal standard for serializing native data structures for transmission. It is light-weight, easy to read, and quick to parse.

```json
{
  "users": [
    {"name": "Bob", "id": 23},
    {"name": "Tim", "id": 72}
  ]
}
```
> Remember, JSON is a serialized format. While it may look like an object, it needs to be parsed so we can interact with it as a true Javascript object.

* **XML** stands for "eXtensible Markup Language", and is the granddaddy of serialized data formats (itself based on HTML). XML is fat, ugly, and cumbersome to parse. However, it remains a major format due to its legacy usage across the web. You'll probably always favor using a JSON API, if available.

```
<users>
  <user id="23">
    <name><![CDATA[Bob]]></name>
  </user>
  <user id="72">
    <name><![CDATA[Tim]]></name>
  </user>
</users>
```

**Many APIs publish data in multiple formats, for example...**

* [http://dev.markitondemand.com/Api/Quote/json?symbol=AAPL](http://dev.markitondemand.com/Api/Quote/json?symbol=AAPL)
* [http://dev.markitondemand.com/Api/Quote/xml?symbol=AAPL](http://dev.markitondemand.com/Api/Quote/xml?symbol=AAPL)

## Where Do We Find APIs?

APIs are published everywhere. Chances are good that most major content sources you follow online publish their data in some type of serialized format. Heck, [even Marvel publishes an API](http://developer.marvel.com/documentation/getting_started). Look around for a "Developers" section on major websites, or ask the Google Answer-Bot.

**That sounds hard. Can't you just give me a freebie?**

Okay... try the [Programmable Web API Directory](http://www.programmableweb.com/apis/directory) or the [Public APIs Directory](http://www.publicapis.com/).

## Intro to Web Scraping

Sometimes, there is information available on the web for which no public API is available.

### You do: Read

https://quickleft.com/blog/is-web-scraping-ethical/

I personally have taken on freelance gigs to extract emails from real estate agent websites, and rental property prices.

## BeautifulSoup

We'll use a module called beatiful soup to retrieve structured markup.

## We do Install Beautiful Soup

```
$ curl -O https://www.crummy.com/software/BeautifulSoup/bs4/download/4.4/beautifulsoup4-4.4.1.tar.gz
$ tar -zxvf beautifulsoup4-4.4.1.tar.gz
$ cd beautifulsoup4-4.4.1/
$ sudo python setup.py install
```

## We do retrieve famous quotes

```py
#!/usr/bin/env python

import urllib
from bs4 import BeautifulSoup
url = 'https://litemind.com/best-famous-quotes'

html = urllib.urlopen(url).read()
soup = BeautifulSoup(html,"html.parser")
for quote in soup.findAll('div',{'class':'wp_quotepage'}):
  text = quote.findChildren()[0].renderContents()
  author = quote.findChildren()[1].renderContents()
  print text, author
```

## You do: Scrape Craigslist

Let's write a program that scrapes craiglist looking for computer gigs

### Setup

```
cd craigslist-server
python -m SimpleHTTPServer
open http://localhost:8000/
```

### Level One

Retrieve the title, link, and date posted for all gigs listed on https://washingtondc.craigslist.org/search/cpg

### Level Two

Retrieve the title, link, date posted, and body for every gig

> Hint: You'll need to `open` each link from above to get the body

## If there's time...

Consider scraping something cool!

- http://www.realclearpolitics.com/epolls/latest_polls/
- http://www.baseball-reference.com/players/
- http://www.washingtonpost.com/wp-srv/metro/lottery/index.html