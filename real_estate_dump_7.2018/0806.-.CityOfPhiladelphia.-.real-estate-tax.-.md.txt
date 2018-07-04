# real-estate-tax

(_work in progress_)

A front-end web app for looking up and paying real estate tax balances. Written in JavaScript using Vue.js. Backed by the [TIPS API](https://github.com/CityOfPhiladelphia/tips-api) account lookup microservice.

## Developing locally

### Requirements

- Node.js (developed using 8.x)
- [Yarn](https://yarnpkg.com/lang/en/)

### Setup

1. `git clone https://github.com/cityofphiladelphia/real-estate-tax`
2. `cd real-estate-tax`
3. `yarn`

### Running

To run the development server and automatically launch the app in your default browser:

```bash
yarn serve
````

## Testing

TODO

## Deploying

### Bundling

To create the app bundle:

```bash
yarn build
```

This will output a build of the app to the `dist` directory. This directory can be placed on any static file server.

### Continuous integration

TODO
