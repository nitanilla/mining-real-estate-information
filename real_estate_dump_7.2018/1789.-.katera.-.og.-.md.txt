# Open Graph Extractor

## Docs
Open Graph Extractor written in Golang

[![License](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/katera/og/blob/master/LICENSE)
[![GoDoc](https://godoc.org/github.com/katera/og?status.svg)](https://godoc.org/github.com/katera/og)
[![codecov](https://codecov.io/gh/katera/og/branch/master/graph/badge.svg)](https://codecov.io/gh/katera/og)
[![Build Status](https://travis-ci.org/katera/og.svg?branch=master)](https://travis-ci.org/katera/og)
## Index

* [Support](#support)
* [Getting Started](#getting-started)
* [Example](#example)
    - [Extract Open Graph From Url](#extract-from-url)
    - [Extract Open Graph From String](#extract-from-html-string)
* [Contribution](#contribution)


## Support

You can file an [Issue](https://github.com/katera/og/issues/new).
See documentation in [Godoc](https://godoc.org/github.com/katera/og)


## Getting Started

#### Download

```shell
go get -u github.com/katera/og
```
## Example

### Extract From URL
```go
package main

import (
    "github.com/katera/og"
 )
 
func main() {
 
 res, err := og.GetOpenGraphFromUrl("https://hackernoon.com/golang-clean-archithecture-efd6d7c43047")
 
 if err != nil {
  log.Fatal(err)
 }
 
 fmt.Printf("%+v",res) 

}
 ```

 ### Extract From HTML string 

 ```go
 package main

import (
    "github.com/katera/og"
 )
 
func main() {
 
 htmlString:=
 `
 	<!DOCTYPE html>
 	<head>
		<title>Welcome to Zucktown. Where Everything Is Just Zucky. - The New York Times</title>
			<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
		<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
	<link rel="shortcut icon" href="https://static01.nyt.com/favicon.ico" />
	<link rel="apple-touch-icon-precomposed" sizes="144×144" href="https://static01.nyt.com/images/icons/ios-ipad-144x144.png" />
	<link rel="apple-touch-icon-precomposed" sizes="114×114" href="https://static01.nyt.com/images/icons/ios-iphone-114x144.png" />
	<link rel="apple-touch-icon-precomposed" href="https://static01.nyt.com/images/icons/ios-default-homescreen-57x57.png" />
	<meta name="sourceApp" content="nyt-v5" />
	<meta id="applicationName" name="applicationName" content="article" />
	<meta id="foundation-build-id" name="foundation-build-id" content="" />
	<link rel="canonical" href="https://www.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<link rel="alternate" media="only screen and (max-width: 640px)" href="http://mobile.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<link rel="alternate" media="handheld" href="http://mobile.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<link rel="alternate" hreflang="es-LA" href="https://www.nytimes.com/es/2018/03/24/facebook-google-zucktown-alphabet/?" />
	<link rel="alternate" hreflang="en" href="https://www.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<meta property="al:android:url" content="nytimes://reader/id/100000005735109" />
	<meta property="al:android:package" content="com.nytimes.android" />
	<meta property="al:android:app_name" content="NYTimes" />
	<meta name="twitter:app:name:googleplay" content="NYTimes" />
	<meta name="twitter:app:id:googleplay" content="com.nytimes.android" />
	<meta name="twitter:app:url:googleplay" content="nytimes://reader/id/100000005735109" />
	<link rel="alternate" href="android-app://com.nytimes.android/nytimes/reader/id/100000005735109" />
	<meta property="al:iphone:url" content="nytimes://www.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<meta property="al:iphone:app_store_id" content="284862083" />
	<meta property="al:iphone:app_name" content="NYTimes" />
	<meta property="al:ipad:url" content="nytimes://www.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<meta property="al:ipad:app_store_id" content="357066198" />
	<meta property="al:ipad:app_name" content="NYTimes" />
	<meta name="robots" content="noarchive" />
	<meta itemprop="alternativeHeadline" name="hdl_p" content="Welcome to Zucktown" />
	<meta name="channels" content="" />
	<meta name="title" content="Welcome to Zucktown. Where Everything Is Just Zucky." />
	<meta itemprop="description" name="description" content="In Menlo Park, Calif., Facebook is building a real community and testing the proposition: Do people love tech companies so much they will live inside them?" />
	<meta name="genre" itemprop="genre" content="News" />
	<meta itemprop="identifier" name="articleid" content="100000005735109" />
	<meta itemprop="usageTerms" name="usageTerms" content="https://www.nytimes.com/content/help/rights/sale/terms-of-sale.html" />
	<meta itemprop="inLanguage" content="en-US" />
	<meta name="hdl" content="Welcome to Zucktown. Where Everything Is Just Zucky." />
	<meta name="col" content="" id="column-name" />
	<meta name="pdate" content="20180321" />
	<meta name="utime" content="20180326104551" />
	<meta name="ptime" content="20180321050012" />
	<meta name="DISPLAYDATE" content="March 21, 2018" />
	<meta name="dat" content="March 21, 2018" />
	<meta name="lp" content="In Menlo Park, Calif., Facebook is building a real community and testing the proposition: Do people love tech companies so much they will live inside them?" />
	<meta name="msapplication-starturl" content="http://www.nytimes.com" />
	<meta name="cre" content="The New York Times" />
	<meta name="slug" content="25zucktown" />
	<meta property="article:collection" content="https://static01.nyt.com/services/json/sectionfronts/technology/index.jsonp" />
	<meta name="sectionfront_jsonp" content="https://static01.nyt.com/services/json/sectionfronts/technology/index.jsonp" />
	<meta property="og:url" content="https://www.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<meta property="og:type" content="article" />
	<meta property="og:site" content="nytimes.com" />
	<meta property="og:site_name" content="The New York Times" />
	<meta property="og:locale" content="en_US" />
	<meta property="og:title" content="Welcome to Zucktown. Where Everything Is Just Zucky." />
	<meta property="og:description" content="In Menlo Park, Calif., Facebook is building a real community and testing the proposition: Do people love tech companies so much they will live inside them?" />
	<meta property="article:published_time" itemprop="datePublished" content="2018-03-21T05:00:12-04:00" />
	<meta property="article:modified_time" itemprop="dateModified" content="2018-03-26T10:45:51-04:00" />
	<meta property="article:section" itemprop="articleSection" content="Technology" />
	<meta property="article:section-taxonomy-id" itemprop="articleSection" content="78FBAD45-31A9-4EC7-B172-7D62A2B9955E" />
	<meta property="article:section_url" content="https://www.nytimes.com/section/technology" />
	<meta property="article:top-level-section" content="technology" />
	<meta property="fb:app_id" content="9869919170" />
	<meta name="twitter:site" value="@nytimes" />
	<meta property="twitter:url" content="https://www.nytimes.com/2018/03/21/technology/facebook-zucktown-willow-village.html" />
	<meta property="twitter:title" content="Welcome to Zucktown. Where Everything Is Just Zucky." />
	<meta property="twitter:description" content="In Menlo Park, Calif., Facebook is building a real community and testing the proposition: Do people love tech companies so much they will live inside them?" />
	<meta name="author" content="David Streitfeld" />
	<meta name="tone" content="feature" id="article-tone" />
	<meta name="byl" content="By DAVID STREITFELD" />
	<meta name="PT" content="article" />
	<meta name="CG" content="technology" />
	<meta name="SCG" content="" />
	<meta name="PST" content="News" />
	<meta name="tom" content="News" />
	<meta name="edt" content="NewYork" />
	<meta property="og:image" content="https://static01.nyt.com/images/2018/03/20/business/00ZUCKTOWN-8/00ZUCKTOWN-8-facebookJumbo-v2.jpg" />
	<meta property="twitter:image:alt" content="Juan Salazar, a Facebook public policy manager, showed a model of the company&rsquo;s planned development to representatives of local businesses. &ldquo;Our goal is to strengthen the community,&rdquo; he said." />
	<meta property="twitter:image" content="https://static01.nyt.com/images/2018/03/20/business/00ZUCKTOWN-8/00ZUCKTOWN-8-videoSixteenByNineJumbo1600-v2.jpg" />
	<meta name="twitter:card" value="summary_large_image" />
	<meta property="article:author" content="https://www.nytimes.com/by/david-streitfeld" />
	<meta property="article:tag" content="Willow Village (Menlo Park, Calif)" />
	<meta name="geo" content="Willow Village (Menlo Park, Calif)" />
	<meta property="article:tag" content="Menlo Park (Calif)" />
	<meta name="geo" content="Menlo Park (Calif)" />
	<meta property="article:tag" content="Computers and the Internet" />
	<meta name="des" content="Computers and the Internet" />
	<meta property="article:tag" content="Area Planning and Renewal" />
	<meta name="des" content="Area Planning and Renewal" />
	<meta property="article:tag" content="Real Estate and Housing (Residential)" />
	<meta name="des" content="Real Estate and Housing (Residential)" />
	<meta property="article:tag" content="Social Media" />
	<meta name="des" content="Social Media" />
	<meta property="article:tag" content="Renting and Leasing (Real Estate)" />
	<meta name="des" content="Renting and Leasing (Real Estate)" />
	<meta property="article:tag" content="Real Estate (Commercial)" />
	<meta name="des" content="Real Estate (Commercial)" />
	<meta property="article:tag" content="Facebook Inc" />
	<meta name="org" content="Facebook Inc" />
	<meta property="article:tag" content="Alphabet Inc" />
	<meta name="org" content="Alphabet Inc" />
	<meta property="article:tag" content="Apple Inc" />
	<meta name="org" content="Apple Inc" />
	<meta property="article:tag" content="Chan Zuckerberg Initiative LLC" />
	<meta name="org" content="Chan Zuckerberg Initiative LLC" />
	<meta property="article:tag" content="Zuckerberg, Mark E" />
	<meta name="per" content="Zuckerberg, Mark E" />
	<meta property="article:tag" content="Mountain View (Calif)" />
	<meta name="geo" content="Mountain View (Calif)" />
	<meta property="article:tag" content="Cupertino (Calif)" />
	<meta name="geo" content="Cupertino (Calif)" />
	<meta name="keywords" content="Willow Village (Menlo Park  Calif),Menlo Park (Calif),Computers and the Internet,Area Planning and Renewal,Real Estate and Housing (Residential),Social Media,Renting and Leasing (Real Estate),Real Estate (Commercial),Facebook Inc,Alphabet Inc,Apple Inc,Chan Zuckerberg Initiative LLC,Zuckerberg  Mark E,Mountain View (Calif),Cupertino (Calif)" />
	<meta name="news_keywords" content="Willow Village Zucktown,Menlo Park CA,Computers and the Internet,Urban Planning,Real Estate and Housing,Social Media,Rent,Commercial Real Estate,Facebook,Alphabet,Apple,Chan Zuckerberg Initiative,Mark E Zuckerberg,Mount View CA,Cupertino" />
	<meta name="thumbnail_150" content="https://static01.nyt.com/images/2018/03/20/business/00ZUCKTOWN-8/00ZUCKTOWN-8-thumbLarge-v2.jpg" />
	<meta name="thumbnail_150_height" content="150" />
	<meta name="thumbnail_150_width" content="150" />
	<meta itemprop="thumbnailUrl" name="thumbnail" content="https://static01.nyt.com/images/2018/03/20/business/00ZUCKTOWN-8/00ZUCKTOWN-8-thumbStandard-v2.jpg" />
	<meta name="thumbnail_height" content="75" />
	<meta name="thumbnail_width" content="75" />
	<meta name="dfp-ad-unit-path" content="technology" />
	<meta name="dfp-amazon-enabled" content="false" />
	<link rel="alternate" type="application/json+oembed" href="https://www.nytimes.com/svc/oembed/json/?url=https%3A%2F%2Fwww.nytimes.com%2F2018%2F03%2F21%2Ftechnology%2Ffacebook-zucktown-willow-village.html" title="Welcome to Zucktown. Where Everything Is Just Zucky." />
	<meta property="fb:pages" content="5281959998" />
	<meta property="fb:pages" content="1002391179791389" />
	<meta property="fb:pages" content="105307012882667" />
	<meta property="fb:pages" content="123334484346296" />
	<meta property="fb:pages" content="142271415829971" />
	<meta property="fb:pages" content="1453472561556218" />
	<meta property="fb:pages" content="153491058028703" />
	<meta property="fb:pages" content="1545690368981813" />
	<meta property="fb:pages" content="1606969219532748" />
	<meta property="fb:pages" content="173455642668373" />
	<meta property="fb:pages" content="176999952314969" />
	<meta property="fb:pages" content="181548405298864" />
	<meta property="fb:pages" content="340711315527" />
	<meta property="fb:pages" content="5518834980" />
	<meta property="fb:pages" content="689907071131476" />
	<meta property="fb:pages" content="751965821517958" />
	<meta property="fb:pages" content="8254939527" />
	<meta property="fb:pages" content="98934992430" />
	<meta property="fb:pages" content="993603507345855" />
	</head>
	
	<body>		 
	<!-- Other Body -->
	</body>
	</html>
 `

 res, err := og.GetOpenGraphFromHtml(htmlString)
 
 if err != nil {
  log.Fatal(err)
 }
 
 fmt.Printf("%+v",res) 

}
 ```
 
## Contribution
To contrib on this project, you can make a PR or just an issue.

### Maintainer
- <a href="https://github.com/bxcodec">  **Iman Tumorang** </a> <br> 


