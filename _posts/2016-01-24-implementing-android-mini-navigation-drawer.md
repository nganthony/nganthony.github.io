---
layout: post
title: "Implementing Android mini navigation drawer"
date: 2016-01-24
---

The Gmail app for Android tablets on Lollipop and above introduces a new navigation drawer called the mini navigation drawer. This variant of the navigation drawer allows the menu icons to be visible when the drawer is in the collapsed state. The mini navigation drawer is also specified in <a href="https://www.google.com/design/spec/patterns/navigation-drawer.html">Google's material design guidelines</a>.

{% include image.html img="images/android-mini-navigation.gif" title="title for image" caption="Example of a mini navigation drawer" width="90%" height="90%" %}

Unfortunately, there are no built in Android libraries to support this type of navigation drawer. The good news is we can use a layout called <a href="http://developer.android.com/intl/ru/reference/android/support/v4/widget/SlidingPaneLayout.html">SlidingPaneLayout</a> to implement this feature.

Create a layout resource file and set SlidingPaneLayout as your parent view. SlidingPaneLayout requires two child views: a master view and a detail view. The master view will contain a list of all our menu options and the detail view will contain the content. 

<script src="https://gist.github.com/nganthony/487fd3f6e9134899ec5b.js"></script>

The master view is contained inside a fragment. When creating multi pane layouts, it is good practice to seperate your panes in fragments. This keeps the code modular and each pane is contained in its own layout file. Add the master fragment class to your project. 

<script src="https://gist.github.com/nganthony/7547c7e8f4c1189ce208.js"></script>

Add the master fragment layout to your layout resources folder.

<script src="https://gist.github.com/nganthony/ab44bf76adff1b6a28a0.js"></script>

The master fragment contains a list view and uses an enumeration of menu options to populate the list.

<script src="https://gist.github.com/nganthony/1aadc7b8c602f0ea2aea.js"></script>

The master fragment also contains a custom array adapter that displays the list of menu options. The custom array adapter inflates a row layout for each menu option.

<script src="https://gist.github.com/nganthony/34c711231c621e37fec1.js"></script>

Add the row layout.

<script src="https://gist.github.com/nganthony/f678c9d9ef121461a9e0.js"></script>

Run your project and you should see something like this. When you swipe your finger right, the master layout will appear.

{% include image.html img="images/android-mini-navigation-step1.gif" title="title for image" caption="Example of SlidingPaneLayout" width="90%" height="90%" %}

To show the menu icons when the drawer is in the collapsed state, we simply add a margin left to the detail view. This shifts the detail view to the right revealing a portion of the master layout that is hidden underneath the detail view when the SlidingPaneLayout is in the collapsed state. 

<script src="https://gist.github.com/nganthony/da0a1eba5c68c5a8ad3a.js"></script>

Run your project again and this time you should see the menu icons on the left of the screen.

{% include image.html img="images/android-mini-navigation-final.gif" title="title for image" caption="Mini navigation drawer" width="90%" height="90%" %}

And there you have it! The mini navigation drawer is perfect for making menu options easily accessible to the user. If you want to try out the mini navigation drawer you can download the <a href="https://github.com/nganthony/MiniNavigationDrawer">sample project</a>!

