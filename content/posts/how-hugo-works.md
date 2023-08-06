---
title: "How Hugo Works"
date: 2023-07-23T20:30:02-03:00
draft: true
---



How to link from inside hugo content?
[about](/about)

How to add image?
![my image](/pic.png) ~> this is inside the static folder


What's the layouts all about?
There are are singles and there are lists.

Hugo functions:
{{ partial "header.html" . -}}

For the poison theme:
base_of.html is the root node

The feed xss is bound to the word posts/post
