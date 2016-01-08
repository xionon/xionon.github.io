---
layout: post
title: "Setting up React on Phoenix<br/>Revised for Brunch 2.0 and Phoenix 1.1"
---

In my last post, I described [getting React, Brunch and Phoenix working together]({% post_url 2015-8-8-setting-up-react-on-phoenix %}) in the most basic way possible. That worked, but I had trouble getting the NPM integration in Brunch 1.8.5 working with other NPM packages. As of [2.1.0](https://github.com/brunch/brunch/blob/master/CHANGELOG.md#brunch-210-jan-1-2016), the Brunch team has significantly improved the NPM integration, and that gives me a good opportunity to revisit it. You might want to check out the docs for [Brunch's NPM integration](https://github.com/brunch/brunch/blob/master/docs/config.md#npm-experimental) before we get started.

For this post, I generated a blank Phoenix 1.1.1 app using `mix phoenix.new`, but it shouldn't be much different to get working in an existing application.

Let's start by installing react and react-dom:

```bash
npm install react react-dom --save
```

The latest version of Brunch, which ships with Phoenix 1.1, doesn't include a JSX parser by default. We'll need to install a preset for that, as well as for the es2015 features we'll want to use.

```bash
npm install babel-preset-es2015 babel-preset-react --save-dev
```

We'll also need to configure brunch to use both of these presets. Modify your `brunch-config.js` file to include the following presets array:

```javascript
plugins: {
  babel: {
    // Do not use ES6 compiler in vendor code
    ignore: [/web\/static\/vendor/],
    presets: ["react", "es2015"]
  }
},
```

After that, we should be good to go. Let's bulid a simple HelloWorld component inside `web/static/js/app.js` to test it out.

```javascript
import React from "react";
import ReactDOM from "react-dom";

class HelloWorld extends React.Component {
  render() {
    return (<h1>Hello world</h1>);
  }
}

ReactDOM.render(
  <HelloWorld />,
  document.getElementsByTagName('main')[0]
)
```

Run `mix phoenix.server` from the command line, and open `http://localhost:4000/`. You should see the React component take over the main section of the page.
