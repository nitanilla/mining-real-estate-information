

# MY place webstore
progressive web app store made with preact

**OBS: For better testing of the ui test in mobile mode**
> **[:boom: View Demo :boom:](https://smart-men.surge.sh/)**


---
# Guide
- [motivation](#motivation)
- [Installation](#installation)
- [Development Workflow](#development-workflow)
- [Folder Structure](#structure)
- [CSS Modules](#css-modules)

# Stack
- preact
- firebase
- webpack


# Motivation

## why progressive webapp ?

Progressive Web Apps are user experiences that have the reach of the web, and are:
Reliable - Load instantly and never show the downasaur, even in uncertain network conditions.
Fast - Respond quickly to user interactions with silky smooth animations and no janky scrolling.
Engaging - Feel like a natural app on the device, with an immersive user experience.
This new level of quality allows Progressive Web Apps to earn a place on the user's home screen.

## More Engaging ?
  More than 50% of the purchases made by mobile are realized through the sites (and not native applications)   https://youtu.be/kD0j2BwgF7c?t=36
  Google has been collecting PWA case studies and the results are pretty impressive.

  **Alibaba** is the global leader in B2B trade. Recently, they upgraded to a PWA:
  - 76% more web conversions
  - 30% more monthly active users on Android, 14% more on iOS
  - 4X higher interaction rate from Add to Homescreen

**Housing.com** is one of the leading real estate platforms in India. After implementing their PWA:
- 38% more conversions
- 40% lower bounce rate
- 10% longer average session
- 30% faster page load


## Installation

**1. Clone this repo:**

```sh
git clone --depth 1 https://github.com/developit/preact-boilerplate.git my-app
cd my-app
```

**3. Install the dependencies:**

```sh
npm install
```


## Development Workflow


**4. Start a live-reload development server:**

```sh
npm run dev
```

> This is a full web server nicely suited to your project. Any time you make changes within the `src` directory, it will rebuild and even refresh your browser.


**6. Generate a production build in `./build`:**

```sh
npm run build
```

> You can now deploy the contents of the `build` directory to production!
>
> **[Surge.sh](https://surge.sh) Example:** `surge ./build -d my-app.surge.sh`
>
> **[Netlify](https://www.netlify.com/docs/cli/) Example:** `netlify deploy`
>
> [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/developit/preact-boilerplate)


**5. Start local production server with [serve](https://github.com/zeit/serve):**

```sh
npm start
```

> This is to simulate a production (CDN) server with gzip. It just serves up the contents of `./build`.



---


## Folder Structure

```
├── 200.ejs
├── _redirects
├── assets
│   └── icons
│       ├── android-chrome-192x192.png
│       ├── android-chrome-512x512.png
│       ├── apple-touch-icon.png
│       ├── browserconfig.xml
│       ├── favicon-16x16.png
│       ├── favicon-32x32.png
│       ├── favicon.ico
│       ├── mstile-150x150.png
│       └── safari-pinned-tab.svg
├── components
│   ├── actionbutton
│   ├── app.js
│   ├── cart
│   ├── checkout
│   ├── header
│   │   ├── index.js
│   │   └── style.less
│   ├── product
│   ├── profile
│   └── snackbar
├── config.json
├── favicon.ico
├── firebaseConfig.js
├── index.ejs
├── index.js
├── lib
│   └── utils.js
├── manifest.json
├── pwa.js
└── style
    ├── index.less
    ├── mixins.less
```


---


## CSS Modules

This project is set up to support [CSS Modules](https://github.com/css-modules/css-modules).  By default, styles in `src/style` are **global** (not using CSS Modules) to make global declarations, imports and helpers easy to declare.  Styles in `src/components` are loaded as CSS Modules via [Webpack's css-loader](https://github.com/webpack/css-loader#css-modules).  Modular CSS namespaces class names, and when imported into JavaScript returns a mapping of canonical (unmodified) CSS classes to their local (namespaced/suffixed) counterparts.

When imported, this LESS/CSS:

```css
.redText { color:red; }
.blueText { color:blue; }
```

... returns the following map:

```js
import styles from './style.css';
console.log(styles);
// {
//   redText: 'redText_local_9gt72',
//   blueText: 'blueText_local_9gt72'
// }
```

Note that the suffix for local classNames is generated based on an md5 hash of the file. Changing the file changes the hash.


# lighthouse score

![pontuação](https://firebasestorage.googleapis.com/v0/b/myplace-d196a.appspot.com/o/Captura%20de%20Tela%202017-02-03%20a%CC%80s%2022.39.31.png?alt=media&token=c66deb33-d352-4002-afe4-36293ff4e730)


# Pingdom

![](https://firebasestorage.googleapis.com/v0/b/myplace-d196a.appspot.com/o/Captura%20de%20Tela%202017-02-03%20a%CC%80s%2022.47.57.png?alt=media&token=b11cc380-99e3-4547-97f4-e05abbcb5e0a)

# Disclamer

I know that this project needs a lot of [improvements](https://blog.prototypr.io/you-will-write-bad-code-94081bb66bec#.c5bv0cmjo),and I will certainly do it,
This was my first tryout with these technologies, and  always good to keep in mind of what matters most is the  [continuous improvement](https://www.youtube.com/watch?v=QLbUzwxkwHA),
aways keep on hacking, and wait for the new improvements.

MIT
