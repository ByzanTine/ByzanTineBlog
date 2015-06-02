---
layout: post
title: "Learning Scala"
description: "notes on progfun-005 Coursera"
modified: 2015-06-01 22:40:59 -0400
category: [Programming Language]
tags: [Scala]
image:
  feature: 
  credit: 
  creditlink: 
comments: 
share: 
---

## Resource
- [Coursera intro to Scala](https://class.coursera.org/progfun-005)

There are two Course progfun-004 and progfun-005, however it seems that only progfun-005 autograder is still on.

## Scala is functional

#### No Mutable Variable

The core concept of Scala is no mutable variable inside a function. So there is no side-effect of those function if you followed this rule. However, the old school for loop won't work then

{% highlight c++ %}
for (int i = 0; i < 10; i++) {
  cout << i << endl;
}
{% endhighlight %}

Then the only tool you have is recursion which leads to accumulator
{% highlight scala %}
def foo(n: Int): Int = {
  def loop(acc: Int, n: Int): Int = {
    print acc
    if (acc == n) acc
    else loop(acc + 1)
  }
  loop(1, 10)
}
{% endhighlight %}
So it means you need to do recursion most of the time. But if you were in school learning imperative programming before, you may consider recursion means inefficient and stackoverflow, why recursion?

#### Lazy evaluation 

Lazy evaluation is part of the solution to those inefficient recursion that can't be solved by tail-recursion or other magic. But it's really fascinating. Consider this high-level example that presented in class

{% highlight scala %}
(1 to 1000) filter (isPrime) take 3
{% endhighlight %}

What is does simply reads as "From 1 to 1000, get all numbers that are prime, then take first 3". Hearing this, you may find it need to have isPrime run 1000 times. But actually we only need first 3. In imperative language, it's easy, you keep a counter. But you now coupled your "filter" with the "take" which may be not desirable. 

In Scala, lazy evaluation tackles this down. Namely, lazy evaluation make a varible be evaluated whenever it's needed. So the program evaluate each number in sequence, not first all filter then take. So it basically remains the expression power and coupled the two function inside the compiler. **BUT, DEBUG IS HARD**
