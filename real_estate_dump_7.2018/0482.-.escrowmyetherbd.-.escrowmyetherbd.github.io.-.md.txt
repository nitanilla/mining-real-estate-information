# For Developers - EscrowMyEther Buyer Dashboard

This repo is for developers who are looking to integrate EscrowMyEther on their site. 




## Getting Started

This repo is hosted on github pages: https://escrowmyetherbd.github.io/

There are several ways to integrate the buyer dashboard in your site. The easiest way is cloning this repository on github and running it on github pages, and replacing the github.io domain with your subdomain (dashboard.yoursite.com).
For more info on setting up github pages, visit: https://pages.github.com/

EscrowMyEther is a static html/css/javascript/ReactJS site and a client-side interface to the escrow smart contract. No special hosting environment is required if you choose to copy the repo and run it on your site.

## Modifying for your own usage - Get started

1)	Copy the "Source Files" folder
2)	Download node_modules.zip from this link: https://drive.google.com/open?id=0By0DAad8QzZAUjBDQ1VJQmZieTg
3)  Copy the extracted folder into "Source Files" folder
4)	Install NodeJS. v8.1.4 is recommended as it's used in the development of this Dapp.
5)  You can then modify the Dapp for your usage. The below commands will be helpful.

npm start - Start a local version of the Dapp in your browser localhost:3000. It automatically reloads the Dapp when you save any updates to the source files. Useful during development.

npm run build - Build an optimized version for deployment. A new folder called build_webpack will be created with the optimized version. You can upload the content of build_webpack directly to github pages for deployment.

## Setting up Seller dashboard

1)	Head to source files > src > App.js
2) Change line 6 from the first line to 2nd line: 

> import BuyerHome from "./BuyerHome"

> import SellerHome from "./SellerHome"

3) On line 19, change "BuyerHome" to "SellerHome"

4) npm run build. You will build the static site for Seller dashboard.

## Layout of source files

### Public > Index.html
Content of the Dapp is served within the root div. Any content added above this root div will show above the Dapp, like a header. Any content added below will display like a footer.

### src > Index.css
Css file for modifying styles.

### src > BuyerHome.js
The buyer dashboard page you see when visiting https://escrowmyetherbd.github.io/

### src > SellerHome.js
The seller dashboard page

### src > NewTransactionRS.js
When you click "Initialize new transaction" on the dashboard, the right side changes to this page. This page should be modified if you wish to hardcode your address as the escrow agent or seller.

![newtx](https://user-images.githubusercontent.com/24837709/31051404-cfbd440a-a699-11e7-9c97-0f9134f3cdaf.jpg)

### src > SpecificTx.js
The right side of the dashboard changes to this page when an existing transaction is clicked.
![tx](https://user-images.githubusercontent.com/24837709/31041943-3ef37698-a5d0-11e7-87bc-f15ca9d95e04.jpg)

## Adding your header & footer

Under Public > Index.html, the Dapp is rendered within the root div. Custom header and footers can be added above and below this div.


## Hardcoding Escrow Agent address
If you look to be the escrow agent for your site (example: Real estate agents, classified sites), you can remove the escrow agent input field and hardcode your address as the escrow agent.

To do this, 

1) Open Source Files > src > NewTransactionRS.js.

2) Hardcode your address. In line 306, replace this.state.escrowAddress with your own address as follows:
![Orignal](https://user-images.githubusercontent.com/24837709/32013863-fb55a59a-b9ee-11e7-867b-437a1f67526f.png)

![New](https://user-images.githubusercontent.com/24837709/32013861-fb290e9a-b9ee-11e7-8754-fa4f7cdca610.png)

3) Remove the Escrow Address input field

Line 425 to 434 and 368 to 377 contains the Escrow Address input field. Remove both of them.

![Remove](https://user-images.githubusercontent.com/24837709/32030707-6ec46738-ba2f-11e7-8fe3-5dd84c7a6181.png)

4) Your address will then be the Escrow Agent for all transactions on your site.

## Further questions
If you need assistance integrating/modifying EsrowMyEther for your site, feel free to raise a github issue or contact me at escrowmyether[at]gmail[dot]com.

## Authors

Cheung Ka Yin 
escrowmyether[at]gmail[dot]com

