---
layout: post
title: "cocurrent trap"
date: 2016-02-20 00:20:17 +0800
comments: true
categories: 
---

#### Apple prefer their developer use block. So they offer enumerate API which you can use block to replace the old for loop way. and because efficiency problem, Apple also add an concurrent enumerate API to solve this problem. Since I found it, i love the concurrent API and use it any time I can. 

#### But unfortunately, I made a big mistake. When I use enumerateKeysAndObjectsUsingBlock to look through all NSDictionary elements and change the dictionary value with some caculate. Something oops, the calculate result is obvious, but the dictionary sometimes contains "(null)=(null)" element instead the real result after calculate. And some extremely times, it crash! Why? because the unstable result, I suddenly realize the source is concurrent. 

#### I stop my job, try to figure out why this happens. I start to search Apple's document, and found something I have known before but never think about. The NSFoundation most mutable class is thread unsafe.But the usual way I used is to change dictionary in concurrent enumerate, that's why the result not predictable.

#### so in iOS world, we should never change mutable class in concurrent way. Unless use thread lock.
