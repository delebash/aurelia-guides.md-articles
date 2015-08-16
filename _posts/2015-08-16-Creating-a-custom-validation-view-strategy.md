---
layout: post
title: "Creating a custom validation view strategy" # Change this here and in the filename
date: 2015-08-16 # Change this here and in the filename
comments: true # this only matters if you have disqus comments enabled in your _config.yml file
categories: # feel free to add categories
---

**david-martyn-ford** defines this post as: When attempting to implement validation using the **aurelia-validation** plugin I ran into some problems with the demos automatically updating the UI accordingly to the validation result but with my app it didn't work. 

After taking a look at the source code on how the plugin updated the UI side of things I discovered there was a Bootstrap view strategy. In LOB apps the chances of you using bootstrap is very slim so I think a blog post showing you how to setup your own view strategy would be very beneficial to other developers who are looking to implement client side validation.
