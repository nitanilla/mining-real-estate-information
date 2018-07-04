Lucky Horse Bitcoin Trader
==========================

__Lucky Horse was a project to test a couple of ideas I had about currency trading.  They were not successful and I'm publishing this only for posterity.  Writing the thing was fun but for the love of Imhotep, don't trust it with real money.__

__I wrote a [blog post](https://mocko.org.uk/b/2017/01/03/step-3-unprofit-a-naive-experiment-in-cryptocurrency-trading/) discussing the project in more depth.__


![SUCH HORSE](docs/horserace.jpg)


Mah Bitcoin trading framework.


TODO
====

* General:
    * Bot startup() method instead of init where time is known to be correct
    * PusherSocketThread needs a way to notify event consumers that there has been an interruption when it reconnects
    * Better logging configuration: external logfiles, debug output off, bots have own logs
* Backtester:
    * Better performance recording for each run.  Generate graphs?
    * Automation to try range of variables over multiple runs
* Trading opportunities:
    * Arbitrage between exchanges.  By holding $1000 balances on many exchanges and flushing coins between them when advantageous. Only move money when absolutely necessary.
* Technical debt wall of shame:
    * `ts_create_hack` in storage/orders.py.  Fix the database so it isn't required.



Links
=====

* http://pandas.pydata.org/


Installation
============

1. `virtualenv -p /usr/local/bin/python3.4 _venv3`
2. `. _venv3/bin/activate.fish`
3. `pip install git+git://github.com/estatic/PyPusher.git`
4. `pip install -r code/requirements.txt`  NB: using remote pypusherapp from github; doesn't work from PyPy


Trading Bots
============

### crashdumper

Attempt to hold all assets in BTC but get out of the market while a crash is happening, then cautiously re-enter after it.  This bot will not make any profit for months on end but should give a huge one by exploiting Bitcoin's regular clusterfucks.


### meandolly

Simple mean-reversion strategy.


### bollydolly

Implements conventional Bollinger Band trading.


### conversebollydolly

Converse Bollinger Band trading.


### reverend

A Bayesian algorithm that estimates the statistical likelihood of the market rising and falling based on an input of what happened before.




DB Maintenance
==============

There is a command for this, `bin/dbmaint`.  See --help for details.  The following modes need better explanation...

##### --compact-sessions - merge overlapping sessions

When lucky horse is restarted it starts recording with a new session_id to indicate a gap in data.  But if you started a new instance before terminating the old one the sessions will overlap and the gap can be closed.  Better still, since trade_id's are distinct to each trade and revision_id's are at least unique, there's no need to change anything but the session_id of each record.

Starting at the highest (so most recent session_id) session_id, step back through the sessions looking for an n-1 session whose last record is later than our first.  If you find one, delete from it any records later than N's earliest then change any instance of the session_id N-1 to N.

Care is taken not to merge the sessions of different exchanges.



Testing
=======

Find all tests with:
```nosetests code/```



Backtesting
===========

Use the `lh-backtest` tool.



Tinkering
=========


### Shell-fu

##### Watch how the Sqlite database grows with orders (in fish)
`while true; sleep 10s; sqlite3 db/ws.db "SELECT COUNT(*) FROM OrderRevisions"; ls -lh db/ws.db; end`


### Useful Database Queries

##### Orders that served most trades

`SELECT order_id, price, COUNT(order_id) AS c FROM OrderRevisions GROUP BY order_id ORDER BY c DESC LIMIT 10;`

##### Life cycle of a single order

`SELECT * FROM OrderRevisions WHERE order_id='43241744’;`

##### N sessions with most orders in
`SELECT session_id, COUNT(*) AS n FROM OrderRevisions GROUP BY session_id ORDER BY n DESC LIMIT 20`



Exchange Notes
==============

### BitStamp

##### Does encryption on the connection affect latency?

```
PusherSocket(key, { 'encrypted': True } )
++++ LATENCIES  min:0.310 avg:0.726 max:1.256
```

```
PusherSocket(key, { 'encrypted': False } )
++++ LATENCIES  min:0.311 avg:0.647 max:1.223
```

No.


##### It's far away...

Pusher WebSockets example endpoint is `ec2-54-80-62-105.compute-1.amazonaws.com`.  This means...

1. Our data is coming from the US so has 1x 80ms transatlantic latency.  But since the exchange core is in UK it has to come from there it's actually 2x transatlantic latency.
2. Endpoint is a node not a LB.  It will go down occasionally.  Does Pusher handle reconnections gracefully?  Even at best this will mean the occasional hiccup in the stream.  Will we miss updates?

Minimum latency for an exchange event to get here is about 300ms.  160ms will be a round trip to America.  Where does the rest come from?  Could a data source closer to home be found?

What about a hit to the server with no data payload to be proxied from BitStamp?  Let's try something simple...

```
mock@core:~$ ping 54.80.62.105
PING 54.80.62.105 (54.80.62.105) 56(84) bytes of data.
64 bytes from 54.80.62.105: icmp_req=1 ttl=42 time=77.2 ms
...

mock@core:~$ curl -v --trace-time http://54.80.62.105/
19:49:07.680532 * About to connect() to 54.80.62.105 port 80 (#0)
19:49:07.680655 *   Trying 54.80.62.105... connected
19:49:07.759304 > GET / HTTP/1.1
19:49:07.759304 > User-Agent: curl/7.22.0 (x86_64-pc-linux-gnu) libcurl/7.22.0 OpenSSL/1.0.1 zlib/1.2.3.4 libidn/1.23 librtmp/2.3
19:49:07.759304 > Host: 54.80.62.105
19:49:07.759304 > Accept: */*
19:49:07.759304 >
19:49:07.837531 * Empty reply from server
19:49:07.837592 * Connection #0 to host 54.80.62.105 left intact
curl: (52) Empty reply from server
19:49:07.837658 * Closing connection #0
```
        


