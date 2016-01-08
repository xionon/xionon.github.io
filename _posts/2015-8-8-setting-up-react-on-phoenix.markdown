---
layout: post
title: Setting up React on Phoenix
---

[I've revised this post for Phoenix 1.1 and Brunch 2.0. Click here for the most recent instructions on setting up React on Phoenix.]({% post_url 2016-01-08-revised:-setting-up-react-on-phoenix %})

For my day job, I mostly write APIs with Rails, but I like to play around with other frameworks whenever I have a chance.  Lately, I've been playing with [Phoenix](http://phoenixframework.org/), which is a full-stack web framework for [Elixir](http://elixir-lang.org/), and [React](http://facebook.github.io/react/), which is a Javascript library from Facebook. This post describes how to get them working nicely together.

*Important: This tutorial requires relatively new features in Brunch and Phoenix, namely the brunch/npm integration. Please ensure your versions of Phoenix and Brunch are up-to-date:*

```bash
mix -h | grep phoenix
mix phoenix.new       # Create a new Phoenix v0.16.1 application

cat package.json | grep '"brunch":'
    "brunch": "^1.8.5",
```

For simplicity, I'm going to be working from a newly scaffolded app, but similar instructions should work for including React in an existing project. First off, we need to install react via NPM:

```bash
npm install react --save
```

This adds the react source to `node_modules`, and updates `package.json` to reflect the new dependency. React has a pretty complex source tree, so we have to tell Brunch which file we mean when we try to import it later. Add an `"overrides"` section to your `package.json` file, right after the `"dependencies"` section:

```json
"overrides": {
  "react": {
    "main": "dist/react.js"
  }
}
```

Let's setup a simple HelloWorld component, to make sure everything worked. Add this to `web/static/js/app.js`:

```javascript
import React from "react";

let HelloWorld = React.createClass({
  render: function() {
    return (<h1>Hello, world!</h1>);
  }
})

React.render(
  <HelloWorld />,
  document.getElementsByClassName('container')[0]
);
```

This will take over the default marketing container that Phoenix creates for you. Load `http://localhost:4000/` in your web browser, and all you should see is a big "Hello, World!" message.

There's a few interesting things going on here to note:

  - Brunch is already configured to let us use modern Javascript syntax, without any additional configuration on our part
  - Once we told it where to look, brunch was able to automatically pull in React from our NPM module, and make it available in the browser. In theory, this would make creating a prerendering app fairly straightforward
  - Brunch automatically handles transpiling JSX syntax to usable JS, without needing any special configuration or file extensions

For my next post, I'll explore linking Phoenix's websockets up to a React component to give us real-time updates from the server.
