---
layout: post
title: Zbytočné volanie toString
tags: [it01, mistake]
---

V drvivej väčšine prípadov nepotrebujeme _explicitne_ volať na objektoch metódu `toString`, zavolá sa automaticky.
Teda takéto riadky: 

{% highlight java %}
System.out.println(triangle.toString());
{% endhighlight %}

{% highlight java %}
public String toString() {
    return "vertices: " + a.toString() + " " + b.toString() + " " + c.toString();
{% endhighlight %}

...môžeme nahradiť za


{% highlight java %}
System.out.println(triangle);
{% endhighlight %}

{% highlight java %}
public String toString() {
    return "vertices: " + a + " " + b + " " + c;
{% endhighlight %}

Pekné vysvetlenie je napríklad tu: [Explicit vs implicit call of toString](http://stackoverflow.com/questions/328661/explicit-vs-implicit-call-of-tostring)