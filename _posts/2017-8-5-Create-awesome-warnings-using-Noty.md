---
layout: post
title: Create awesome warnings using Noty
img: /images/noty_post_icon.png
---

In mobile apps, we would like to show little warnings/dialogs/notification when an <b>important thing</b> happens. This important 
thing can be a download complete notification, a message alert or an update required warning. In this way we inform the user and they 
feel more confortable. For this purpose here is <a href="https://github.com/emre1512/Noty"><b>Noty</b></a>, an open source library for creating animated custom warnings/dialogs. 

<img src="https://camo.githubusercontent.com/17db940bf1e073549cb9db79081d2af1512f4992/68747470733a2f2f6d656469612e67697068792e636f6d2f6d656469612f336f67304953654b4d6446423879466764322f67697068792e676966">
<img src="https://camo.githubusercontent.com/e6b95b638ae3fd11b201ba05b23d8ef0ca45583d/68747470733a2f2f6d656469612e67697068792e636f6d2f6d656469612f7855413761503231524a496e756c627748752f67697068792e676966">

## Installation

Adding <b>Noty</b> to your application is super easy. Just add the line below to your app's gradle file and click <b>sync the project</b>

~~~
    compile 'com.emredavarci:noty:1.0.3'
~~~
<br>

## Usage

<b>Noty</b> is providing us to customize almost everything. You can find the full list of the customization methods <a href="https://github.com/emre1512/Noty/wiki/All-methods"><b>here</b></a>.

Now lets look at an example given at the <b>Noty</b> github page. You can also find all example codes <a href="https://github.com/emre1512/Noty/wiki/Examples"><b>here</b></a>.

The simplest usage of <b>Noty</b> is this:

~~~java
/*
 * rl is the layout we are working on.
 */
 RelativeLayout rl = (RelativeLayout) findViewById(R.id.myLayout) ;

 Noty.init(YourActivity.this
          ,"Your warning message" 
          ,yourLayout, Noty.WarningStyle.SIMPLE)
          .show();
~~~

Note that you need to get reference of the layout that you want to use <b>Noty</b>.

This example is only including a message. but we can also add an action button too. At below there is an example of that.

~~~java
 Noty.init(YourActivity.this, "Your warning message", yourLayout, 
    Noty.WarningStyle.ACTION)
    .setActionText("OK").show();
~~~

Ok, lets go deeper and add some customization to it.

~~~java
 Noty.init(YourActivity.this, "Your warning message", yourLayout,
        Noty.WarningStyle.ACTION)
        .setActionText("OK")
        .setWarningBoxBgColor("#ff5c33")
        .setWarningTappedColor("#ff704d")
        .setWarningBoxPosition(Noty.WarningPos.BOTTOM)
        .setAnimation(Noty.RevealAnim.FADE_IN, Noty.DismissAnim.BACK_TO_BOTTOM, 400,400)
        .show();  
~~~

We changed the default background color, tapped color, warning position and we gave an <b>animation</b> to it. <b>Noty</b> provides you 4 types of animations: Slide in, Slide out, Fade in and Fade out. You can do an animating warnings and change their animation durations also.

But what if we want to know when the user clicked on the warning or the action button? <b>Noty</b> also provides us handy callbacks. For the tap event, there is a <b>tapListener</b>. For clicking the action button, there is <b>clickListener</b>. Here are examples for them below.

~~~java
 Noty.init(YourActivity.this, "Your warning message", yourLayout,
        Noty.WarningStyle.SIMPLE)
        .setTapListener(new Noty.TapListener() {
            @Override
            public void onTap(Noty warning) {
                // do something...
            }
        }).show();
~~~

~~~java
 Noty.init(YourActivity.this, "Your warning message", yourLayout,
        Noty.WarningStyle.ACTION)
        .setClickListener(new Noty.ClickListener() {
            @Override
            public void onClick(Noty warning) {
                // do something...
            }
        }).show();
~~~

Note that you can also use all listeners at once.

The last thing I should mention is <b>animation listeners</b>. <b>Noty</b> is providing us animation listeners too. We may want to know the time when the animation started or stopped. The all listeners <b>Noty</b> providing are given below.

~~~java
 Noty.init(YourActivity.this, "Your warning message", yourLayout,
        Noty.WarningStyle.ACTION)
        .setAnimationListener(new Noty.AnimListener() {
            @Override
            public void onRevealStart(Noty warning) {
                // Start of reveal animation
            }

            @Override
            public void onRevealEnd(Noty warning) {
               // End of reveal animation
            }

      @Override
            public void onDismissStart(Noty warning) {
               // Start of dismiss animation
            }

            @Override
            public void onDismissEnd(Noty warning) {
               // End of dismiss animation
            }
        }).show();
~~~

You can use animation listeners with the tap and click listeners at once too.

<br>
## Conclusion

If you want to create colorful and animated warnings easly instead of boring toast messages and dialogs, you can try <b>Noty</b>. You will like it.





