---
layout: post
title: flexbox alternative for elastic rows 
---

needed a way to keep a dynamic list of items looking tidy w/o flexbox.  
the requirements:  
	
1. rows by default would have an explicit number of equally sized items.  
2. if the last row had fewer items, the items would each take an equal size and fill the entire row.  

[check out the codepen][main-codepen]

for example, here is an example of a list with rows of 4 items each

![default view 4 items](/images/4_items.png)

but if the last row only had 3 items, all 3 should be of an equal width, but they should all take up the full horizontal space of the list. so 33.333% instead of 25%

![default view 3 items](/images/3_items.png)

and with just 2 items in the last row, they should be 50% width

![default view 2 items](/images/2_items.png)

and 1 fullwidth item

![default view 1 items](/images/1_item.png)


[main-codepen]:http://codepen.io/d8nieldonaldson/pen/zxjyRE

