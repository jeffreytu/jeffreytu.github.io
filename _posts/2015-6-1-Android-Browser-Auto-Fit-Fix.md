---
layout: post
title: Android Browser Auto-Fit Text Fix
---

My latest discovery while making one of my client's design mobile-friendly, was finding that the Android browser has an auto-fit text option pre-selected. When viewing my client's page on the phone, text would become squished to one-third of the width of the screen. This only happened with the Android browser. The Chrome mobile browser displayed the mobile page perfectly.

Spent many hours fumbling with the CSS and with no solution, I decided to look at the settings of the Android browser on my phone, and I see an Auto-Fit Text option selected. Turned that off and what do you know, the text fit perfectly.

So now the solution is to find something to work around this pre-selected android option without doing something very hacky. Did some Googling and of course other developers had the same problem:

http://stackoverflow.com/questions/8508889/android-autofit-mode-causing-issues-with-css-width-in-web-page

```
background-image:url(data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==); 
background-repeat:repeat;
```
The workaround is simply adding a background to the text area, either a <p> or <span> ect.

Oh Android.
