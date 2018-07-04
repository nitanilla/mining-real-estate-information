# Data Science Experience Demo Center

This repo contains source code for several demos to be used in DSX

## Demos

Click [here](https://ibm.box.com/s/1nu9cd0k0ojosttnmy8waebrp4xw1yze) for a deck with high level information on each demo.

|Demo Name|Industry|Deployed App| Video |
|:--------|:-------|:-----------|:------|
|**[Machine Learning and CPLEX](finanCPLEX)**| Financial Services | |
|**[Predicting Customer Churn](predictCustomerChurn)** | Telecommunications | [Bluemix](https://predictcustomerchurn.mybluemix.net) |
|**[BlocPower](blocPower)**| Energy | [iOS App](https://itunes.apple.com/us/app/blocpower-analyze/id1161437091) |
|**[San Francisco Traffic Accidents](trafficAccidents)**| Civil Services | [Interactive Notebook](http://nbviewer.jupyter.org/github/nwngeek212/DSX-DemoCenter/blob/4cabeb0e28f9053398358bd4858290a59c447735/trafficAccidents/notebooks/TrafficAccidentsPixieDust.ipynb) | [YouTube](https://www.youtube.com/watch?v=cYUdXFEmxP4)
|**[Modeling Tarmac Delays](tarmacTimes)**| Travel | |
|**[Weather Geographies](weatherGeographies)**| Weather | |
|**Coming Soon!**| Hardware | |
|**Coming Soon!**| Retail | |
|**Coming Soon!**| Real Estate | |

## Adding Content
Anyone with access to the IBMDataScience GitHub repo can add content to the Demo Center.

**Repo Structure**

- `data_assets` folder which contains all the relevant `csv` files
- `notebooks` folder which contains the Python or R notebooks being demoed
- `README.md` a brief decription of the demo. You can use the attached [template](README_template.md) to create the readme

**Slide**

Each demo will contain one slide in a more general DSX-DemoCenter deck. The slide should be very brief, including only the purpose, tools, industry, and other high level information of the demo.

To add a slide, you'll have to download the deck from the link above, which is located within IBM Box, modify it to reflect your added demo, and replace it within Box.

**This README**

You can follow the format of the table above when inserting a new demo. Simply create a new row in the table, include your demo, industry, and deployed app/video (if applicable). The easiest way to do with would be to just copy and paste the format from a previous row in the table and modify it. Be sure to `git add` the updated `README.md` file before running `git commit`