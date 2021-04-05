---
layout: post
title:  "Spaceship operator in C++20 is awesome!"
date:   2021-04-03 16:17:46 +0700
categories: c++
---
When you write a class in C++ with a plentiful amount of data, you soon realize you need some ways to compare objects of
this type. The new spaceship <=> operator in C++20 help you do that while keeping your code clean.

{% highlight cpp %}
(1 <=> 2) < 0
(2 <=> 1) > 0
(3 <=> 3) == 0
{% endhighlight %}

As can be easily seen, it works like strcmp in C when comparing two strings. In C++98 through C++17 you would have six operators to
overload: `==`, `!=`, `<`, `>`, `<=` and `>=` which is a boring chore.

