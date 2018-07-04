# Description

.blm files are a real estate specific file format developed by Rightmove, a British-based company that runs
www.rightmove.co.uk, an online real estate portal. The format definition is available at
http://www.rightmove.co.uk/ps/pdf/guides/RightmoveDatafeedFormatV3iOVS_1.5.pdf. It is essentially just a specialized
csv format. The module input is the file path of a .blm file and the output of the module is a JSON object containing
the property value mappings as defined by the file.

## Usage:

```
let parser = require('blm-parser');
parser.parseBlmFile("./test.blm", (err, result) => {
    if (err) {
        console.log(err);
        return;
    }
    //If no error then result is the JSON object containing file data
    console.log(result);
});
```

## NPM
https://www.npmjs.com/package/blm-parser
