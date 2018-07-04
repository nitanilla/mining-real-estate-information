# real-estate-japan
Sample code of local advanced search helper for 'real-estate-japan' website.

## Why do I create this?
- 'real-estate-japan' website has a rough and terrible search interface with extremely long response times.
- To learn Python/MongoDB (i'm a beginner at them).

## Usage
```
python get.py "http://www.fudousan.or.jp/system/?act=l&type=31&pref=13&stype=e&line%5B%5D=2184&eki%5B%5D=2184131&rl=l&rh=h&asl=l&ash=h&submitbtn=l"
```

Python >= 3.6

## How does it work?
1. Get data from 'real-estate-japan's search results page
2. Modify the data schema
3. Store them into your local MongoDB
4. You can browse them via Robo 3T (Robomongo) or such tools
