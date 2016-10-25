---
layout: post
title: Babeling React code in ES6 with Webpack
---

In continuing by React education, I figured I'd start a fun, inconsequential project. Over a year ago, when I was learning JavaScript, I decided to build out [Snake](https://en.wikipedia.org/wiki/Snake_(video_game)). The code for a rudimentary working version of it can be found [here](https://github.com/lewaabahmad/snak3/tree/2d) and that version can also be played [here]() for those of you that are fun.

Before I could start writing code for the game, I need to figure out how I can even use React in HTML pages. [This is the installation documentation for React.](https://facebook.github.io/react/docs/installation.html) I scroll down to "Creating a Single Page Application" - brilliant, exactly what I need. Apparently, the easiest way to set stuff up for using React is to use an npm module titled "[create-react-app](https://github.com/facebookincubator/create-react-app)." As per the installation docs it "uses Webpack, Babel and ESLint under the hood, but configures them for you."

Annnnnd boom - ladies and gentlemen, we've come across magic. 

Soooooooooooo, let's get to the bottom of this wizardry and pop the hood, tear the motor out, and fuck everything up. 

First off, let's make sure our JavaScript runtime is all set up. I didn't have nvm (node version manager) so I installed that and made sure I was using the last LTS release, which as of this writing is 4.6.1. I did the same for npm at version 2.15.9. 

*Note! Though I tried to make things work with the LTS releases, I needed to update to latest to use my modules properly and run webpack! Install and use the latest version instead if you are following this for whatever godforsaken reason!*

Great. Installing the React app generator was as simple as `npm install -g create-react-app` after that. Running the command `create-react-app hello-world` gives us the following:

```
// ♥ tree -I node_modules
.
├── README.md
├── package.json
├── public
│   ├── favicon.ico
│   └── index.html
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    └── logo.svg

2 directories, 10 files
```
*Note the 'tree' with the -I command to ignore the node_modules directory.*

Huh. Definitely not what I was thinking... this seems like they've packaged everything that has to do with building and the like to the modules. My suspicions are reinforced by the package.json file: 

```
{
  "name": "hello-world",
  "version": "0.1.0",
  "private": true,
  "devDependencies": {
    "react-scripts": "0.7.0"
  },
  "dependencies": {
    "react": "^15.3.2",
    "react-dom": "^15.3.2"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

Reading the docs, it seems like I can run `npm run eject` to pull out the guts and see the Babel, Webpack, and ESLint configurations. Running the command pulls the congig files to `./config/`, adds a ton of dependencies (likely dependencies of the React module wrappers got from `create-react-app`) and updates the package.json. Yeah, this is more like it! The new folder:

```
├── config
│   ├── env.js
│   ├── jest
│   │   ├── CSSStub.js
│   │   └── FileStub.js
│   ├── paths.js
│   ├── polyfills.js
│   ├── webpack.config.dev.js
│   └── webpack.config.prod.js
```

...and new package.json: 

```
{
  "name": "hello-world",
  "version": "0.1.0",
  "private": true,
  "devDependencies": {
    "autoprefixer": "6.5.1",
    "babel-core": "6.17.0",
    "babel-eslint": "7.0.0",
    "babel-jest": "16.0.0",
    "babel-loader": "6.2.5",
    "babel-preset-react-app": "^1.0.0",
    "case-sensitive-paths-webpack-plugin": "1.1.4",
    "chalk": "1.1.3",
    "connect-history-api-fallback": "1.3.0",
    "cross-spawn": "4.0.2",
    "css-loader": "0.25.0",
    "detect-port": "1.0.1",
    "dotenv": "2.0.0",
    "eslint": "3.8.1",
    "eslint-config-react-app": "^0.3.0",
    "eslint-loader": "1.6.0",
    "eslint-plugin-flowtype": "2.21.0",
    "eslint-plugin-import": "2.0.1",
    "eslint-plugin-jsx-a11y": "2.2.3",
    "eslint-plugin-react": "6.4.1",
    "extract-text-webpack-plugin": "1.0.1",
    "file-loader": "0.9.0",
    "filesize": "3.3.0",
    "find-cache-dir": "0.1.1",
    "fs-extra": "0.30.0",
    "gzip-size": "3.0.0",
    "html-webpack-plugin": "2.24.0",
    "http-proxy-middleware": "0.17.2",
    "jest": "16.0.2",
    "json-loader": "0.5.4",
    "object-assign": "4.1.0",
    "path-exists": "2.1.0",
    "postcss-loader": "1.0.0",
    "promise": "7.1.1",
    "react-dev-utils": "^0.3.0",
    "recursive-readdir": "2.1.0",
    "rimraf": "2.5.4",
    "strip-ansi": "3.0.1",
    "style-loader": "0.13.1",
    "url-loader": "0.5.7",
    "webpack": "1.13.2",
    "webpack-dev-server": "1.16.2",
    "webpack-manifest-plugin": "1.1.0",
    "whatwg-fetch": "1.0.0"
  },
  "dependencies": {
    "react": "^15.3.2",
    "react-dom": "^15.3.2"
  },
  "scripts": {
    "start": "node scripts/start.js",
    "build": "node scripts/build.js",
    "test": "node scripts/test.js --env=jsdom"
  },
  "jest": {
    "moduleFileExtensions": [
      "jsx",
      "js",
      "json"
    ],
    "moduleNameMapper": {
      "^.+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "<rootDir>/config/jest/FileStub.js",
      "^.+\\.css$": "<rootDir>/config/jest/CSSStub.js"
    },
    "setupFiles": [
      "<rootDir>/config/polyfills.js"
    ],
    "testPathIgnorePatterns": [
      "<rootDir>/(build|docs|node_modules)/"
    ],
    "testEnvironment": "node"
  },
  "babel": {
    "presets": [
      "react-app"
    ]
  },
  "eslintConfig": {
    "extends": "react-app"
  }
}
```

Well damn. Poking around, a lot of this makes sense. Then again, a lot of doesn't. There's a lot already set up and without some prior knowledge I don't think it's the best use of my time to play around toooo much in here - I'd rather start my own app and write some configs from scratch. And you know what, let's set it up so I can start programming that Snake game. [This](https://egghead.io/lessons/react-building-a-react-js-app-notetaker-introduction?play=yes) is a great video tutorial I found. Don't think I'll go through it all, but I'll definitely see how he sets stuff up ^.^

Here are the steps I noted: 

1 - Start the empty project with npm init (duh!)

2 - `npm install --save react` - really doing some rocket science here! 

3 - `npm install --save react-dom` - this module handles interactions react has with the DOM. It's pretty aptly named. Why? [That's explained here pretty well.](http://stackoverflow.com/questions/34114350/react-vs-reactdom)

4 - `npm install --save -dev babel-core babel-loader babel-preset-es2015` - this is what the Babel installation page tells you to do when you intend to use Webpack. Seems like Babel has a lot of ways it can be installed/configured depending on the implementation. We NEED Babel for JSX translation. 

5 - `mkdir public && touch public/index.html` - the root view of the app: 

```html
<!DOCTYPE html>
<html>
<head>
  <title>Snak3 in R3act</title>
</head>
<body>
  <div id="game"></div>
  <script type="text/javascript" src="bundle.js"></script>
</body>
</html>
```

`bundle.js` will be the result of Webpack's compiling the React/JSX code we write. 

6 - `touch webpack.config.js` (if you don't have webpack run `npm install webpack -g` - you might need to go `sudo` on that.)

```
module.export = {
  // The root component. Where all the other components are rendered from:
  entry: "./app/components/board.js",
  // Where the transpiled code goes:
  output: {
    filename: "public/bundle.js"
  },
  // The configurtions of the modules we are to use. This is where it gets weird.
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel', 
        query: {
          presets: [ 'react', 'es2015' ]
        }
      }
    ]
  }
}
```

Webpack Loaders are documented [here](http://webpack.github.io/docs/using-loaders.html).

7 - `mkdir components && touch components/board.js` to make our main/root react component. I wrote the following code in there: 

```
var React = require('react');
var ReactDOM = require('react-dom');

var Board = React.createClass({
  render: function() {
    return (
      <div id="main-board">
        hello?
      </div>
    )
  }
})

ReactDOM.render(<Board />, document.getElementById('game'))
```

8 - `webpack -w` - this actually was giving me a number of errors. Fantastic. I had to update from the LTS release because they handled/navigated the npm modules folder differently from the recent releases, and had to squash some other bugs. I added a note to the earlier install step. 

And boooooooooom!

My bundle.js file exists, everything I need is in there, and when I open my index.js file in the browser I see my 'hello?'.

Now I can start programming the game!

I found even more tutorials for React [here](http://andrewhfarmer.com/getting-started-tutorials/). I don't know to what extent I'll check them out but I'm definitely gonna stick to learning the framework. 