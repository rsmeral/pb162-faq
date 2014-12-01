---
layout: post
title: What's wrong with while(true)?
tags: [java, style, bestpractice]
---

> Should I replace it with `while(1==1)` or some other tautology?

<span class="lead">
Yes, someone actually asked this. No, you shouldn't. Read on to learn why.
</span>

The loop constructs used in Java (and most other languages) have a stopping condition as their argument, not for tautologies, not for fun, but in the first place for readability. You can always hack up a loop like


    while(true) {
        // some ugly conditional break
    }

You are making it a tiny bit easier for yourself by not formulating the stopping condition clearly in the beginning, but a lot harder for anyone reading your code afterwards. 

I call these loops "lazy loops", where in this case, the word lazy is in no way connected to the concept of laziness as used in some programming concepts, like lazy initialization. This time, it signifies the sheer laziness of the code's author. It appears like the author doesn't take the time to think about the loop's boundaries and decides to take care of them later using `break`, `continue` or `return`.

### An example

Let's see how two simple loops with the same functionality compare if we read them out loud. One lazy, one good.

{% highlight java %}
while(true) {
    eat(makeSandwich());
    sandwichesEaten++;
    if(sandwichesEaten == 4) {
        break;
    }
    hungry = checkIfStillHungry();
    if(!hungry) {
        break;
    }
}
{% endhighlight %}

> *From now on and forever, your task is to make sandwiches, eat them and count how many you've eaten. However, once you've eaten four, feel free to stop. Then also check if you're hungry. If not, you don't need to make any more.*

versus

{% highlight java %}
while(sandwichesEaten < 4 && hungry) {
    eat(makeSandwich());
    sandwichesEaten++;
    hungry = checkIfStillHungry();
}
{% endhighlight %}

> *While you're hungry and you've eaten less than four sandwiches, keep 'em comin'!*


Two things should be clear from these examples:

* I was hungry while writing this post
* you should think before using `break` &ndash; in most cases, it can and should be avoided

For a less hunger-infused view on the issue of ugly loops, I suggest you google around and you might find [other](http://stackoverflow.com/a/595714) [opinions](http://stackoverflow.com/questions/18188123/is-it-bad-practice-to-use-break-to-exit-a-loop-in-java).

### A final warning

{% highlight java %}
while /* it's */ (true) {
    /* you can */ 
    try {
        using(this, kindOfLoop);
        /* you should */ 
        hope( i , !will);
    } catch (You doingIt) {
         if(you) continue;
         might(your.code); break;
    }   
}
{% endhighlight %}

*Remember*: if you feel like using a `break` &ndash; take a break instead.