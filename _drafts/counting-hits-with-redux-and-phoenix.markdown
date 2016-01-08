---
layout: draft
title: "Counting hits with Redux and Phoenix"
---

I've written two blog posts on wiring up React and Phoenix, but I have yet to write anything that actually involves code. Let's change that, and build a simple hit counter using Phoenix, React, and [Redux](https://github.com/rackt/redux).

First, we'll generate a new application, county:

```bash
mix phoenix.new county
# snip
Fetch and install dependencies? [Yn] y
# snip
cd county
mix ecto.create
```

We'll need to install React, ReactDOM, and the babel transformation presets.

```bash
npm install react react-dom --save
npm install babel-preset-es2015 babel-preset-react --save-dev
```
