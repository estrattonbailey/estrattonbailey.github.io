---
layout: post
title Weekend Project: Beer Club
excerpt: Hello
---

> Update 6/20/15: just migrated this post to my new site, fun to read over it again. I became a developer full time just over five months ago, and it's great to see how far I've come since writing this.

* * *

**TL;DR:** Project: designing and building a custom Wordpress site in a weekend. Skip ahead and [view the finished product.](http://beerclub.ericbailey.co)

* * *

**11:18am**

# The Beginning

As it's 11:18am on Saturday morning, I'm getting a late start at this. But that's what makes it fun! As an exercise in Wordpress theme dev and web design, I'm going to attempt to redesign one of my side projects, [Beer Club](http://illhaveabeer.com), and build it onto a custom Wordpress theme over the next day-and-a-half.

I'm doing this for a couple of reasons. First, Beer Club has always been a group of people, but up until now, I'm the only one with access to the blog. With accounts, our core group will be able to share every inebriated moment, wherever they are. Second, I want archives, and Tumblr doesn't really cut it. Looking for an IPA in NYC? Search for it. The highest rated stout in Vegas? You'll be able to find that too. (I might not get to this this weekend, but that's the idea)

Third, I want Beer Club to grow. The original founders now live as far as Vegas, Chicago, and New York. The beer adventures don't stop once we leave Iowa, and I want to capture those foreign experiences for people to engage with and reference, should they travel to those locations.

And that's the larger idea of Beer Club: a network of people, who are passionate about beer.

* * *

**11:33am**

# Logo Redesign

So, probably not the best time for this, but I've had the idea of making the logo more 'badge-like' for a couple weeks, and I wanted to give it a shot. I whipped this up just now, and it still needs some work, but I'll roll with it for now.

[![Screen Shot 2014-10-25 at 11.35.15 AM.png](https://d23f6h5jpj26xu.cloudfront.net/ssjyllladlbfjw_small.png)](http://img.svbtle.com/ssjyllladlbfjw.png)

> Love it, hate it? [Tweet me!](http://twitter.com/estrattonbailey)

Next step, wireframes. Haven't given them much thought, so this could take a while.
 
* * *

**1:18pm**

# Wireframes

These are rough, but I like the direction. Currently, the live site focuses on the images, but if the future, I want it to be a resource as much as it is a community. So I want to place a search box prominently on the home page that will search any and all tags associated with the beers. 

On the single post page, I want to maintain the simple rating system we use currently – zero, one, or two thumbs up – while adding meta info for the beers like ABV, IBU, and where the photo was taken.

{% include images/full.html image="http://img.svbtle.com/fbctpvvrkubqa.png" caption="This is the caption." %}

> Beer Club: made with beer & love.

* * *

**2:59pm**

# HMTL Build Out

I've started to build out the site using [SVBSTRATE](http://svbstrate.io). I've got the preliminary styles worked our and a bit of structure, so it should speed up from here.

I'm kind of excited right now because I took a moment to look specifically at the `::-{prefix)-placeholder` pseudo-classes/elements and created a neat little function. I've had to mess with them before, but it's kind of a neat little piece of code that I'll definitely use in future projects.

Here's the function, pretty straightforward:

```css
@mixin placeholder($color, $padding) {
    &::-webkit-input-placeholder {
        color: $color;
        padding: $padding;
    }
    &:-moz-placeholder {
        color: $color;
        padding: $padding;
    }
    &::-moz-placeholder {
        color: $color;
        padding: $padding;
    }
    &:-ms-input-placeholder {
        color: $color;
        padding: $padding;
    }
}
```

Which I call in the template file like this:

```css
.beerSearch {
    @include placeholder( lighten($primaryColor, 10%), 8px 0px 0px 0px);
}
```

Which outputs this:

```css
.beerSearch::-webkit-input-placeholder {
    color: #f37e84;
    padding: 8px 0px 0px 0px; 
}
.beerSearch:-moz-placeholder {
    color: #f37e84;
    padding: 8px 0px 0px 0px; 
}
.beerSearch::-moz-placeholder {
    color: #f37e84;
    padding: 8px 0px 0px 0px; 
}
.beerSearch:-ms-input-placeholder {
    color: #f37e84;
    padding: 8px 0px 0px 0px; 
}
```

> How neat is that?

See it at work on my sandbox page [here.](http://ericbailey.co/sandbox/beerclub_base/)

**Time for lunch.**

* * * 

**4:41pm**

Wrapping up styles for the home page, off canvas menu also almost completed. Demo [here.](http://ericbailey.co/sandbox/beerclub_base/)

* * *

**11:29pm**

# Home Page: I think it's done?

Only spent about 2.5 hours on the site this evening, had friends to see and baseball to watch. But I managed to finish up the home page and build an off canvas menu.

Skipping high-fidelity mockups is a pain in the ass because I find myself designing in the browser, which is time consuming, and my fingers default to Cmd+Shift+R now. But I'd say it looks nice. 

Tomorrow I need to set up the other template pages and then migrate the HTML to the Wordpress Base. If I can have that done by noon, I'd be stoked! Then the rest of the day can be debugging and 'blogging' – *read: drinking beer*.

Check out the **[sandbox site](http://ericbailey.co/sandbox/beerclub_base/)**, and try it on your phone!

* * *

**Time for a beer**

[![IMG_2392.JPG](https://d23f6h5jpj26xu.cloudfront.net/a65d6m5exjskrg_small.jpg)](http://img.svbtle.com/a65d6m5exjskrg.jpg)

> Ruination IPA by Stone Brewing Co.

*Read about it tomorrow on the new blog. I'll have a better photo then too.*

* * *
# Day 2
* * *
**10:20am**
# Finishing HTML, Begin Merging with Wordpress
Hoping to wrap up HTML before lunch, dive into Wordpress after. Need to clean up the jQuery controlling the menu, I want to be able to click off and have it slide back as well. Blog listing and single post pages shouldn't take me too long to style.

* * *

**11:31am**

Still finishing HTML, almost done with the single post page. I'll start merging with Wordpress after lunch, really excited to get started!

I also wrote a nice little jQuery function for the menu slide out. I didn't realize you could make a `.target` listener a jQuery object, so to begin with I was trying to make an array of classes using `className.split(" ")`, which was just gross and didn't work very well. What I ended up with was this:

```javascript
$('body').click(function(e){    
    if ( $(e.target).is(".js-menuToggle") ) {
        $(".mainMenu").toggleClass("mainMenu--visible");
        $('body').toggleClass('js-fixScroll');
    }
    else {
        $(".mainMenu").removeClass("mainMenu--visible"); 
        $('body').removeClass('js-fixScroll');
    }
});
```

This method still has some lag issues at times. Could it be cause by my having two elements with the class `js-menuToggle`? Hopefuly someone who knows jQuery better will read this and call me out. It does work fairly well though: it paralyzes scrolling and the menu can be hidden by clicking anywhere else on the screen. I'll leave it for now.

**[Demo](http://ericbailey.co/sandbox/beerclub_base/)**

* * *

**2:09pm**

# My developer friends are awesome.

Just got back from lunch to find my questions answered! It not only works flawlessly now, but I learned something in the process. 

First suggestion came from [Stephen Ausman](https://twitter.com/sausman), who reminded me that storing variables saves the script having to search the DOM each time you want to grab an object. Very smart, going to remember this one from now on:

```javascript
// Store $('body') and $('.mainMenu') in variables outside of the event handler
// This way they only need to be looked up once and not on every click
var $body = $('body');
var $mainMenu = $(".mainMenu");
 
$body.click(function(e){
    // Since you're only checking the className you can use `hasClass` here instead of `is`
    // http://jsperf.com/jquery-is-vs-hasclass
    if ( $(e.target).hasClass("js-menuToggle") ) {
        $mainMenu.toggleClass("mainMenu--visible");
        $body.toggleClass('js-fixScroll');
    }
    else {
        $mainMenu.removeClass("mainMenu--visible"); 
        $body.removeClass('js-fixScroll');
    }
});
```

This worked perfectly, but I was still experiencing the click problems from before. Thankfully, [Ross Johnson](https://twitter.com/rossdjohnson) pointed out what should have been obvious to me: that the problem stemmed from clicking on the children of `js-menuToggle` which then invalidated the `e.target` check.

So one option is just to add a class of `js-menuToggle` to the parent element and its children. But he suggested another option as well, using `.on()`: 

```javascript
$body.on('click', '.js-menuToggle', function(){
    ....
});
```

Which is brilliant. I've had to use `.on()` once before, over a year ago for a [AJAX experiment](http://ericbailey.co/archive/gehry/) I was working on, since it dynamically binds the action to the listener (Did that make sense? Something like that.) and child elements. Glad he brought it to mind, should have used that to begin with! 

So here's what I ended up with – an amalgamation of Steven's, Ross's, and my own code:

```javascript
// Variables from Stephen Ausman
var $body = $('body');
var $mainMenu = $(".mainMenu"); 
  
// Use of .on() from Ross Johnson  
$body.on('click', '.js-menuToggle', function(){

    // My measly contribution
    if ( $mainMenu.hasClass("mainMenu--visible") ) {
        $mainMenu.removeClass("mainMenu--visible"); 
        $body.removeClass('js-fixScroll');
    }
    else {
        $mainMenu.toggleClass("mainMenu--visible"); 
        $body.toggleClass('js-fixScroll');
    }
});
```

And that's that. It works! Now time to kick it in gear, not much time left.

* * *

**3:35pm**

# Here goes nothing.

HTML is done! Check out the **[demo here.](http://ericbailey.co/sandbox/beerclub_base/)** Time to merge it with Wordpress and get crackin'. 

I've never worked with Wordpress search, so that should be interesting. I'm excited to give it a shot!

* * *

**6:33pm**

# It's alive.

Wordpress is running. I have a static front page, a post listing page, single post page, and the archives set up. Menus, tags, etc, all pulling fine. But I haven't started the search stuff yet (which I've never done before), so that may take some time.

Looking forward to getting it up on a subdomain and posting the first beer later tonight. Gotta go make a sandwich now. 

[![Screen-Shot-2014-10-26-at-6.36.22-PM.jpg](https://d23f6h5jpj26xu.cloudfront.net/4b67pi4ewylx3w_small.jpg)](http://img.svbtle.com/4b67pi4ewylx3w.jpg)

> Isn't it beautiful? 

* * *

**9:57pm**

# Damn you, searchform.php

To be honest, things are looking good. Wordpress is working just like it should, and I'm not using any messy plugins to make it happen (besides Advanced Custom Fields, but that hardly counts).

I did run into the fact that showing popular tags outside The Loop isn't exactly easy. That's a little frustrating. But not a huge deal just now, I can figure that out later.

The main problem I have – and the only one preventing me from putting the damn thing live and calling it a day – is that *the search form only searches one post right now.* Tell me that isn't weird. I'm using essentially the default searchform.php template, with no custom post types either. Having some trouble finding a solution online for it.

I'm going to troubleshoot a few more minutes, but if I can't get it I'll push it live and share it on GitHub to see if anyone has any ideas.

* * *

**11:01pm**

Technically I'm 17 minutes away from my deadline, but I also just opened a beer.

[![Freudian-Slip.jpg](https://d23f6h5jpj26xu.cloudfront.net/84sarlrraazxw_small.jpg)](http://img.svbtle.com/84sarlrraazxw.jpg)

> It's a 10.3% kind of night.

So I'm all set to push this thing live. I found out that I wasn't just searching one post, I was searching titles (apparently). I tried for almost an hour to write a function that would allow the search request to crawl everything in a post –  content, tags, etc – to no avail.

But [Scott Polhemus](https://twitter.com/ScottPolhemus) saved the day! He pointed me towards [Search Everything](https://wordpress.org/plugins/search-everything/), which was incredibly easy to install and implement. And it seems to have solved the problem. Now, visitors to the site should be able to type in any search parameters they would like to and be returned results! Stellar, and convenient when you're thirsty.

Pushing it live now.

* * *
# Day 3 (technically)
* * *
**12:37am**
# Weekend Project: Success
At this point, the site is up, it's running, and it looks pretty good (for being designed and built in a weekend). Only one post for now, I'll migrate the previous posts from the [previous site](http://illtakeabeer.com) later this week + get a few of the other members up and running and posting their beer excursions. Look for that.

## Next steps:
Improve profile pages. I want to build out the pages to include a biography, relevant links, favorite beers, and average ABV based on posts (not sure how I'll do that one, but it could be fun).

I still really want a way to access the most popular tags outside The Loop – say inside the menu for instance. That way, on pages other than the main page that has the search bar, a viewer would be able to browse by the most common beers types/tags.

The menu no longer closes when you click off it. Couldn't tell ya' why, but I want that to work again as well.
* * *
And I'm sure I'm going to find many other things I want to improve or change. Or if you're looking at the site, feel free to [tweet me](http://twitter.com/estrattonbailey) suggestions/bugs.
* * *
**Overall, I'm stoked. This is my first complete Wordpress build that I've published, and I managed to do it in a weekend (almost). Starting at 11:18am on Saturday, I'm now 37 hours and 30 minutes into the project, but I'm very proud of what I've built in that time. Also, I'm really glad I blogged along the way. It'll be fun to look back on, I'm sure. I might do this more often.**

Better finish this beer now.
* * *
# [VIEW THE FINISHED PROJECT](http://beerclub.ericbailey.co)
* * *
