---
layout: post
title: "Hex my map up"
date: 2020-11-08
permalink: /hex-my-map-up/
published: true
tags: ["mapping", "hexagonal tiling", "hexagon", "data viz" ]
---

So I got all inspired by some of the US elction data viz, in partucular some of the mapping of states as abstract shapes with areas proportional to the number fo college votes they have. The issue is that without doing this, you see a lot less blue (Democrat) on a regular map than there really is (in terms of number of votes). This is due to many of the densely populated states tending to be blue-leaning (think north-east).

Well in Victoria, we have a similar issue, we have 88 lower house electorates, but 6 or 7 of them (by eyeball) cover more than half the state. So when you show a map of the electorates, these electorates swamp the viz, and the smaller (but just as populated) electorates shrink to invisibility.

![Plot of Victoria's electorates.](../assets/img/electorate_map.png "Plot of Victoria's electorates.")

I had a bit of a hunt for a library that dies what I want, but I couldn't see quite what I was after. This is a pretty rough attempt, but it is doing something not totally terrible.

![Plot of Victoria's electorates as equal area hexagons.](../assets/img/hex_map.png "Plot of Victoria's electorates as equal area hexagons.")

There's a bit to unpack here:

* Why is Melbourne so far west? Well, if you think about how much population is east versus west of the CBD, and the wedge-shape of Victoria (with more area to the west), it makes sence that Melbourne is pushed west.
* Coloured here, the regions (in Victoria, the lower house electorates, or "districts" roll-up into upper-house "regions") remain contiguous ... apart from the rural ones that get spread around the edge of the state. But then when you think about it, where *should* they be? They each cover wide stretches of the border of Victoria and touch many other regions.
* Eyeballing the districts I know, it looks like the neighbouring ones have remained roughly neighbouring.
* Overall, I think this is not a terrible representation, but I do think the algorithm for allocating the geometry (districts here) to hex tiles could use some tweaking.
* I have only tested this on a couple of Victorian regions ... it would be interesting to see what it looks like on onther geometries.

The code (such as it is) can be foune [here](https://gist.github.com/smcateer/d810f397f39b4153f0a555d0363b488c). 100% happy for anyone who finds it useful to use it ... it would be great to hear from you if you do.

(The bits that this code does, that I couldn't see in other libraries, it the bit in which the grid is automatically constructed to match the geometry of the original map, and the automatic allocation of geometries to tiles .. I get the feeling this tends to be done manually, but I am happy to be shown otherwise).
