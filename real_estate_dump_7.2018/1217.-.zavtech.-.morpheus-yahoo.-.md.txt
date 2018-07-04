## Disclaimer

**THIS PROJECT IS NOT AFFILIATED OR ENDORSED BY YAHOO AND IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, 
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR 
PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES 
OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION 
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE. DATA EXTRACTED USING THIS LIBRARY IS FOR PERSONAL 
NON-PROFESSIONAL USE AND MUST CONFORM TO YAHOO'S TERMS AND CONDITIONS**

## Yahoo Finance

### Introduction

[Yahoo Finance](https://finance.yahoo.com) is an excellent source of free market data and analytics covering both 
domestic and international markets. While not aimed at a professional user, it does offer a rich source of information 
that is invaluable to the **individual investor** at a price that cannot be beat, namely free! The Morpheus adapter 
for Yahoo Finance provides users a programmatic mechanism to capture some of this data for further analysis which
may be helpful for informing your own investment decisions. 

Yahoo Finance does not provide any officially supported APIs, so this adapter is essentially reverse engineered 
from the actions one can affect on the website itself. For that reason, the adapter could break at anytime, and 
could take some time to fix or perhaps become unsupportable altogether. Accordingly, the suggestion is to only 
rely on this code for personal non critical research projects.

## Data Access

The Morpheus Yahoo Finance adapter includes various `DataFrameSource` implementations that provide access to
**asset prices, asset returns, equity fundamentals, option prices and FX rates** using `DataFrames`. In particular, 
daily [historical quote](https://finance.yahoo.com/quote/BLK/history?p=BLK) bars (Open, High, Low, Close, Volume) in 
both **dividend adjusted** and **unadjusted** formats are available, as well as **intraday delayed quotes** while markets 
are trading. For those of you interested in [option](https://finance.yahoo.com/quote/BLK/options?p=BLK) markets, 
expiry dates given an underlying ticker are accessible along with intraday delayed quotes which include an **implied 
volatility estimate**. Finally, equity fundamental data can be accessed programmatically from the key [statistics page](https://finance.yahoo.com/quote/BLK/key-statistics?p=BLK)
of any security accessible on the site.

The following sections provide some useful examples of how to leverage the API and illustrate some commonly used 
techniques for analyzing portfolios of investment securities. Firstly, to leverage the library in your project, the 
following dependency should be included in your build tool of choice.

```xml
<dependency>
    <groupId>com.zavtech</groupId>
    <artifactId>morpheus-yahoo</artifactId>
    <version>${VERSION}</version>
</dependency>
```

There are two ways to integrate with the library, either via a convenience API which involves instantiating an 
instance of the `YahooFinance` class or by using the various `DataFrameSource` implementations directly. In the 
latter case, the sources should be pre-registered in some initializer as follows.

<?prettify?>
```java
static {
    DataFrameSource.register(new YahooOptionSource());
    DataFrameSource.register(new YahooQuoteHistorySource());
    DataFrameSource.register(new YahooQuoteLiveSource());
    DataFrameSource.register(new YahooReturnSource());
    DataFrameSource.register(new YahooStatsSource());
}
```

### Historical Quotes

For most securities represented on Yahoo Finance, it is possible to download historical quote bars into
a CSV file, and Morpheus leverages this same interface to capture **Open, High, Low, Close and Volume** data 
in a `DataFrame`. Historical price quotes are most often used to compute asset returns, so Yahoo presents these 
historical prices in both **dividend and split adjusted** terms making it easy to compute returns that incorporate 
these affects. The code below downloads split adjusted end of day quotes over the past 10 years for [BlackRock](https://finance.yahoo.com/quote/BLK/history?p=BLK), 
and plots the close price series.  

<?prettify?>
```java
String ticker = "BLK";
YahooQuoteHistorySource source = DataFrameSource.lookup(YahooQuoteHistorySource.class);

//Load end-of-day quote bars and select close price series
DataFrame<LocalDate,YahooField> closePrices = source.read(options -> {
    options.withStartDate(LocalDate.now().minusYears(10));
    options.withEndDate(LocalDate.now());
    options.withDividendAdjusted(true);
    options.withTicker(ticker);
}).cols().select(YahooField.PX_CLOSE);

//Create area plot of close prices
Chart.create().asSwing().withAreaPlot(closePrices, false, chart -> {
    chart.plot().axes().domain().label().withText("Date");
    chart.plot().axes().range(0).label().withText("Close Price");
    chart.title().withText(ticker + ": Close Prices (Last 10 Years)");
    chart.legend().off();
    chart.show();
});
```

<p align="center">
    <img class="chart" src="../../images/yahoo/blk_prices_1.png"/>
</p>

In the example we requested dividend adjusted prices which are convenient for computing returns, however
these are artificially changed and do not reflect actual observed prices at the time. To query for **unadjusted** 
prices simply pass `false` as the last parameter to `getQuoteBars()`. The code below pulls both adjusted and 
unadjusted prices, then selects the close prices from each frame and plots them for comparison. BlackRock is a 
high paying dividend stock, so we would expect to see material differences in the two price series.

<?prettify?>
```java
String ticker = "BLK";
YahooQuoteHistorySource source = DataFrameSource.lookup(YahooQuoteHistorySource.class);

//Load both adjusted and unadjusted quotes
DataFrame<LocalDate,String> frame = DataFrame.combineFirst(
    Stream.of("Adjusted", "Unadjusted").map(style -> source.read(options -> {
        options.withStartDate(LocalDate.now().minusYears(10));
        options.withEndDate(LocalDate.now());
        options.withDividendAdjusted(style.equals("Adjusted"));
        options.withTicker(ticker);
    }).cols().select(YahooField.PX_CLOSE).cols().mapKeys(column -> style))
);

//Plot close prices from both these series
Chart.create().asSwing().withLinePlot(frame, chart -> {
    chart.plot().axes().domain().label().withText("Date");
    chart.plot().axes().range(0).label().withText("Close Price");
    chart.title().withText(ticker + ": Adjusted & Unadjusted Close Prices");
    chart.legend().bottom();
    chart.show();
});
```

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/blk_prices_2.png"/>
</p>

[Netflix](https://finance.yahoo.com/chart/NFLX) currently does not pay a dividend, so if we ran this code for NFLX, 
the two series should be coincident.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/nflx_prices_1.png"/>
</p>

### Asset Returns

Investment decisions fundamentally boil down to making a judgement call regarding future asset returns, and the likely
volatility of those returns over the investment horizon. While Yahoo Finance does not provide an API to directly download
asset returns, the ability to capture dividend and split adjusted prices makes it very easy to compute returns. The Morpheus
adapter for Yahoo Finance provides an API to calculate **daily**, **weekly**, **monthly** and **cumulative** returns as 
demonstrated in the following sections.

#### Cumulative Returns

Consider 6 major asset classes, namely Emerging Market Equities, Real-Estate, International Equities (outside US), Commodities,
Large Blend and Fixed Income. The returns for these asset classes can be proxied using well known liquid ETFs from the likes
of [Vanguard](https://investor.vanguard.com/home/), [BlackRock](https://www.blackrock.com/) or [State Street Global Advisors](https://www.ssga.com/home.html) 
among others. For this example, let's use the following tickers.

| Ticker | Name                                     | Provider    |                                                               |
|--------|------------------------------------------|-------------|---------------------------------------------------------------|
| VWO    | Vanguard FTSE Emerging Markets ETF       | Vanguard    | [Details](https://finance.yahoo.com/quote/VWO/profile?p=VWO)  |   
| VNQ    | Vanguard REIT ETF                        | Vanguard    | [Details](https://finance.yahoo.com/quote/VNQ/profile?p=VNQ)  |
| VEA    | Vanguard FTSE Developed Markets ETF      | Vanguard    | [Details](https://finance.yahoo.com/quote/VEA/profile?p=VEA)  |
| DBC    | PowerShares DB Commodity Tracking ETF    | Powershares | [Details](https://finance.yahoo.com/quote/DBC/profile?p=DBC)  |
| VTI    | Vanguard Total Stock Market ETF          | Vanguard    | [Details](https://finance.yahoo.com/quote/DBC/profile?p=VTI)  |
| BND    | Vanguard Total Bond Market ETF           | Vanguard    | [Details](https://finance.yahoo.com/quote/BND/profile?p=BND)  |
 
The code below demonstrates how to use the `YahooReturnSource` to calculate **cumulative returns** for these tickers including 
the effect of any splits and dividend payments. To make the plot more user friendly, we re-label the columns as asset class 
names rather than the ticker symbols.
  
<?prettify?>
```java
YahooReturnSource source = DataFrameSource.lookup(YahooReturnSource.class);
DataFrame<LocalDate,String> returns = source.read(options -> {
    options.withStartDate(LocalDate.now().minusYears(10));
    options.withEndDate(LocalDate.now());
    options.withTickers("VWO", "VNQ", "VEA", "DBC", "VTI", "BND");
    options.cumulative();
}).cols().mapKeys(column -> {
    switch (column.key()) {
        case "VWO": return "EM Equities";
        case "VNQ": return "Real-estate";
        case "VEA": return "Foreign Equity";
        case "DBC": return "Commodities";
        case "VTI": return "Large Blend";
        case "BND": return "Fixed Income";
        default:    return column.key();
    }
}).applyDoubles(v -> {
    return v.getDouble() * 100d;
});

Chart.create().asSwing().withLinePlot(returns, chart -> {
    chart.title().withText("Major Asset Class Cumulative Returns Last 10 Years (ETF Proxies)");
    chart.plot().axes().domain().label().withText("Date");
    chart.plot().axes().range(0).label().withText("Return");
    chart.plot().axes().range(0).format().withPattern("0.##'%';-0.##'%'");
    chart.legend().on().bottom();
    chart.show();
});
```

Some of the potential take aways from this chart are as follows:
    
* **Fixed Income** returns are much less volatile than the other asset classes in the plot.
* Everything except Fixed Income got crushed in the 2007/2008 **Global Financial Crisis (GFC)**
* **Commodities** have been a terrible investment over the past 10 years.
* **EM** & **International** Equities have only recently gone positive over the past 10 years.
* VTI, the **broadest** of all the funds, has out performed over the past 10 years.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/asset_returns_1.png"/>
</p>

#### Smoothed Returns

On a day-to-day basis, market prices are extremely noisy and for the most part completely random. It is often useful to 
remove some of this noise by smoothing the returns, which in turn develops a more stable signal which can be consumed by 
a systematic investment process. The Morpheus adapter supports smoothing returns based on an [Exponential Weighted Moving Average](https://en.wikipedia.org/wiki/Exponential_smoothing) 
(EWMA) which is a commonly used technique in signal processing.

The code below generates cumulative returns for the **S&P 500 Index** tracker with ticker symbol [SPY](https://finance.yahoo.com/quote/SPY?p=SPY), 
and smooths the data with various half-lives, namely 0, 5, 10, 30 and 60 business days. A 0 day half-life is interpreted as 
no smoothing, so this simply yields the raw data. The smoothed signal is computed as follows:

<p align="center">
    <img class="chart" src="./images/equation-1.png"/>
</p>

There are various ways to compute \\( \alpha \\), but in Morpheus we calculate it based on a half-life as follows:
 
<p align="center">
    <img class="chart" src="./images/equation-2.png"/>
</p>

<?prettify?>
```java
String ticker = "SPY";
YahooReturnSource source = DataFrameSource.lookup(YahooReturnSource.class);
Array<Integer> halfLives = Array.of(0, 5, 10, 30, 60);
DataFrame<LocalDate,String> frame = DataFrame.combineFirst(halfLives.map(halfLife -> {
    return source.read(options -> {
        options.withStartDate(LocalDate.now().minusYears(5));
        options.withEndDate(LocalDate.now());
        options.withTickers(ticker);
        options.withEmaHalfLife(halfLife.getInt());
        options.cumulative();
    }).cols().replaceKey(ticker, String.format("%s(%s)", ticker, halfLife.getInt()));
}));

Chart.create().withLinePlot(frame.applyDoubles(v -> v.getDouble() * 100d), chart -> {
    chart.title().withText(String.format("%s EWMA Smoothed Returns With Various Half-Lives", ticker));
    chart.plot().axes().domain().label().withText("Date");
    chart.plot().axes().range(0).label().withText("Return");
    chart.plot().axes().range(0).format().withPattern("0.##'%';-0.##'%'");
    chart.legend().on().bottom();
    chart.show();
});
```
It's clear from the plot below that the larger the half-life the more smoothing is applied, which makes sense
based on the expression for half-life above.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/spy_returns_1.png"/>
</p>

#### Return Distribution

Many of the statistical techniques in modern finance are predicated on the assumption that asset returns are **normally 
distributed**. However, it is often the case that returns are not normal, which is why during the GFC many funds experienced 
greater than -6 sigma events one day after the next. While returns are not normal, the statistical techniques that are commonly 
used are still a reasonable engineering approximation when markets are *not* under stress. When they are under stress, all bets 
are off (no pun intended), which can lead to bad outcomes for investors.

The code below computes daily returns for the S&P 500 ETF tracker with ticker symbol SPY over the past 20 years, and then generates 
a histogram of these returns using 200 bins. In addition, the mean and standard deviation of these daily returns are calculated. 
They are then used to compute a normal probability density function which is scaled appropriately and then overlaid on the chart. 

<?prettify?>
```java
String ticker = "SPY";
YahooReturnSource source = DataFrameSource.lookup(YahooReturnSource.class);
DataFrame<LocalDate,String> returns = source.read(options -> {
    options.withStartDate(LocalDate.now().minusYears(20));
    options.withEndDate(LocalDate.now());
    options.withTickers(ticker);
}).applyDoubles(v -> {
    return v.getDouble() * 1d;
});

double binCount = 200;
double min = returns.stats().min();
double max = returns.stats().max();
double mean = returns.stats().mean();
double stdDev = returns.stats().stdDev();
double bound = Math.max(Math.abs(min), Math.abs(max));
double scale = ((max - min) / binCount) * returns.stats().count();
DataFrame<Double,String> normDist = normal("NDIST", -bound, bound, (int)binCount, mean, stdDev, scale);

Chart.create().withHistPlot(returns, (int)binCount, chart -> {
    chart.title().withText(ticker + ": Daily Return Frequency Distribution");
    chart.subtitle().withText(ticker + " Returns over past 20 years");
    chart.plot().<String>data().add(normDist);
    chart.plot().style("NDIST").withColor(Color.BLACK).withLineWidth(2f);
    chart.plot().render(1).withLines(false, false);
    chart.plot().axes().domain().label().withText("Return");
    chart.plot().axes().domain().format().withPattern("0.00'%';-0.00'%'");
    chart.plot().axes().range(0).label().withText("Frequency");
    chart.show();
});
```

A couple of features regarding the fit standout immediately, namely that the actual distribution has a **higher central peak** and
the **shoulders are a bit narrower**. The standard deviation of SPY daily returns over the past 20 years comes out to be 1.239%, and
the plot suggests that the fit is a reasonable approximation between +/-3%, or say a little less than **+/-2.5 standard deviations 
(2.5 sigma)**. The fitted distribution predicts that a -2.5 sigma event, or a one day drop in the S&P 500 of approximately -3.1% has 
a probability of 0.5733%, which on the assumption of **252 trading days a year** is likely to happen once in 175 days or about 1.44 
times per year. This is not inconsistent with the actual frequency distribution as shown in the second plot below, which is zoomed 
into the left side of the distribution inorder to magnify this part of the plot.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/return_dist_1.png"/>
</p>

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/return_dist_2.png"/>
</p>

Where the normal distribution is a wholly **inadequate model** is in the space beyond +/- 2.5 sigma. As mentioned earlier, many funds 
experienced -6 sigma events or greater during the global financial crisis, day after day. The S&P 500 fitted distribution presented
above suggests that such an extreme event is likely to occur with a probability of 8.2934E-8% implying it **should only happen once
in 4,784,799 years!**  The plot below zooms into the left tail of the distribution demonstrating that extreme events occur far more
frequently than a normal distribution would suggest.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/return_dist_3.png"/>
</p>

In the above example we leverage a function called `normal()` to generate a scaled normal distribution that we can superimpose on 
the plot to get a sense of how well the return histogram fits such a model. The code below simply generates a normal curve given 
the mean, standard deviation of the daily returns, with an appropriate scale factor to fit the histogram.

<p align="center">
    <img class="chart" src="./images/equation-3.png"/>
</p>

<?prettify?>
```java
/**
 * Returns a single column DataFrame containing values generated from a normal distribution probability density function
 * @param label     the column key for the PDF series
 * @param lower     the lower bound for PDF
 * @param upper     the upper bound for PDF
 * @param count     the number of values to include
 * @param mean      the mean for the distribution
 * @param sigma     the standard deviation for the distribution
 * @return          the DataFrame of Normal PDF values
 */
@SuppressWarnings("unchecked")
<C> DataFrame<Double,C> normal(C label, double lower, double upper, int count, double mean, double sigma, double scale) {
    final double stepSize = (upper - lower) / (double)count;
    final Range<Double> xValues = Range.of(lower, upper, stepSize);
    return DataFrame.of(xValues, (Class<C>)label.getClass(), columns -> {
        columns.add(label, xValues.map(x -> {
            final double part1 = 1d / (sigma * Math.sqrt(2d * Math.PI));
            final double part2 = Math.exp(-Math.pow(x - mean, 2d) / (2d * Math.pow(sigma, 2d)));
            return part1 * part2;
        }));
    }).applyDoubles(v -> {
        return v.getDouble() * scale;
    });
}
```

#### Return Distribution (Smoothed)

Consider the same setup as in the prior example, but in this case we look at the frequency distribution of daily returns after they 
have been **exponentially smoothed** with a 20 day half-life. De-noising the returns does not yield a better fit, and the positive 
skew in the distribution becomes more apparent. In addition, while there is a positive skew, it is also clear that smoothing the
returns highlights far **more negative extreme events** than positive events.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/return_dist_4.png"/>
</p>

<?prettify?>
```java
String ticker = "SPY";
int halfLife = 20;
YahooReturnSource source = DataFrameSource.lookup(YahooReturnSource.class);
DataFrame<LocalDate,String> returns = source.read(options -> {
    options.withStartDate(LocalDate.now().minusYears(10));
    options.withEndDate(LocalDate.now());
    options.withTickers(ticker);
    options.withEmaHalfLife(halfLife);
}).applyDoubles(v -> {
    return v.getDouble() * 100d;
});

double binCount = 200;
double min = returns.stats().min();
double max = returns.stats().max();
double mean = returns.stats().mean();
double stdDev = returns.stats().stdDev();
double bound = Math.max(Math.abs(min), Math.abs(max));
double scale = ((max - min) / binCount) * returns.stats().count();
DataFrame<Double,String> normDist = normal("NDIST", -bound, bound, (int)binCount, mean, stdDev, scale);

Chart.create().withHistPlot(returns, (int)binCount, chart -> {
    chart.title().withText(String.format("%s: Smoothed Daily Return Distribution (HL: %s)", ticker, halfLife));
    chart.plot().<String>data().add(normDist);
    chart.plot().style("NDIST").withColor(Color.BLACK).withLineWidth(2f);
    chart.plot().render(1).withLines(false, false);
    chart.plot().axes().domain().label().withText("Return");
    chart.plot().axes().domain().format().withPattern("0.00'%';-0.00'%'");
    chart.plot().axes().range(0).label().withText("Frequency");
    chart.show();
});
```

### Latest Quotes

Accessing a snapshot of the most recent data for one or more securities can be done via a single call using the `YahooQuoteLiveSource`
as shown below. In this example, we request the most recent data for several tickers, and we are presented with a `DataFrame` 
containing all available fields as columns. When accessing this data outside of market hours, fields such as the bid/ask price 
and size will often show NaN values. The resulting `DataFrame` is keyed by the security ticker along the row axis and `YahooField` 
along the column axis allowing fast access to elements of the frame. 

<?prettify?>
```java
YahooQuoteLiveSource source = DataFrameSource.lookup(YahooQuoteLiveSource.class);
DataFrame<String, YahooField> quotes = source.read(options -> {
    options.withTickers("AAPL", "BLK", "NFLX", "ORCL", "GS", "C", "GOOGL", "MSFT", "AMZN");
});
```

<pre class="frame">
 Index  |  TICKER  |               NAME                |   PX_BID   |  PX_BID_SIZE  |   PX_ASK   |  PX_ASK_SIZE  |    PX_VOLUME    |  PX_CHANGE  |  PX_CHANGE_PERCENT  |  PX_LAST_DATE  |  PX_LAST_TIME  |  PX_LAST   |  PX_LAST_SIZE  |   PX_LOW   |  PX_HIGH   |  PX_PREVIOUS_CLOSE  |  PX_OPEN   |  EXCHANGE  |  AVG_DAILY_VOLUME  |  TRADE_DATE  |  DIVIDEND_PER_SHARE  |    EPS    |  EPS_ESTIMATE  |  EPS_NEXT_YEAR  |  EPS_NEXT_QUARTER  |   FLOAT_SHARES    |  FIFTY_TWO_WEEK_LOW  |  ANNUALISED_GAIN  |     MARKET_CAP      |       EBITDA       |  PRICE_SALES_RATIO  |  PRICE_BOOK_RATIO  |  EX_DIVIDEND_DATE  |  PRICE_EARNINGS_RATIO  |  DIVIDEND_PAY_DATE  |  PEG_RATIO  |  PRICE_EPS_RATIO_CURRENT_YEAR  |  PRICE_EPS_RATIO_NEXT_YEAR  |  SHORT_RATIO  |
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  AAPL  |    AAPL  |                       Apple Inc.  |  160.9400  |    1500.0000  |  161.0000  |     800.0000  |  71714046.0000  |    -0.6400  |            -0.0040  |    2017-09-12  |      16:00:00  |  160.8600  |      100.0000  |  158.7700  |  163.9600  |           161.5000  |  162.6100  |       NMS  |     26754500.0000  |        null  |              2.5200  |   8.8100  |        9.0200  |        10.8900  |            3.8400  |  5031913000.0000  |            104.0800  |              NaN  |  830880000000.0000  |  70210000000.0000  |             3.7300  |            6.3000  |        2017-08-10  |               18.2600  |         2017-08-17  |     1.5900  |                       17.8300  |                    14.7700  |       1.9000  |
   BLK  |     BLK  |                  BlackRock, Inc.  |       NaN  |          NaN  |       NaN  |          NaN  |    333885.0000  |     4.5300  |             0.0107  |    2017-09-12  |      16:02:00  |  428.5700  |    38358.0000  |  424.6900  |  428.7000  |           424.0400  |  426.1400  |       NYQ  |       513127.0000  |        null  |             10.0000  |  20.8300  |       21.8200  |        24.9100  |            5.8200  |   123755000.0000  |            336.8400  |              NaN  |   69520000000.0000  |   5060000000.0000  |             5.9700  |            2.3300  |        2017-08-31  |               20.5700  |         2017-09-22  |     1.3700  |                       19.6400  |                    17.2000  |       3.1800  |
  NFLX  |    NFLX  |                    Netflix, Inc.  |  185.0600  |     500.0000  |  185.6700  |     200.0000  |   6689568.0000  |     3.4100  |             0.0188  |    2017-09-12  |      16:00:00  |  185.1500  |   199365.0000  |  180.6400  |  185.3300  |           181.7400  |  182.5500  |       NMS  |      7144270.0000  |        null  |                 NaN  |   0.8200  |        1.1900  |         2.0200  |            0.3100  |   424846000.0000  |             93.2600  |              NaN  |   79940000000.0000  |    706920000.0000  |             7.7000  |           25.2100  |              null  |              225.2400  |               null  |     1.9700  |                      155.5900  |                    91.6600  |       3.0700  |
  ORCL  |    ORCL  |               Oracle Corporation  |       NaN  |          NaN  |       NaN  |          NaN  |  13352387.0000  |     0.2800  |             0.0053  |    2017-09-12  |      16:01:00  |   52.7700  |   839129.0000  |   52.4700  |   52.8900  |            52.4900  |   52.6400  |       NYQ  |     13043800.0000  |        null  |              0.7600  |   2.2100  |        2.9500  |         3.1900  |            0.6900  |  3009105000.0000  |             37.6200  |              NaN  |  218290000000.0000  |  14670000000.0000  |             5.7600  |            4.0300  |        2017-07-17  |               23.8800  |         2017-08-02  |     1.9400  |                       17.8900  |                    16.5400  |       1.8400  |
    GS  |      GS  |  Goldman Sachs Group, Inc. (The)  |       NaN  |          NaN  |       NaN  |          NaN  |   3745841.0000  |     4.8900  |             0.0221  |    2017-09-12  |      16:00:00  |  225.9500  |   160193.0000  |  222.0200  |  227.6900  |           221.0600  |  222.5400  |       NYQ  |      3043750.0000  |        null  |              3.0000  |  19.0700  |       18.2300  |        19.9700  |            5.0400  |   350537000.0000  |            157.7700  |              NaN  |   87720000000.0000  |            0.0000  |             2.6600  |            1.1400  |        2017-08-29  |               11.8500  |         2017-09-28  |     1.0600  |                       12.3900  |                    11.3100  |       1.2700  |
     C  |       C  |                  Citigroup, Inc.  |       NaN  |          NaN  |       NaN  |          NaN  |  15495439.0000  |     1.0800  |             0.0160  |    2017-09-12  |      16:00:00  |   68.7900  |  1090112.0000  |   68.1000  |   69.2500  |            67.7100  |   68.2200  |       NYQ  |     16707800.0000  |        null  |              0.8000  |   4.9900  |        5.2200  |         5.9600  |            1.2900  |  2721749000.0000  |             45.1600  |              NaN  |  187420000000.0000  |            0.0000  |             2.8700  |            0.8800  |        2017-08-03  |               13.7700  |         2017-08-25  |     1.2700  |                       13.1800  |                    11.5400  |       0.0200  |
 GOOGL  |   GOOGL  |                    Alphabet Inc.  |  946.0100  |     100.0000  |  947.2300  |     100.0000  |   1284787.0000  |     3.3600  |             0.0036  |    2017-09-12  |      16:00:00  |  946.6500  |   113174.0000  |  937.5000  |  948.0900  |           943.2900  |  946.9200  |       NMS  |      1773140.0000  |        null  |                 NaN  |  27.5900  |       30.5900  |        39.9900  |            9.6000  |   600581000.0000  |            743.5900  |              NaN  |  655910000000.0000  |  32250000000.0000  |             6.5800  |            4.4100  |              null  |               34.3100  |               null  |     1.6200  |                       30.9500  |                    23.6700  |       1.4500  |
  MSFT  |    MSFT  |            Microsoft Corporation  |   74.6800  |     500.0000  |   74.9300  |     100.0000  |  14394850.0000  |    -0.0800  |            -0.0011  |    2017-09-12  |      16:00:00  |   74.6800  |  1682458.0000  |   74.3700  |   75.2400  |            74.7600  |   74.7600  |       NMS  |     22427700.0000  |        null  |              1.5600  |   2.7100  |        3.1700  |         3.5600  |            0.8300  |  7595028000.0000  |             55.9800  |              NaN  |  575200000000.0000  |  30430000000.0000  |             6.4000  |            7.9600  |        2017-08-15  |               27.5600  |         2017-09-14  |     2.3500  |                       23.5600  |                    20.9800  |       1.9500  |
  AMZN  |    AMZN  |                 Amazon.com, Inc.  |  982.8700  |     100.0000  |  985.0000  |     200.0000  |   2481066.0000  |     4.6200  |             0.0047  |    2017-09-12  |      16:00:00  |  982.5800  |    99104.0000  |  975.5200  |  984.6700  |           977.9600  |  983.2700  |       NMS  |      3773170.0000  |        null  |                 NaN  |   3.9300  |        3.9900  |         8.1800  |            1.7700  |   400088000.0000  |            710.1000  |              NaN  |  472010000000.0000  |  12300000000.0000  |             3.1300  |           20.2200  |              null  |              249.8900  |               null  |     6.3700  |                      246.2600  |                   120.1200  |       1.2100  |
</pre>

Data from this frame can be accessed in a **type safe** manner as follows:

<?prettify?>
```java
String name = quotes.data().getValue("AAPL", YahooField.NAME);
double closePrice = quotes.data().getDouble("AAPL", YahooField.PX_LAST);
LocalDate date = quotes.data().getValue("AAPL", YahooField.PX_LAST_DATE);
```

Usually not all these fields are desired so specific fields can be requested as follows:

<?prettify?>
```java
YahooQuoteLiveSource source = DataFrameSource.lookup(YahooQuoteLiveSource.class);
DataFrame<String, YahooField> quotes = source.read(options -> {
    options.withTickers("AAPL", "BLK", "NFLX", "ORCL", "GS", "C", "GOOGL", "MSFT", "AMZN");
    options.withFields(
        YahooField.PX_LAST,
        YahooField.PX_BID,
        YahooField.PX_ASK,
        YahooField.PX_VOLUME,
        YahooField.PX_CHANGE,
        YahooField.PX_LAST_DATE,
        YahooField.PX_LAST_TIME
    );
});
```

<pre class="frame">
 Index  |  PX_LAST   |   PX_BID   |   PX_ASK   |    PX_VOLUME    |  PX_CHANGE  |  PX_LAST_DATE  |  PX_LAST_TIME  |
------------------------------------------------------------------------------------------------------------------
  AAPL  |  160.8600  |  160.9400  |  161.0000  |  71714046.0000  |    -0.6400  |    2017-09-12  |      16:00:00  |
   BLK  |  428.5700  |       NaN  |       NaN  |    333885.0000  |     4.5300  |    2017-09-12  |      16:02:00  |
  NFLX  |  185.1500  |  185.0600  |  185.6700  |   6689568.0000  |     3.4100  |    2017-09-12  |      16:00:00  |
  ORCL  |   52.7700  |       NaN  |       NaN  |  13352387.0000  |     0.2800  |    2017-09-12  |      16:01:00  |
    GS  |  225.9500  |       NaN  |       NaN  |   3745841.0000  |     4.8900  |    2017-09-12  |      16:00:00  |
     C  |   68.7900  |       NaN  |       NaN  |  15495439.0000  |     1.0800  |    2017-09-12  |      16:00:00  |
 GOOGL  |  946.6500  |  946.0100  |  947.2300  |   1284787.0000  |     3.3600  |    2017-09-12  |      16:00:00  |
  MSFT  |   74.6800  |   74.6800  |   74.9300  |  14394850.0000  |    -0.0800  |    2017-09-12  |      16:00:00  |
  AMZN  |  982.5800  |  982.8700  |  985.0000  |   2481066.0000  |     4.6200  |    2017-09-12  |      16:00:00  |
</pre>

### Option Quotes

Market data for listed [Options](https://en.wikipedia.org/wiki/Option_(finance)) on equities and ETFs is also accessible from 
Yahoo Finance (for example, listed options on Apple can be accessed [here](https://finance.yahoo.com/quote/AAPL/options?p=AAPL)). 
It is not clear that Yahoo provides a CSV API for this data, so the Morpheus Adapter screen scrapes the relevant information from 
the HTML page, which obviously makes it somewhat sensitive to changes in the page style.

The code below demonstrates how to query for the **expiry dates** on options given the underlying security symbol. It then
selects the next upcoming expiry date, and queries for all options, including **calls and puts** for this expiry.

<?prettify?>
```java
String ticker = "SPY";
YahooFinance yahoo = new YahooFinance();
Set<LocalDate> expiryDates = yahoo.getOptionExpiryDates(ticker);
LocalDate nextExpiry = expiryDates.iterator().next();
DataFrame<String,YahooField> optionQuotes = yahoo.getOptionQuotes(ticker, nextExpiry);
```

**Calls and puts** can easily be separated by filtering the Morpheus `DataFrame` in the usual fashion as shown below.

<?prettify?>
```java
//Select rows representing CALL options
DataFrame<String,YahooField> calls = optionQuotes.rows().select(row -> {
    final String type = row.getValue(YahooField.OPTION_TYPE);
    return type.equalsIgnoreCase("Call");
});
```

<pre class="frame">
       Index         |  TICKER  |  OPTION_TYPE  |  EXPIRY_DATE  |  PX_STRIKE  |  PX_LAST   |  PX_CHANGE  |  PX_CHANGE_PERCENT  |   PX_BID   |   PX_ASK   |  PX_VOLUME   |  OPEN_INTEREST  |  IMPLIED_VOLATILITY  |
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 SPY170915C00050000  |     SPY  |         CALL  |   2017-09-15  |    50.0000  |  187.5000  |     0.0000  |                NaN  |  186.0900  |  189.2100  |      1.0000  |         0.0000  |              0.0000  |
 SPY170915C00055000  |     SPY  |         CALL  |   2017-09-15  |    55.0000  |  195.0100  |     3.0300  |             0.0158  |  193.1200  |  197.1800  |     56.0000  |       686.0000  |             10.7500  |
 SPY170915C00060000  |     SPY  |         CALL  |   2017-09-15  |    60.0000  |  190.0900  |     3.1200  |             0.0167  |  188.1200  |  192.1300  |     38.0000  |       617.0000  |              9.7188  |
 SPY170915C00065000  |     SPY  |         CALL  |   2017-09-15  |    65.0000  |  185.1500  |     5.5800  |             0.0311  |  183.1200  |  187.2600  |     52.0000  |       390.0000  |             10.0625  |
 SPY170915C00070000  |     SPY  |         CALL  |   2017-09-15  |    70.0000  |  180.1100  |     2.2700  |             0.0128  |  178.0000  |  182.2000  |     67.0000  |       142.0000  |              8.0625  |
 SPY170915C00075000  |     SPY  |         CALL  |   2017-09-15  |    75.0000  |  175.0800  |     6.3200  |             0.0374  |  173.0000  |  177.0300  |     18.0000  |       138.0000  |             13.9258  |
 SPY170915C00080000  |     SPY  |         CALL  |   2017-09-15  |    80.0000  |  170.0800  |     6.1700  |             0.0376  |  168.0000  |  172.2500  |     25.0000  |        59.0000  |              7.8125  |
 SPY170915C00085000  |     SPY  |         CALL  |   2017-09-15  |    85.0000  |  165.1500  |     6.0600  |             0.0381  |  163.0000  |  167.0900  |     13.0000  |       182.0000  |             12.6523  |
 SPY170915C00090000  |     SPY  |         CALL  |   2017-09-15  |    90.0000  |  160.0800  |     8.3800  |             0.0552  |  158.0000  |  162.2200  |      8.0000  |       180.0000  |              6.7500  |
 SPY170915C00095000  |     SPY  |         CALL  |   2017-09-15  |    95.0000  |  155.0800  |     6.1700  |             0.0414  |  153.0000  |  157.2000  |      4.0000  |        55.0000  |              6.1875  |
</pre>

<?prettify?>
```java
//Select rows representing PUT options
DataFrame<String,YahooField> puts = optionQuotes.rows().select(row -> {
    final String type = row.getValue(YahooField.OPTION_TYPE);
    return type.equalsIgnoreCase("Put");
});
```

<pre class="frame">
       Index         |  TICKER  |  OPTION_TYPE  |  EXPIRY_DATE  |  PX_STRIKE  |  PX_LAST  |  PX_CHANGE  |  PX_CHANGE_PERCENT  |  PX_BID  |  PX_ASK  |  PX_VOLUME   |  OPEN_INTEREST  |  IMPLIED_VOLATILITY  |
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 SPY170915P00055000  |     SPY  |          PUT  |   2017-09-15  |    55.0000  |   0.0200  |     0.0000  |                NaN  |  0.0000  |  0.0100  |     10.0000  |      2250.0000  |              8.5000  |
 SPY170915P00060000  |     SPY  |          PUT  |   2017-09-15  |    60.0000  |   0.0200  |     0.0000  |                NaN  |  0.0000  |  0.0100  |     50.0000  |      1912.0000  |              8.0000  |
 SPY170915P00065000  |     SPY  |          PUT  |   2017-09-15  |    65.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |     10.0000  |      4117.0000  |              7.7500  |
 SPY170915P00070000  |     SPY  |          PUT  |   2017-09-15  |    70.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |      5.0000  |      8582.0000  |              7.2500  |
 SPY170915P00075000  |     SPY  |          PUT  |   2017-09-15  |    75.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |      1.0000  |      5598.0000  |              6.8750  |
 SPY170915P00080000  |     SPY  |          PUT  |   2017-09-15  |    80.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |    150.0000  |      3061.0000  |              6.5000  |
 SPY170915P00085000  |     SPY  |          PUT  |   2017-09-15  |    85.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |     14.0000  |      5525.0000  |              6.1250  |
 SPY170915P00090000  |     SPY  |          PUT  |   2017-09-15  |    90.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |      2.0000  |      5638.0000  |              5.8750  |
 SPY170915P00095000  |     SPY  |          PUT  |   2017-09-15  |    95.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |     50.0000  |     22290.0000  |              5.5000  |
 SPY170915P00100000  |     SPY  |          PUT  |   2017-09-15  |   100.0000  |   0.0100  |     0.0000  |                NaN  |  0.0000  |  0.0100  |     99.0000  |     19382.0000  |              5.2500  |
</pre>

#### Volatility Smile

One of the most influential inputs to the famous [Black-Scholes-Merton](https://en.wikipedia.org/wiki/Black%E2%80%93Scholes_model) 
option pricing model concerns the future volatility of the returns on the underlying asset. In fact, volatility is so fundamental to 
option pricing that certain types of option contracts are quoted in volatility units rather than price. Black-Scholes assumes that 
the volatility of the underlying returns are constant over the term in question, and it also assumes that other characteristics of 
the option such as the moneyness (how far in or out-of-the-money the option might be), do not influence estimates of future volatility.

In reality, this does not appear to be the case based on observed market prices. A commonly used visualization in option trading is 
called the **Option Volatility Smile**, which plots **implied volatilities** of options with different **strike prices** for the same 
expiry date. According to Black-Scholes, these curves should be flat, but in reality they form more of a curve in the shape of a 
person smiling. That is, implied volatilities for **at-the-money** options tend to be lower than for deep **in-the-money** or deep 
**out-the-money** options.

The plot below illustrates the volatility smiles for options on the S&P 500 ETF with ticker symbol SPY which has been generated
using the Morpheus Yahoo Finance adapter. While various **outliers** appear to exist, the smile pattern is pretty clear. These outliers 
are likely to be explained by low volume at the strike prices in question, so the calculated implied volatilities are stale at those
points. The other possibility is a mis-pricing of some options at these strikes, but that is fairly unlikely as such differences would 
be quickly arbitraged away. The code to generate this plot is also shown below.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/option_call_smile.png"/>
</p>

<?prettify?>
```java
String ticker = "SPY";
//Instantiate Yahoo convenience adapter
YahooFinance yahoo = new YahooFinance();
//Select last price for underlying
double lastPrice = yahoo.getLiveQuotes(Array.of(ticker)).data().getDouble(0, YahooField.PX_LAST);
//Select call options with strike price within 10% of current market price and non zero vol
DataFrame<String,YahooField> options = yahoo.getOptionQuotes(ticker).rows().select(row -> {
    final String type = row.getValue(YahooField.OPTION_TYPE);
    if (!type.equalsIgnoreCase("CALL")) {
        return false;
    } else {
        final double strike = row.getDouble(YahooField.PX_STRIKE);
        final double impliedVol = row.getDouble(YahooField.IMPLIED_VOLATILITY);
        return impliedVol > 0 && strike > lastPrice * 0.9d && strike < lastPrice * 1.1d;
    }
});

//Select all distinct expiry dates for quotes
Array<LocalDate> expiryDates = options.colAt(YahooField.EXPIRY_DATE).distinct();
//Creates frames for each expiry including only strike price and implied-vol columns
Array<DataFrame<Integer,String>> frames = expiryDates.map(v -> {
    final LocalDate expiry = v.getValue();
    final DataFrame<String,YahooField> calls = options.rows().select(row -> {
        final LocalDate date = row.getValue(YahooField.EXPIRY_DATE);
        return expiry.equals(date);
    });
    return DataFrame.of(Range.of(0, calls.rowCount()), String.class, columns -> {
        columns.add("Strike", calls.colAt(YahooField.PX_STRIKE).toArray());
        columns.add(expiry.toString(), calls.colAt(YahooField.IMPLIED_VOLATILITY).toArray().applyDoubles(x -> {
            return x.getDouble() * 100d;
        }));
    });
});

//Create plot of N frames each for a different expiry
Chart.create().asSwing().withLinePlot(frames.getValue(0), "Strike", chart -> {
    for (int i=1; i<frames.length(); ++i) {
        DataFrame<Integer,String> data = frames.getValue(i);
        chart.plot().<String>data().add(data, "Strike");
        chart.plot().render(i).withLines(true, false);
    }
    chart.plot().render(0).withLines(true, false);
    chart.plot().axes().domain().label().withText("Strike Price");
    chart.plot().axes().range(0).label().withText("Implied Volatility");
    chart.plot().axes().range(0).format().withPattern("0.00'%';-0.00'%'");
    chart.title().withText("SPY Call Option Implied Volatility Smiles");
    chart.legend().on().right();
    chart.show();
});
```

We can use a slightly modified version of this code to run the analysis for all **PUT options**, the results of 
which are plotted below. The same smile pattern is evident, as are the existence of outliers, which is most likely due 
to the lack of transactions at the strikes in question. Another take-away from these plots is that deep **in-the-money**
options are more expensive from an implied volatility perspective than deep **out-the-money** options as the smile
does not appear to be symmetric in nature.

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/option_put_smile.png"/>
</p>

### Key Statistics

Various **financial, trading** and **valuation statistics** are made available by Yahoo Finance on the [Statistics](https://finance.yahoo.com/quote/AAPL/key-statistics?p=AAPL)
page for each applicable security. The Morpheus adapter provides a programmatic mechanism to extract this data into
a `DataFrame` which allows for easy cross sectional comparisons between companies. Only current values are available
via this interface, historical values are not supported. The code below demonstrates how to extract these statistics
for various companies, and then transposes and prints the `DataFrame` to standard out.

<?prettify?>
```java
YahooFinance yahoo = new YahooFinance();
Array<String> tickers = Array.of("AAPL", "ORCL", "BLK", "GS", "NFLX", "AMZN", "FB");
DataFrame<String,YahooField> stats = yahoo.getStatistics(tickers);
stats.transpose().out().print(200, formats -> {
    final SmartFormat smartFormat = new SmartFormat();
    formats.setPrinter(Object.class, Printer.forObject(smartFormat::format));
});
```

<pre class="frame">
           Index            |     BLK      |     NFLX     |     AAPL     |     ORCL     |      GS      |      FB      |     AMZN     |
--------------------------------------------------------------------------------------------------------------------------------------
                MARKET_CAP  |    69.4700B  |    78.7300B  |   825.8200B  |   201.6200B  |    87.4300B  |   498.4800B  |   474.0300B  |
               PE_TRAILING  |     20.5800  |    221.8400  |     18.1500  |     22.0500  |     11.8100  |     38.4200  |    250.9600  |
                PE_FORWARD  |      1.4000  |      1.9800  |      1.4500  |      1.9800  |      1.0900  |      1.2100  |      6.6200  |
         PRICE_SALES_RATIO  |      6.0300  |      7.7300  |      3.6900  |      5.3400  |      2.7100  |     15.0300  |      3.1600  |
          PRICE_BOOK_RATIO  |      2.3500  |     25.2900  |      6.2400  |      3.7400  |      1.1600  |      7.4900  |     20.4000  |
           FISCAL_YEAR_END  |  2016-12-31  |  2016-12-31  |  2016-09-24  |  2017-05-31  |  2016-12-31  |  2016-12-31  |  2016-12-31  |
       MOST_RECENT_QUARTER  |  2017-06-30  |  2017-06-30  |  2017-07-01  |  2017-05-31  |  2017-06-30  |  2017-06-30  |  2017-06-30  |
             PROFIT_MARGIN  |      0.2992  |      0.0355  |      0.2087  |      0.2474  |      0.2644  |      0.3966  |      0.0128  |
          OPERATING_MARGIN  |      0.4205  |      0.0633  |      0.2684  |      0.3519  |      0.3618  |      0.4666  |      0.0231  |
          RETURN_ON_ASSETS  |      0.0138  |      0.0287  |      0.1152  |      0.0671  |      0.0095  |      0.1493  |      0.0283  |
          RETURN_ON_EQUITY  |      0.1174  |      0.1310  |      0.3603  |      0.1830  |      0.0980  |      0.2251  |      0.0967  |
               REVENUE_TTM  |    11.5200B  |    10.1900B  |   223.5100B  |    37.7300B  |    32.2500B  |    33.1700B  |   150.1200B  |
         REVENUE_PER_SHARE  |     70.5300  |     23.6900  |     42.4000  |      9.1700  |     77.9100  |     11.5000  |    314.7300  |
       REVENUE_GROWTH_QTLY  |      0.0570  |      0.3230  |      0.0720  |      0.0280  |     -0.0060  |      0.4480  |      0.2480  |
              GROSS_PROFIT  |    10.9500B  |     2.8000B  |    84.2600B  |    30.2600B  |    30.6100B  |    23.8500B  |    47.7200B  |
                EBITDA_TTM  |     5.0600B  |   706.9200M  |    70.2100B  |    14.6700B  |         NaN  |    18.0800B  |    12.3000B  |
               EPS_DILUTED  |     20.8300  |      0.8200  |      8.8100  |      2.2100  |     19.0700  |      4.4700  |      3.9300  |
      EARNINGS_GRWOTH_QTLY  |      0.0860  |      0.6100  |      0.1180  |      0.1490  |      0.0050  |      0.7060  |     -0.7700  |
                      BETA  |      1.6800  |      0.6300  |      1.4300  |      1.1400  |      1.4400  |      0.5400  |      1.3800  |
                  CASH_MRQ  |     6.2500B  |     2.1600B  |    77.0100B  |    66.0800B  |   732.4800B  |    35.4500B  |    21.4500B  |
            CASH_PER_SHARE  |     38.5300  |      5.0100  |     14.9100  |     15.9700  |     1.8868K  |     12.2100  |     44.6500  |
                  DEBT_MRQ  |     4.9700B  |     4.8400B  |   108.6000B  |    57.9100B  |   404.4600B  |         NaN  |    23.6200B  |
      DEBT_OVER_EQUITY_MRQ  |     16.6300  |    155.3900  |     82.0100  |    106.7500  |    463.8500  |         NaN  |    101.7500  |
             CURRENT_RATIO  |      1.2300  |      1.3100  |      1.3900  |      3.0800  |      1.8000  |     12.3100  |      1.0100  |
      BOOK_VALUE_PER_SHARE  |    182.2100  |      7.2100  |     25.6100  |     13.0200  |    194.4100  |     22.9200  |     48.3600  |
       OPERATING_CASH_FLOW  |     3.3900B  |    -1.9000B  |    64.0700B  |    14.1300B  |   -15.8300B  |    19.3800B  |    17.0600B  |
    LEVERED_FREE_CASH_FLOW  |     3.4500B  |     5.8300B  |    40.6200B  |     9.6300B  |         NaN  |    10.2200B  |    11.1500B  |
                ADV_3MONTH  |   505.7900K  |     6.9300M  |    26.7900M  |    13.1800M  |     3.0200M  |    16.4700M  |     3.6400M  |
                 ADV_10DAY  |   435.9500K  |     5.6800M  |    34.1000M  |    14.5700M  |     3.3800M  |    13.0400M  |     2.7500M  |
        SHARES_OUTSTANDING  |   160.9800M  |   431.7500M  |     5.1700B  |     4.1400B  |   388.2100M  |     2.3700B  |   480.3800M  |
              SHARES_FLOAT  |   123.7600M  |   424.8500M  |     5.0300B  |     3.0100B  |   350.5400M  |     2.3400B  |   400.0900M  |
     OWNER_PERCENT_INSIDER  |      0.0361  |      0.0182  |      0.0008  |      0.2725  |      0.0179  |      0.0175  |      0.1677  |
 OWNER_PERCENT_INSTITUTION  |      0.8775  |      0.8284  |      0.6247  |      0.5984  |      0.7931  |      0.7244  |      0.6234  |
              SHARES_SHORT  |     2.0600M  |    27.8500M  |    40.3100M  |    31.8300M  |     4.5400M  |    20.2500M  |     4.7200M  |
        SHARES_SHORT_RATIO  |      3.1800  |      3.0700  |      1.9000  |      1.8400  |      1.2700  |      0.9700  |      1.2100  |
        SHARES_SHORT_PRIOR  |     2.3100M  |    25.7400M  |    39.1500M  |    35.7800M  |     4.3500M  |    21.8400M  |     5.0600M  |
              DIVIDEND_FWD  |     10.0000  |         NaN  |      2.5200  |      0.7600  |      3.0000  |         NaN  |         NaN  |
        DIVIDEND_FWD_YIELD  |      0.0235  |         NaN  |      0.0158  |      0.0144  |      0.0139  |         NaN  |         NaN  |
         DIVIDEND_TRAILING  |      9.5800  |         NaN  |      2.3400  |      0.6400  |      2.7000  |         NaN  |         NaN  |
   DIVIDEND_TRAILING_YIELD  |      0.0225  |         NaN  |      0.0148  |      0.0121  |      0.0119  |         NaN  |         NaN  |
     DIVIDEND_PAYOUT_RATIO  |      0.4599  |         NaN  |      0.2650  |      0.2896  |      0.1421  |         NaN  |         NaN  |
         DIVIDEND_PAY_DATE  |  2017-09-22  |        null  |  2017-08-17  |  2017-08-02  |  2017-09-28  |        null  |        null  |
          DIVIDEND_EX_DATE  |  2017-08-31  |        null  |  2017-08-10  |  2017-07-17  |  2017-05-30  |        null  |        null  |
           LAST_SPLIT_DATE  |  2007-06-05  |  2015-07-15  |  2014-06-09  |  2000-10-13  |        null  |        null  |  1999-09-02  |
</pre>

The code below demonstrates how to generate a plot of a small subset of the profitability and return metrics for a number
of prominent financial services and technology firms.

<?prettify?>
```java
YahooFinance yahoo = new YahooFinance();
Array<String> tickers = Array.of("BLK", "GS", "MS", "JPM", "C", "BAC", "AAPL", "NVDA", "GOOGL");
DataFrame<String,YahooField> data = yahoo.getStatistics(tickers);
DataFrame<String,YahooField> stats = data.cols().select(
    YahooField.PROFIT_MARGIN,
    YahooField.OPERATING_MARGIN,
    YahooField.RETURN_ON_ASSETS,
    YahooField.RETURN_ON_EQUITY
).applyDoubles(v -> {
    return v.getDouble() * 100d;
});

Chart.create().withBarPlot(stats.transpose(), false, chart -> {
    chart.title().withText("Profitability & Return Metrics");
    chart.plot().axes().domain().label().withText("Statistic");
    chart.plot().axes().range(0).label().withText("Value");
    chart.plot().axes().range(0).format().withPattern("0.00'%';-0.00'%'");
    chart.legend().right().on();
    chart.show();
});
```

<p align="center">
    <img class="chart" src="http://www.zavtech.com/morpheus/docs/images/yahoo/asset_stats.png"/>
</p>

### Portfolio Analysis

There are several examples of how to use the Yahoo Finance adapter to analyze and construct portfolios of risky assets
in the section on [Modern Portfolio Theory](http://www.zavtech.com/morpheus/docs/examples/mpt/).
