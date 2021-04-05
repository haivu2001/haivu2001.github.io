---
layout: post
title:  "Decorators decorate your functions in Python."
date:   2021-04-05 16:17:46 +0700
categories: python
---

You might have already seen something like this:

{% highlight python %}
@app.route('/')
def index():
    return "Hello, world!"
{% endhighlight %}

What it does is simplify how you call high-order functions. 

For example: 

{% highlight python %}
def greet_hai(greeter):
  greeter("hai")

@greet_hai
def japanese_greet(name):
  print("こんにちは " +name+"さん")
{% endhighlight %}

...is same as:

{% highlight python %}
def greet_hai(greeter):
  greeter("hai")

def japanese_greet(name):
  print("こんにちは " +name+"さん")

greet_hai(japanese_greet)
{% endhighlight %}

### Modifying behaviors

You can modify behavior of a function by just returning a new function.

{% highlight python %}
def bye(greeter):
  def say_bye(name):
    print("Bye " + name)

  return say_bye

@bye
def hello(name):
  print("Hi "+ name)

hello("hai")
# print Bye, hai instead.
{% endhighlight %}
