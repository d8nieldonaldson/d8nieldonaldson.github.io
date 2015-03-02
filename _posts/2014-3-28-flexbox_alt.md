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



<p data-height="394" data-theme-id="0" data-slug-hash="raKPYd" data-default-tab="result" data-user="d8nieldonaldson" class='codepen'>See the Pen <a href='http://codepen.io/d8nieldonaldson/pen/raKPYd/'>maintain max # of items in a row// css edition</a> by d8nieldonaldson (<a href='http://codepen.io/d8nieldonaldson'>@d8nieldonaldson</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>


##How it works##

The interesting part is chaining nth selectors in CSS  
	consider the following:


```css
li:nth-child(4n+1):nth-last-child(1){ ... }
```




[css-only-codepen]:http://codepen.io/d8nieldonaldson/pen/raKPYd/

