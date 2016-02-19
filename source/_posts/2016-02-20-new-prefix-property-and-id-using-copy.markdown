---
layout: post
title: "new prefix property &amp; id using copy"
date: 2016-02-20 01:43:16 +0800
comments: true
categories: 
---

1. property named using new prefix

in Objective-C, there’s many system keyword you can not use, besides that, the system also has banned some prefix method name.

Such as “init” prefix. the “init” prefix method only can be used when the method return instanceType value.because “initxxx” is designed to initilaize class instance by syntax.

the problem I met is another banned prefix method name I have never mentioned – “new”, when you use a “new” prefix method that means the same as “init” prefix to compiler syntax check – it should return intanceType value.

Don’t forget one more thing, property means getter and setter,so every property except @dynamic can be transfer to ‘propertyname’ and set’Propertyname” method. as a result,when you use new or init prefix as a property name,there’s no doubt an compiler error.

2. id using copy
As we know about copy in Objective-C, if you want an custom object support copy method, you need to make the class conform to NSCopying protocol and everything will be fine,you can call copy method which the real method “-(id)copyWithZone:(NSZone *)zone” will be called.

But sometimes, the custom object should be used as an heterogeneous way.the usual mechanism we used is make custom object as id type.but unfortunately, some times we should limit the id object to conform some protocol. in this condition, object call “copy” method will cause an compiler error describe like “can not find method define”.

Why id object conform protocol can not call “copy” method directly,let’s look deeply,id is an universal type, the compiler allow this type to call any method include “copy”,but when you specific the protocol id should conform,it will only call the method in protocol.any other method call will cause compiler error. and the base protocol “NSObject” do not contains the “copy” method.

finally the solution is when “id<xxx>” wants to use “copy” method, you should instead “id” with “NSObject *”,except your object is an NSProxy.
