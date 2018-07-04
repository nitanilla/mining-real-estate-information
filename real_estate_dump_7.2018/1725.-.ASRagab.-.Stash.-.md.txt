# Stash Interview (Article Recommender)

## Prerequisites
1. Scala `2.12`


## Instructions
0. Clone or download and unzip
1. Run `sbt "run <article number 1-11>"` from command line 

or

in IntelliJ:

1. Edit Configurations
2. Add a number between 1 - 11 to program arguments

For example:<br> 
`> sbt "run 1"`

### Sample Output

```
Article Liked: 
As their name implies, ETFs are investment funds that are traded on an exchange, such as the New York Stock Exchange (NYSE) 
or NASDAQ. ETFs often correspond to a particular size of company, industrial sector, market, or even social goal. So, you 
could own shares in an ETF that owns blue chip stocks of large companies, or the stocks of less well-known, smaller companies.
------------------------------
Similar Articles:
401(k)s and IRAs are types of savings accounts that allow you to invest in stocks, bonds, mutual funds, certificates of 
deposit, ETFs and index funds, among other investments, using your pre-tax dollars.

As their name implies, ETFs are investment funds that are traded on an exchange, such as the New York Stock Exchange 
(NYSE) or NASDAQ. ETFs often correspond to a particular size of company, industrial sector, market, or even social goal. 
So, you could own shares in an ETF that owns blue chip stocks of large companies, or the stocks of less well-known, 
smaller companies.

A REIT can also be an ETF. And like an ETF it trades throughout the day like anything else on an exchange, such as a 
stock or a bond. There are about 200 REIT funds in the U.S. and they can be structured in different ways. The majority 
own actual real estate. Others can own debt, such as residential or commercial mortgages. Real Estate Tycoon, also known 
as VNQ or the Vanguard REIT Index Fund, tracks an index of publicly traded REITs. It only invests in shares of trusts 
that actually own real estate property.
```