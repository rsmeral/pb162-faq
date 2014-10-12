---
layout: post
title: Zásadná a typická chyba v porovnávaní a vracaní booleanov
tags: [it01, mistake]
---

{% highlight java %}
public boolean isDivided() {
    if(triangle == null) {
        return false;
    } else {
        return true;
    }
}
{% endhighlight %}
:disappointed: :thumbsdown:

{% highlight java %}
public boolean isDivided() {
   return triangle != null;
}
{% endhighlight %}
:heart_eyes: :thumbsup: :sparkles: