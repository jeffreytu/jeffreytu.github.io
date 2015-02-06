---
layout: post
title: Head-bashing CasperJS AJAX Syntax
---

I have been working on making a small script that uses CasperJS to navigate through a website and read data. The purpose of the script is to essentially count the number of entries of a particular resource and send an AJAX request to an e-mail API and the user receives a text message. I'll talk about why you don't need a SMS API in another post.

The AJAX was the most difficult part to implement due to a lack of resources for using it with CasperJS. My first instinct wasn't to look in the documentation for AJAX, but to start with what I know - jQuery.

```javascript
 	$.ajax({
 		type: "POST",
 		async: false,
 		contentType: "application/json",
 		crossDomain: true,
 		url: "http://www.google.com",
 		data: {},
 	})
```
Using jQuery in CasperJS is not very easy. Because jQuery is a DOM manipulation framework, CasperJS requires jQuery to be wrapped in a specific `casper.evaluate(function(){..})` in order to access the DOM. Ok.. so I'll just wrap my AJAX in the `evaluate`, but of course there's more to that. 

Since I'm doing more with my stript, such as reading and checking values, I needed to pass variables globally. The evaluate (or DOM environment) is separate from the CasperJS environment, so you can't just assume normal JavaScript scoping rules. There's a nice diagram on the documentation:

[http://casperjs.readthedocs.org/en/latest/modules/casper.html#evaluate](http://casperjs.readthedocs.org/en/latest/modules/casper.html#evaluate)

The only way pass the variables from CasperJS to the DOM is something like this:

```javascript
var file = "some file";
var data = "some data";

casper.thenEvaluate(function(file, data) {
    try {
        console.log(file);
        console.log(data);
    } catch (e) {
        console.log("Caught");
    }
}, file, data);
```
Although I now understand the passing of variables in environments, I still was not making progress so I decided to look at the CasperJS documentation for AJAX.

In the documentation we are given an example:

```javascript
var data, wsurl = 'http://api.site.com/search.json';

casper.start('http://my.site.com/', function() {
    data = this.evaluate(function(wsurl) {
        return JSON.parse(__utils__.sendAJAX(wsurl, 'GET', null, false));
    }, {wsurl: wsurl});
});

casper.then(function() {
    require('utils').dump(data);
});
```
This seemed a little daunting at first, but it's essentially the same as jQuery +  __utils__, which is a client-side utility for accessing the DOM in CasperJS.

I was having better success using this since the email API I am using, [Email Yak](https://www.emailyak.com/), was giving me validation errors. For a period of time, I was getting a response:

```
{
    "Message": "Invalid JSON/XML. Malformed JSON/XML syntax. During Beta, needs to be JSON.",
    "Status": 402
}
```

There was absolutely nothing wrong with my JSON data, but how I was sending the request was bad. It essentially came out to be two things:

- `JSON.stringify(data)`
- `{ contentType: "application/json" }`

These are the optional parameters when using the CasperJS `sendAjax`. My entire AJAX call that worked looked something like this:

```javascript
casper.start('http://www.emailyak.com/', function() {
    data = this.evaluate(function(wsurl, data) {
        return JSON.parse(__utils__.sendAJAX(wsurl, 'POST', JSON.stringify(data), false, { contentType: "application/json" }));
    }, {wsurl: wsurl, data:data});
});
```
