# awesome-URLSchemes
> a collection for iOS URLSchemes

**非常欢迎大家提pull request 或者 issue 来提交你知道的scheme**


## 关于

URLScheme 是作为 App 之间跳转的一种常用的手段。目前绝大部分的 App 也都支持。自从有了 Widget 之后，也出现了很多 Luancher 可以帮助你快速的启动 App 或者 执行 App 内部的某个动作。于是就有了这个列表，尽可能的收集目前支持 URLScheme 跳转的 App 所支持的 URLScheme 的情况。以方便您快速使用 URL Scheme 去构建一些更有效率的东西。


## 怎么使用

Awesome-URLSchemes 是一个大集合他可以帮助您快速找到一个 app 支持的 URLScheme 并构建一个 URL 取执行特定的动作例如：

1. 打开某些App
2. 开发某些APP的特定页面
3. 在固定时间打开某些 App
4. ....

## 介绍

* [URL Schemes 使用详解](https://sspai.com/post/31500)

## 内容

* 系统
* 应用



## 系统

> iOS 10 把之前 prefs 开头的 URL Schemes 改成了 Prefs 开头。如果是 App 调用，可添加“App-”前缀。 这些在iOS 11上目前都无效。还在继续寻找有效的方法。

* 电池电量 Prefs:root=BATTERY_USAGE
* 通用设置 Prefs:root=General
* 存储空间 Prefs:root=General&path=STORAGE_ICLOUD_USAGE/DEVICE_STORAGE
* 蜂窝数据 Prefs:root=MOBILE_DATA_SETTINGS_ID
* Wi-Fi 设置 Prefs:root=WIFI
* 蓝牙设置 Prefs:root=Bluetooth
* 定位设置 Prefs:root=Privacy&path=LOCATION
* 辅助功能 Prefs:root=General&path=ACCESSIBILITY
* 关于手机 Prefs:root=General&path=About
* 键盘设置 Prefs:root=General&path=Keyboard
* 显示设置 Prefs:root=DISPLAY
* 声音设置 Prefs:root=Sounds
* App Store 设置 Prefs:root=STORE
* 墙纸设置 [Prefs:root=Wallpaper](Prefs:root=Wallpaper)
* 打开电话 [Mobilephone://](Mobilephone://)
* 世界时钟 Clock-worldclock://
* 闹钟 Clock-alarm://
* 秒表 Clock-stopwatch://
* 倒计时 Clock-timer://
* 打开相册 Photos://
* 日历 calshow://
* 备忘录 mobilenotes://


## 应用

### 微信

> 在 微信 6.3.25 版本中，所有外部唤起 URL 的方式均无法打开对应页面。 未来这些 url 都只能在微信内部的浏览器使用了。


前缀 **weixin://**

* 唤起 weixin://
* 扫一扫 wexin://scanqrcode


### 支付宝

前缀 **alipay://**

* 唤起 alipays://
* 滴滴出行 alipays://platformapi/startapp?appId=20000778
* 蚂蚁庄园 alipays://platformapi/startapp?appId=66666674
* 收款 alipays://platformapi/startapp?appId=20000123
* 转账 alipays://platformapi/startapp?appId=20000221
* 股票 alipays://platformapi/startapp?appId=20000134
* 扫一扫 alipayqr://platformapi/startapp?saId=10000007
* 记账 alipay://platformapi/startapp?appId=20000168
* 蚂蚁森林 alipay://platformapi/startapp?appId=60000002
* 手机充值 alipayqr://platformapi/startapp?saId=10000003

### [iLauncher](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fancylauncherplus://

### [百度地图](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开APP  baidumap://
* 回家  baidumap://map/direction?origin=我的位置&destination=${DADDR}&mode=driving&coord_type=gcj02
* 搜索附近  baidumap://map/place/search?query=${QUERY}

### [高德地图](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开APP  iosamap://
* 回家  iosamap://path?sourceApplication=iLauncher&${DADDR}&dev=0
* 搜索附近  iosamap://poi?sourceApplication=applicationName&name=${QUERY}&dev=0
* 附近交通状况  iosamap://showTraffic?sourceApplication=iLauncher

### [Google Maps](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开APP  comgooglemaps://
* 回家  comgooglemaps://?saddr=${SADDR}&daddr=${DADDR}&directionsmode=driving
* 搜索附近  comgooglemaps://?q=${QUERY}

### [Evernote](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  evernote://

### [AOL Radio](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com.aol.radio

### [Epocrates](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  epocrates-essentials://

### [WeatherBug - Weather Forecasts & Alerts](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb314671695276719://

### [eBay](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ebay://

### [Todo 6 ](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  appigotodo://

### [Bible](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  youversion://

### [PayPal](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  paypal://

### [Pandora Radio](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  pandora://

### [Currency](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  currency://

### [Movies by Flixster, with Rotten Tomatoes](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  flixster://

### [SplashID Safe Password Manager](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-06fps1zo86up2h9://

### [ウィズダム英和・和英辞典](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mkwisdom://

### [Remote](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  remote://

### [Outliner](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  outliner://

### [PCalc - The Best Calculator](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  pcalc://

### [Urbanspoon - Restaurant & Food Reviews](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  uspn://

### [Google Search](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  googleapp://

### [Bank of America - Mobile Banking](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  bofa://

### [NYTimes - Breaking National & World News](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  nytimes://

### [TripAdvisor Hotels Flights Restaurants](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  tripadvisor://

### [Facebook](https://itunes.apple.com/cn/app/id(null)?mt=8)



* Launch App  fb://
* Go To My Profile  fb://profile/
* Someone Else's Facebook Profile  fb://profile?id=${PROFILE}
* Facebook Page  fb://page?id=${PAGE}
* Facebook Group  fb://group?id=${GROUP}

### [Imangi](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  imangi://

### [AP Mobile](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb118162278248556five://

### [Yelp](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开APP  yelp4:
* Search Yelp  yelp4:///search?terms=${TERMS}&category=${CATEGORY}&location=${LOCATION}
* Open Business Page  yelp4:///biz/${BIZ_ID}
* Check In Nearby  yelp4:///check_in/nearby
* Check Ins  yelp4:///check_ins
* Check In Rankings  yelp4:///check_in/rankings

### [Molecules](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  molecules://

### [Car Care - fuel economy, mpg, gas mileage & service maintenance](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  carcare://

### [Byline](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  byline://

### [iXpenseIt](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ix://

### [Aftonbladet](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb128432323892318aftonbladet://

### [GuitarToolkit](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  guitartoolkit://

### [eniro.se](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  eniro://

### [BVG FahrInfo Plus Berlin](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fahrinfo-berlin://

### [Things](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  things:///

### [Hotels.com Hotel booking and last minute hotel deals](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  AdX-hotels1001://

### [SoundHound ∞ – Search, Discover, and Play Music](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb247047359503a://

### [NeoReader® - QR & Mobile Barcode Scanner](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  neoreader://

### [Mocha VNC](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mochavnc://

### [Mocha VNC Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mochavnc://

### [Shazam](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  shazam://

### [Check: Mobile bill pay, banking, money & credit card manager](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ionce://

### [Flashlight.](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  flashlight.://

### [ScanLife Barcode & QR Reader with Product Price Comparison, Coupons, & Reviews](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  scanlife://

### [Ambiance](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  amb://

### [Files Pro : Document & PDF Reader](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-um83ka2zph618eg://

### [NYC Subway 24-Hour KickMap](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  kmap://

### [IM+ Instant Messenger](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  implus://

### [theScore](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  thescore://

### [Crossword Light](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-qm7xh4l2fnoyujx://

### [mixi](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mixi://

### [Mantis Bible Study](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mantis://

### [Yahoo Sports](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ysportacular://

### [Air Hockey](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  airhockey://

### [Clinometer](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  clinometer://

### [Radio Javan](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb133218859477://

### [iTeleport Remote Desktop - VNC & RDP](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  iteleport://

### [Timer](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  timer://

### [Echofon for Twitter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  echofon://

### [Mocha Telnet Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mochatelnet://

### [Keeper® Password Manager & Digital Vault](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  keeper://

### [Bible+ Maps](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb363425330341082://

### [Frotz](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-nv5pml9vkxszw8r://

### [iSSH - SSH / VNC Console](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ssh://

### [GPS Kit - Offline GPS Tracker](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  geodata://

### [Measures - Unit and Currency Converter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  x-measures://

### [Grocery Gadget Shopping List - shop groceries, scan, sync share with family, track prices, save or use as checklist.](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  grocerygadget://

### [Stitcher Radio for Podcasts](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  stitcher://

### [iTranslate - translator & dictionary - translate 80+ languages](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  itranslate://

### [AeroWeather Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb185026994846079://

### [Wikipanion](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  wikipanion://

### [ShopShop - Shopping List](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  shopshop://

### [Remote Desktop - RDP Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mochavnc://

### [RadarScope](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  radarscope://

### [LinkedIn](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  linkedin://

### [Real Estate - Homes for Sale, Apartments for Rent](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb18357754166600://

### [imiwa? (Japanese dictionary)](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  kotoba://

### [Instapaper](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  instapaper://

### [DianHua Dictionary](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  dianhua://

### [Embark iBART - San Francisco BART](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  eklookup://

### [Tally Counter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  tallycounter://

### [Shopper Lite - Shopping List for Walmart, Costco, Home Depot Shopping](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  myshopperliteapp://

### [SaiSuke](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  saisuke://

### [Yummy](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  yummy://

### [Chess Game](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  memechess://

### [Simplenote](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  simplenote://

### [Blackjack Free](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb300894903378834://

### [Diner Dash Classic Deluxe](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com.ooi.dinerdash://

### [Yammer](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  yammer://

### [Pregnancy & Baby | What to Expect](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb289560144://

### [Mobile Mouse](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mobilemouse://

### [iRedTouch](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  iredt://

### [PDX Bus, MAX, Streetcar and WES](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  pdxbus://

### [White Noise](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb152524258096813full://

### [Shush](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  x-red-sweater-shush://

### [Air Sharing for iPhone & iPod touch](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  airsharing://

### [AroundMe](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb123448314320://

### [Notebook](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  appigonotebook://

### [Credit Card Terminal - Accept Payment with Mobile Point of Sale Reader](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com-innerfence-ccterminal://

### [Timewerks: Mobile Billing with PDF Invoice](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com-sorth-timewerks://

### [Currency Converter - Money Exchange Rates for more than 220 currencies!](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  currencyconverter://

### [Grocery iQ](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com-coupons-print://

### [iHeartRadio – Free Streaming Music & Internet AM/FM Radio Stations](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  iheartradio://

### [CashFlow](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-l3kwbhrw695lm4t://

### [Box for iPhone and iPad](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  box://

### [XpenseTracker - Expense Tracker & Mileage Log](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  xpensetracker://

### [Wikiamo](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  wikiamo://

### [fring](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fring://

### [Delivery Status touch, a package tracker](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  deliveries://

### [Olive Tree NIV Bible+](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb346110995416247://

### [Tap Forms Organizer and Secure Database](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  tapforms://

### [BeejiveIM with Push](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  beejiveim://

### [Holy Bible](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb143219889066960://

### [Run with Map My Run - GPS Running, Jog, Walk, Workout, Heart Rate, Sleep, Weight, Step and Activity Tracking, Coaching, and Calorie Counter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb43211574282://

### [GuitarStudio](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  guitarrx://

### [Map My Ride - GPS Cycling, Riding, Mountain Biking, and Workout Tracking](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mmride://

### [Geocaching](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  gcapp://

### [HT Professional Recorder](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  htpro://

### [Deezer Music](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  deezer://

### [Toodledo - To Do List](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  toodledo://

### [EleMints: Periodic Table](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  elemints://

### [WorldView by webcams.travel](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  worldview://

### [White Noise Lite: Relax. Sleep. Better.](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb152524258096813lite://

### [Omnio: Your personalized, all-in-one clinical resource](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  myskyscape://

### [HanDBase Database Manager](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  handbase://

### [Sonos Controller](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  sonos://

### [Remember The Milk](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  rtm://

### [iHandy Carpenter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ihandycarpenter://

### [Google Earth](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  comgoogleearth://

### [Internet Radio Box](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  radiobox://

### [Weightbot — Track your Weight in Style](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  weightbot://

### [iTalk Recorder](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-81yds93v7ardowg://

### [RainbowNote: notebook/diary with photo calendar](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  rainbownote://

### [Le Monde, l'info en continu](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  lemondeapp://

### [FOX Sports Mobile](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb120349781309793://

### [Files : Document & PDF Reader](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-xr3ymi0lhu8yn20://

### [SaiSuke FREE](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  saisukefree://

### [mCounter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com.mactips.mcounter.launch://

### [CashFlow Free](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-uibif0dvic8jiv8://

### [BigOven 350,000+ Recipes and Grocery List](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  favorite://

### [Corkz - Wine Reviews,Scanner, Cellar Management, Journal & Database](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  corkz://

### [Calc-12E RPN Financial Calculator](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  calc12e://

### [Cooliris](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb153426168085342://

### [WeatherPro](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  weatherpro://

### [TripView Sydney](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  TripView://

### [SBB Mobile](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  sbbmobileb2c://

### [Crazy Snowboard](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  Snowboard-plusplus://

### [Surf Report - Free daily reports and forecasts, tide charts, and beach weather conditions from Oakley, powered by Surfline](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  surfreport://

### [Star Walk™ - 5 Stars Astronomy Guide](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  starwalk://

### [Chess With Friends Free](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ChessWithFriends://

### [Flight Update - Live Flight Status](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  flightupdate://

### [The Weather Channel and weather.com - local forecasts, radar, and storm tracking](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  twcweather://

### [Subnet Calc](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  subnetcalc://

### [AutoScout24 Schweiz: Die Nummer 1 auf dem Schweizer Automarkt](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  as24iphone://

### [Gas Cubby - Fuel Economy & Service Log](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  gascubby://

### [ACTPrinter - Virtual Printer](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  phttp://

### [iTalk Recorder Premium](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  italk://

### [Bredbandskollen](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb314692708544://

### [iXpenseIt Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ix://

### [SkyBook](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  skybook://

### [OpenTable](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb123876194314735otiphone://

### [MomoNote](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  momonote://

### [ITmedia](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  itmedia://

### [iPeng Classic](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ipeng://

### [VLC Remote](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  vlcremote://

### [iComic -comic reader-](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  icohttp://

### [Lose It! – Weight Loss Program and Calorie Counter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  loseit://

### [Target](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  target://

### [Daijisen Jpn-Jpn Dictionary](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  daijisen://

### [Amazon App](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com.amazon.mobile.shopping://

### [The Snow Report](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb153994034631056://

### [Toobz-Free](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  a1f7b0af-bfb1-4d1d-8a8b-dda99d5081a7://

### [FileApp](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fileapp://://

### [NoteMaster - Amazing notes, synced with Dropbox or Google Drive](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  notemaster://

### [OldBooth](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb192242309827://

### [Tellmewhere : Restaurants Hotels Bars](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  tmw://

### [seeker](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  seeker://

### [Slacker Radio](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  slacker://

### [BatteryLog](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  batterylog://

### [ItemShelf](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  itemshelf://

### [産経新聞](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  sankeishimbun://

### [LimeChat - IRC Client](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  limechat://

### [BB2C](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  beebee2seeopen://

### [Cisco WebEx Meetings](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  wbx://

### [Map My Fitness - Workout Trainer for General Fitness, Running, Cycling, GPS, Step and Activity Tracking, Coaching, Weight, and Calorie Counter](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb44829295357://

### [Instaviz](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  instaviz://

### [大辞林](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mkdaijirin://

### [Westpac Mobile Banking](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  consultwbc://

### [Airports](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  airports://

### [Yahoo! JAPAN](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  yjipn://

### [Jelly SMS](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  jsms://

### [VLC Remote Free](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb175133809181991free://

### [Backgammon Free!](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  BackgammonLite-plusplus://

### [Call Notes](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  callnotes://

### [「乗換案内」無料の鉄道･バスルート検索･時刻表･運賃･列車運行情報･交通案内ナビゲーション](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  nrkjpaid://

### [WordsWorth Pro](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb84577438279://

### [Allrecipes Dinner Spinner](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb175712445801802://

### [HP ePrint](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  hpeprint://

### [PagesJaunes – Pour trouver bien plus que des coordonnées – Leader de la recherche locale de professionnels et annuaire téléphonique de particuliers partout en France](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb104830589607172://

### [iHandy Level Free](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ihandycarpenterlevel://

### [MotionX GPS](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  motionxgps://

### [SPORT1](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  kwsport1://

### [AccuWeather - Weather for Life](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb263111297051918://

### [iDownload](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  idownload://

### [Swiss Phone Book by local.ch](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  localch://

### [RunKeeper - GPS Running, Walk, Cycling, Workout and Weight Tracker](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb62572192129://

### [Headspace](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-cnc5sff8hjopebr://

### [ABC News](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb166722186711306://

### [Firetask - Project-oriented GTD Task Management for iPhone](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  firetask://

### [Lock 'n' Roll](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  locknroll://

### [CalenGoo](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  calengoo://

### [Photo fx](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb113287418691693://

### [MultiCam Philadelphia](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  multicamplusphiladelphia://

### [Speedtest.net Mobile Speed Test](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  speedtest://

### [楽天トラベル](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  rakutentravel://

### [ibisMail - Filtering Mail](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ibismail://

### [Groups: SMS, Mail and Manage Contacts](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  groups://

### [MultiCam BC Highway](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  multicamplusbchighway://

### [iShred](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ishredrx://

### [Kobo Reading App – Read Books and Magazines](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  kobo://

### [iGun Pro™ - The Original Gun Application](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb311385198923870full://

### [Ustream](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ustream://

### [Citi Mobile®](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  citiglobal://

### [Two Hundred Situps: Strengthen Your Core](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb192575334139712://

### [FahrInfo Stuttgart](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fahrinfo-stuttgart://

### [豊平文庫](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  kahouhei://

### [Skout - Meet, Chat, Friend](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  skout://

### [Kindle – Read Books, eBooks, Magazines, Newspapers & Textbooks](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  kindle://

### [ooTunes Radio - Recording and Alarm Clock!](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ootunes://

### [Trunk Notes Personal Wiki](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  tn://

### [GrubHub Food Delivery & Takeout](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  grubhub://

### [HopStop Transit Directions for iPhone](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  hopstop://

### [myHomework Student Planner](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb283058048395364://

### [2Do: Tasks Done in Style](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  twodo://

### [xkcd](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  xkcd://

### [Organizer for iPhone](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  organizer://

### [Audio Memos Free - The Voice Recorder](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  QuickVoice://

### [Yahoo](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  yahoofp://

### [Camera Genius](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb272128689676genius://

### [CashTrails with Sync - Expense and Income Tracker](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  cashtrailslite://

### [Papers](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  papers://

### [Skype](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开APP  skype:
* Call Someone  skype:${USER_ID}

### [Wedding Dash](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com.playfirst.weddingdashlite://

### [KAYAK Flights, Hotels & Cars](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  kayak://

### [Audioboo](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  audioboo://

### [Tumblr](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  tumblr://

### [MultiCam Alberta Highway](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  multicamalbertahighway://

### [Ambiance Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  amb://

### [CashTrails+ with Sync - Expense and Income Tracker](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  cashtrails://

### [Organizer Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  organizerlite://

### [SimpleMind+](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  simplemind://

### [Dictate + Connect (Dictamus)](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  dictateconnect://

### [Dictate + Connect Free (Dictamus Free)](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  dictateconnectfree://

### [Quran Reader](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  quranreader://

### [Match Dating - #1 App to Chat with Singles](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  match://

### [Eye-Fi](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  eyefi://

### [Lumen Trails Organizer+ Create a Daily Workout Timer, Calorie Counter, Journal, Exercise Tracker, Food Diary, Fitness Tracker, Diet Plan, Expense Tracker, Day Planner, GTD To-Do List, Checklist, Weight Loss Tracker, Sleep Time Log, Budget Tracker & More.](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  lumentrails://

### [Lumen Trails Planner+ Create a Daily Checklist, Money Tracker, Meal Planner, Health Diary, Time Tracker, Workout Plan, Photo Journal, Calendar Planner, Mileage Tracker, Flight Log, Body Weight Chart, Bill Tracker, Student Note Pad, Pill Reminder & More.](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  lumentrailslite://

### [GPS Log LITE](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  gpslog-gls://

### [MobiLinc Lite Insteon and X10 Controller](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb219570841417750://

### [FitnessBuilder](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fitnessbuilder://

### [Producteev by Jive - Task Management for Teams](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb113103452049605://

### [Wattpad - Free Books and eBook Reader - Read Fiction, Romance, Fanfiction stories](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  wattpad://

### [Drum Kit](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb104913711157://

### [MouthOff™](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  MouthOff://

### [Dog Whistler - Your Free Dog Whistle](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb213046138734358://

### [Free Translator - Translate English to Spanish, Persian and many more languages with Text, Speech and Dictionary](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  myL://

### [Pocket Universe: Virtual Sky Astronomy](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  astronomy://

### [Foursquare](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  foursquare://

### [MyDictionary](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  mydict://

### [Diner Dash](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com.playfirst.dinerdashlite://

### [Geocaching with Geosphere](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  geosphere://

### [CBS Sports](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  cbssports://

### [DIRECTV](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  directv://

### [Sudoku](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  com.genina.sudoku://

### [The New York Times Crossword](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  nytxwd://

### [HomeBudget Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  db-jo30ojpyypvtju7://

### [VIP Access for iPhone](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  vip://

### [Doodle Jump](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  doodlejump://

### [Relax with Andrew Johnson Lite](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ajrelaxlite://

### [Flashcards Deluxe](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fcd://

### [JotNot Pro | scan multipage documents to PDF](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  x-jotnotiphone://

### [TwitBird Premium](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  twitbird://

### [Tapatalk](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  tapatalk://

### [Fandango Movies – Times & Tickets](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb5885186655://

### [iBird Pro Guide to Birds](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  ibird8://

### [iCab Mobile](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  x-icabmobile://

### [YouMail Visual Voicemail](https://itunes.apple.com/cn/app/id(null)?mt=8)



* 打开  fb163973404916://
