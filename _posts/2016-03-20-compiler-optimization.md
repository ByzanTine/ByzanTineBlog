---
layout: post
title: Compiler Optimization
modified:
categories: 
excerpt:
tags: []
image:
  feature:
date: 2016-03-20T21:38:56-07:00
---

## Resource
- [Dragon Book Chapater 8-12](http://www.amazon.com/Compilers-Principles-Techniques-Tools-2nd/dp/0321486811)
- [Awesome Summary](https://github.com/jivimberg/cs243-summary)

## Dataflow Analysis 

A simple problem we want to solve looks like
{% highlight python %}
a = 3
b = a
c = b
print c
{% endhighlight %}

which is equivalent to 
{% highlight python %}
print 3
{% endhighlight %}

It's indeed intuitive to human that this optimization is correct, but it raises complexity when compiler deals with this problem. The above example used two techiques [Constant Propagation](https://en.wikipedia.org/wiki/Constant_folding#Constant_propagation) and [Copy Propagation](https://en.wikipedia.org/wiki/Copy_propagation).

#### Why?

Because the Goal is to optimize the program while retaining the **correctness**. Branching will greatly raise the cost of retaining correctness. So the [Control Flow Graph](https://en.wikipedia.org/wiki/Control_flow_graph) comes into play. Whatever optimization we do, we need to ensure all path results in the same as before. 

## Instruction Scheduling

#### Cache

Consider we only have one register, here is a snippet.
{% highlight python %}
a = 3
c = 2
print a
print c
{% endhighlight %}

Notice when **print a** we need to reload **a** from memory since cache is tiny. However, it's possible to rewrite the program into 
{% highlight python %}
a = 3
print a
c = 2
print c
{% endhighlight %}

By some simple [Data Dependence](https://en.wikipedia.org/wiki/Data_dependency) Analysis, we can assure out optimization is correct. 


#### Software pipelining

Consider a loop.
{% highlight c++ %}
int a[4];
for (int i = 0; i < 4; i++) {
	a[i] = 1;
}
{% endhighlight %}

By default, this loop will run sequentially on one core. But it's obvious that we want to achieve parallism when we have multiple processors. However, we do need to introduce complexity to handle data dependency and resource constraint.

## Grabage Collection

[Reference Counting](https://en.wikipedia.org/wiki/Reference_counting) and [Mark and Sweep](https://en.wikipedia.org/wiki/Tracing_garbage_collection) are way too introductory.

A interesting topic is generational garbage collection. The assumption is variables are mostly young (create and delete soon). Whenver objects that are reachable after one garbage collection pass, it would probably pass the next garbage collection pass. So it's wise to ignore them in the next few garbage collection pass. So we gain the perfomance by ignoring things like global objects.