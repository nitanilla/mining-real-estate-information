# neura

Neura is the fast and customizable neural network for JavaScript

### Requirements:
Node.js 4.2+

### Installation:
```
npm i neura
```

### Usage:
Initialize
```javascript
const Neura = require('neura');
let n = new Neura({layers: 2, iterations: 10000});
```

Add train data and run
```javascript
n.train({input: [[1, 0, 0],[0, 1, 1],[1, 1, 0]], output: [0, 0, 1]});
n.run([1,0,0]);
```

or
```javascript
n.train({input: [[1, 0, 0],[0, 1, 1],[1, 1, 0]], output: [0, 0, 1]})
  .run([1, 0, 0]);
```

Data can be saved in file
```javascript
n.train({input: [[1, 0, 0],[0, 1, 1],[1, 1, 0]], output: [0, 0, 1]})
  .saveToFile('./output.json');
```

Saved neural network synapse can be used again
```javascript
n.readFromFile('./output.json')
  .run([1, 0, 0]);
```
### For example:
Lets create a real estate scoring (chance to be sold)
Yes or no denoted by 1/0

|   id        |   Price in M$      |   Rooms    |   Area    |   Sold     |
|   -------   |   --------------   |   ------   |   -----   |   ------   |
|   1         |   1.12             |       3    |   25      |   0        |
|   2         |   25.2             |       4    |  116      |   1        |
|   ...       |   ...              |     ...    |  ...      |   ...      |
|   100000    |   4.1              |       1    |   65      |   1        |

Input is 2, 3 and 4 columns, output is 5 column.
Now we have to train our network
```javascript
let data = sellingChanceData;
n.train(data)
```
finnaly
```javascript
n.train(data).run([18, 2, 95]); // 0.85 => This house is likely to be sold
```
### Contributing:
Create issue or PR
```
git clone https://github.com/AlexanderGY/neura.git
cd neura && npm install
```

### Coming soon
Image recognition
