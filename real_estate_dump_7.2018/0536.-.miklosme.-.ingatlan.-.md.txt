# ingatlan

React Native app for scraping adverts from hungarian real estate site `ingatlan.com`, and present results in a better manner.

Support is iOS only for now.

Non profit and open source project.

# Known Issues

- Markers aren't appearing on the map from the second map render (3rd party issue)

# Build

You will need OSX, with the newest Xcode. Apple Dev account is NOT required.

Steps of building the app: [React Native getting started](https://facebook.github.io/react-native/docs/getting-started.html)

# Highlights
Here are some interesting parts from the project. Things what I just learnt, or something that worth mentioning.

### Cheerio
[Cheerio](https://github.com/cheeriojs/cheerio): jQuery on the server.

How to use with React Native? Override these Node modules:
`npm install --save cheerio buffer events stream`

### generate_component.sh
Generate clean React component structure:
[generate_component.sh](https://github.com/CAPSLOCKUSER/ingatlan/blob/master/generate_component.sh)
[generate_stateless_component.sh](https://github.com/CAPSLOCKUSER/ingatlan/blob/master/generate_stateless_component.sh)

### Vector icons
[React Native Vector Icons](https://github.com/oblador/react-native-vector-icons)
I highly recommend this package!

### RNPM
[RNPM](https://github.com/rnpm/rnpm)
Gives you the excellent `rnpm link` command.

### eslint autofix
When you pass `--fix` flag to eslint, it tries to fix some errors. Great stuff.
Usage in this project: `npm run lint -- --fix`

### setup.js && LOG
[Handy trick](https://github.com/CAPSLOCKUSER/ingatlan/blob/master/js/setup.js#L34) from [F8App](https://github.com/fbsamples/f8app).

# Licence
MIT
