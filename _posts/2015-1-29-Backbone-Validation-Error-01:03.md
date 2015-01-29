---
layout: post
title: Backbone Validation Error and Callback
---
After several hours of head bashing on why Backbone wasn't giving me an error callback from the .save method so I can display it to the user, I finally found the answer - it was taken out of Backbone 0.9.9

More information: (https://github.com/jashkenas/backbone/issues/2153)

Backbone validates before .save, so if you try to do something like what I did:

<pre><code>model.save({}, {
	success: function(){
		console.log('success');
	},
	error: function(){
		console.log('error');
	}
});</code></pre>
You will never see anything from Backbone's validation errors. You would still see the server responses if you did not implement validation in Backbone.

The way to get the validation error object is:
<pre><code>    if (this.model.validationError) {
      console.log(this.model.validationError);</code></pre>

Most of Stackoverflow responses were for the outdated Backbone version where error callbacks still work.
