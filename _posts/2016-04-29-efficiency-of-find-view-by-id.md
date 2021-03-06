---
layout: post
title: "Efficiency of findViewById"
date: 2016-04-29
---

A very common method that is used when developing Android applications is the method <i>findViewById</i>, which retrieves a view from a view hierarchy based on an identifier. This seemingly harmless method may in fact cause performance issues in your Android application if used carelessly. 

<i>findViewById</i> uses depth first search starting at the root of your view hierarchy in order to find the view with the identifier you have specified. To fully understand this, let's take a look at the Android source code to see how <i>findViewById</i> is implemented for the ViewGroup class. 

<script src="https://gist.github.com/nganthony/83f2c847422ec017d3b856b827ca2b4d.js"></script>

<i>findViewById</i> first starts off by checking if the identifier is valid. It then calls <i>findViewTraversal</i>, to search for the view with the specified id. <i>findViewTraversal</i> checks if the current view is the view we're looking for. If it's not, then we traverse through the child views by recursively calling <i>findViewById</i> on each of the children. 

An interesting takeaway from this is that since we're traversing through the view hierarchy by checking all the views, we should keep our views as simple as possible. If we have an overly complicated view with a lot of unneccessary nesting, then <i>findViewById</i> will take longer to execute.

Another takeaway is that you can find all the views that you need in your activity or fragment by calling <i>findViewById</i> in the onCreate and onCreateView methods respectively, and storing references to those views so that you will no longer have to find the views in your view hierarchy again.

In a future post, I'll talk about how we can use what we've learned about <i>findViewById</i> and apply them to ListViews and RecyclerViews for smooth scrolling. 