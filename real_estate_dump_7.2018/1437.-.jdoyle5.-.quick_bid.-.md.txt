# quickBid

[quickBid](https://quickbid.wixsite.com/quickbid) is a 60 second live auction app aimed at helping companies eliminate surplus inventory fast and minimize deadweight loss.

## Table of Contents

- [Background](#background)
- [Technologies](#technologies)
- [Features](#features)
- [Maintainers](#maintainers)

## Background

This app was inspired by the estate sales and auto auctions that team member Max Tocarev attended. Every minute, there is a new item up for auction, and each auction lasts one minute. quickBid serves 2 sides: companies with excess items that need extra visibility beyond their own sales and discounts, and value-seeking customers looking to score great deals fast. In a nutshell, quickBid is a combination of eBay auctions and flash sales.

## Technologies

* JavaScript and MERN-Native stack (MongoDB, Express, React Native, Node.js)
* Socket.io powers live auction and real time bidding
* OAuth 2.0 for authentication layer
* Walmart open API for sample data

## Features

### OAuth 2.0

![OAuth](https://github.com/jdoyle5/quick_bid/blob/master/docs/screenshots/OAuth.png)

Allows users to seamlessly and securely signup/log in using Facebook or Google. OAuth 2.0 uses token-based authentication to orchestrate an approval interaction between users and our app. When a user logs in, our backend checks to see if user has logged in to our app before and decides whether to create a new user profile or fetch an existing one.

### Dashboard

![Dashboard](https://github.com/jdoyle5/quick_bid/blob/master/docs/screenshots/Dashboard_1.png)

Features a list of all the items available for bidding. We incorporated Walmart open API to generate sample items that get reseeded on the backend perpetually to keep scheduling active at all times. Database uses MongoDB architecture running on Mongoose. Express on Node.js connects our frontend to the backend providing API endpoints to React Native.

![Dashboard2](https://github.com/jdoyle5/quick_bid/blob/master/docs/screenshots/Dashboard_2.png)

Clicking on an item will display additional information; the item's MSRP and the auction time for the item.

### Bidding window

![Bidding Window](https://github.com/jdoyle5/quick_bid/blob/master/docs/screenshots/Auction_Window.png)

Showcases the item details and multi-player real time bidding functionality enabled by websockets. By clicking on the yellow button with the current bid price, it will increase the current bid by a set increment. The increment is determined based on that item’s MSRP (i.e. a more expensive item will have a larger bid increment than a less expensive item)

```javascript
//socket.js

export const increaseBid = (userKey, bidAmount, auctionItemId, socket) => {
  Item.findOne({bid_time: bidTime()}).exec((err, foundItem) => {
    if (foundItem.id === auctionItemId) {
      Item.findOneAndUpdate({bid_time: bidTime()}, {
        "$set": {
          "highest_bid": bidAmount,
          "highest_bidder_key": userKey
        }
      }, {new: true}
    ).exec((err2, updatedItem) => {
        socket.emit('auction item', updatedItem);
        if (err2) {
          console.log(err2);
        }
      });
    }

  });

```
When a user clicks on bid button, our backend confirms that the user's bid is higher than the current winning bid as well as provisions for timing discrepancy. In case multiple users submit bids for the same amount, the server will accept the first bid that comes in. Then the server emits updated highest bid to all connected clients on socket.io. Users' Redux store gets updated with the most recent information which triggers React component to re-render. At that point all users can bid again.


### Future Directions
* Implement categories for easier navigation
* Users can bookmark a future auction and set a reminder (push notification)
* User profile component

## Maintainers

[@tocarevmax](https://github.com/tocarevmax)
[@Maxine-Chui](https://github.com/Maxine-Chui)
[@jdoyle5](https://github.com/jdoyle5)
[@w-chun](https://github.com/w-chun)
