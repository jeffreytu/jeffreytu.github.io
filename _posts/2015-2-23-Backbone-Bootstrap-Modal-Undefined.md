---
layout: post
title: Why is the bootstrap .modal function undefined in Backbone?
---

So you want to render a .modal from bootstrap.js in Backbone, but get `undefined` when calling it?

Inside your backbone.view.js, you probably be setting up a render function to render the modal:
```
render: function() {
  var context = this.model.toJSON();
  this.$el.html(this.temp(context)).appendTo(document.body);
  this.$el.modal();
  return this;
},
```
<hr>
<b>The Problem</b>

So why would you be getting undefined on the line `this.$el.modal();` when you've included the bootstrap.js in your html file?
<b>The bootstrap.js (included in the HTML) is not extending the jQuery version that was being revealed to Backbone via Backbone.</b>
<hr>
<b>The Solution</b>
- Remove any jQuery and Bootstrap js file references in the HTML because they should be required in Backbone already
- Set window.jQuery in your main.js file that also requires Backbone,<br>e.g. `Backbone.$ = exports.$ = window.jQuery = require('jquery');`
- Require bootstrap, this means `npm install --save bootstrap`

Doing all these ensures that Backbone extends the correct version of jQuery, making the bootstrap.js function available. However, since we are setting jQuery to the global window, this isn't the best solution. If you are using something similar to Browserify in your application, using a shim for bootstrap to set it dependent on jQuery might be the best solution.
