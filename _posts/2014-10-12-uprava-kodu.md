---
layout: post
title: Úprava kódu
tags: [style, it01]
---

## Takto nie!
{% highlight java %}
public Triangle getSubTriangle(int i){
         if(!isDivided  || i>2 || i<0){
            return null;
        }
        else if (i==0){
                return sub0;}
            else if(i==1){
                 return sub1;
                }
                          else return sub2;
                        }
{% endhighlight %}
:crying_cat_face: :tired_face: :rage: 

## Takto je to lepšie

{% highlight java %}
public Triangle getSubTriangle(int i) {
    if (!isDivided || i > 2 || i < 0) {
	return null;
    } else if (i == 0) {
	return sub0;
    } else if (i == 1) {
	return sub1;
    } else {
	return sub2;
    }
}
{% endhighlight %}
:smiley: :beers:

---
_Toto je len ukážka úpravy kódu. Ukázaný kód nie je nutne (ne)korektný._
