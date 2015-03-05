---
layout: post
title: nth-child as a flexbox alternative for elastic rows 
---


The goal: A dynamic list of 'x' equally sized elements per row. If the last row is > x number of elements, each element should be equal in size and take up the full width of the row.  

Simple enough, right?  

However, we have a couple of stipulations:  

First of all, we cannot use [Flexbox](http://www.w3.org/TR/css3-flexbox/), and second, while a javascript solution would be fairly simple, our layout must be achieved via CSS _only_.  

In other words, the requirements are:    
	
1. Rows by default must have an explicit number of equally sized items.   
2. In cases where the last row has fewer items than the desired amount, the items of this row must each take an equal size and fill the entire row.  
3. We cannot use [Flexbox](http://www.w3.org/TR/css3-flexbox/)    
4. Javascript is not an option, must solve this using only CSS!


If you don't want to learn about how and why, just check out the codepen below or [here][css-only-codepen].  



<p data-height="350" data-theme-id="0" data-slug-hash="raKPYd" data-default-tab="result" data-user="d8nieldonaldson" class='codepen'>See the Pen <a href='http://codepen.io/d8nieldonaldson/pen/raKPYd/'>maintain max # of items in a row// css edition</a> by d8nieldonaldson (<a href='http://codepen.io/d8nieldonaldson'>@d8nieldonaldson</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>


##How It Works##

The scope of this post is a 'nth-child' based approach. However, there are other options. We will look at some of these in future, related posts.  

The nth-child is part of a larger group of CSS [pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) (see also, related: [pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements) )

If you're not familiar with nth-child selectors in CSS, [read this][nth-child-tricks], you can also play with Lea Verou's [demo](http://lea.verou.me/demos/nth.html).

The pseudo-class syntax is simple, but gives developers a lot of control over the presentation of the elements which it targets, all without the expense of having to clutter up the DOM with new selectors, such as CSS classes.

You probably knew that chaining pseudo-classes is allowed, so you have probably seen and or done something like this:

```css
li:first-child:hover{ ... }
```

which would allow us to style the hover state of the first list item.  

More importantly, we can extend this pseudo-class chaining to do some fairly sophisticated styling.

## Psuedo-class Chaining Implementation##

For our experiment, we will start with an unordered list of dynamically generated items. We want to have 4 items per row by default. For simplicity, we will use percentages as our measurement unit.

```css
li{
	width: 25% /* 4 items max per row or: 1/4 as a percentage */
}
```

The above works great, but only if all rows are 4 items. But what if there are a total of 5 items, and not 4 or 8? Let's solve for just this one case right now: a total of 5 elements.
So, the fifth item can be targeted like this:

```css
li:nth-child(4n + 1){ ... }
````

We know that the above selector will actually target the 1st, 5th, 9th et cetera element, which is not exactly what we need. What we want to do is to target the 1st, 5th, and so on _if_ it is also the _last_ 'li' in the 'ul'.  

Considering the ability to chain pseudo-classes, the answer may be apparent: 

```css
li:nth-child(4n+1):last-child{ width: 100% }
```
checkout the codepen below or [here](http://codepen.io/d8nieldonaldson/pen/ZYjpvQ)
<p data-height="197" data-theme-id="12800" data-slug-hash="ZYjpvQ" data-default-tab="result" data-user="d8nieldonaldson" class='codepen'>See the Pen <a href='http://codepen.io/d8nieldonaldson/pen/ZYjpvQ/'>ZYjpvQ</a> by d8nieldonaldson (<a href='http://codepen.io/d8nieldonaldson'>@d8nieldonaldson</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Ok, that was pretty easy, but what about the next case: the list is made up of 6 items. So, we will have one row with 2 items, each taking up 50% of the width.

```css
li:nth-child(4n+1):nth-last-child(2), li:nth-child(4n+2):nth-last-child(1){}
```
checkout the codepen below or [here](http://codepen.io/d8nieldonaldson/pen/MYBQvo)
<p data-height="201" data-theme-id="12800" data-slug-hash="MYBQvo" data-default-tab="result" data-user="d8nieldonaldson" class='codepen'>See the Pen <a href='http://codepen.io/d8nieldonaldson/pen/MYBQvo/'>nth-child elastic rows</a> by d8nieldonaldson (<a href='http://codepen.io/d8nieldonaldson'>@d8nieldonaldson</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>




[css-only-codepen]:http://codepen.io/d8nieldonaldson/pen/raKPYd/

[nth-child-tricks]:https://css-tricks.com/how-nth-child-works/

