---
layout: post
title:  "Getting started with multiprocessing in Python."
date:   2021-04-08 16:17:46 +0700
categories: python
---

In the modern world, processors have multiple cores to run different tasks in parallel. Here how to make your Python
apps utilize more one core to run faster.

Python has a module called `multiprocessing` that help you spawn processes.

{% highlight python %}
from multiprocessing import Process
{% endhighlight %}

Let's run a function called `f` 10 times using 10 different processes.

{% highlight python %}
from multiprocessing import Process
import time

def f(x):
  print(f"x = {x} starts")
  time.sleep(x)
  if x == 5:
    print("Hey")
  print(f"x = {x} ends")

[Process(target = f, args = (i,)).start() for i in reversed(range(10))]

{% endhighlight %}

See what happens!