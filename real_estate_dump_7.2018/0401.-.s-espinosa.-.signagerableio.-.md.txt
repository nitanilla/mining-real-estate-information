# Signagerableio

### TEAM
 - [Sal Espinosa](https://twitter.com/sespinos)
 - [Alex Navarrete](https://twitter.com/salvi6god)

Signagerableio is a project assigned by [Trelora](http://www.trelora.com/) (a Real Estate Agency located in Denver) that allows an administrator to control content being displayed on televisions throughout their office. Content is pulled from an internal Trelora API and displayed based on 'roles' assigned by an administrator (currently 'sold' or 'coming soon').

## Features
- Dynamically generates slides to be displayed and fades between two divs in which the slides are rendered

- Admin is able to manually "refresh" their slides and roles whenever Trelora ends up updating their API

- Admin is able to select the amount of seconds they'd like in between the transition for the slides

-  Heroku scheduler that calls on a rake task that "refreshes" the types of roles and slides that will be displayed on the devices each night

## Demo
![Admin Dashboard](https://media.giphy.com/media/xT8qBbxkfCYDMryhi0/giphy.gif)
![Sold Properties](https://media.giphy.com/media/3o6gEgag4Txrf1mZdC/giphy.gif)
![Coming Soon Properties](https://media.giphy.com/media/xT8qBfsC1njLXXfcvS/giphy.gif)

