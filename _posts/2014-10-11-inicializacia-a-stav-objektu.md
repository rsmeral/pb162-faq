---
layout: post
title: Inicializácia, stav objektu, použitie triedy
tags: [it01, design]
---

Možno ste našli v poznámkovom bloku niečo ako:

> Zbytocna inicializacia atributov Triangle

Problémom v 1. iterácii je, že sa v nej máte naučiť používať getters a setters, a preto vám vyslovene zakazuje používať konštruktory.
Výsledná trieda ale má potom tak trochu zvláštnu formu, nie bežnú pre reálne programy. V druhej iterácii už triedy vyzerajú trochu rozumnejšie.

Problémom nie je obecne inicializácia atribútov. Tá sa určite v niektorých prípadoch dá rozumne použiť. 

### Chybné riešenie

Problémom je, tento vzor, ktorý som videl celkom často:

{% highlight java %}
public class Triangle {
    private Vertex2D a = new Vertex2D();
    ...
}
{% endhighlight %}

Teda incializované atribúty reprezentujúce vrcholy. 
Použité v `Demo` nasledovne:

{% highlight java %}
public class Demo {
    public static void main(String[] args) {
        Triangle t = new Triangle();
        t.getVertexA().setX(...);
        ...
    }
}
{% endhighlight %}

Pričom Vertex2D atribúty inicializované nemá:

{% highlight java %}
public class Vertex2D {
    private double x, y;
    ...
}
{% endhighlight %}

### Kde je problém

Čerstvo skonštruovaný objekt typu `Triangle` má tak trochu nekonzistentnú formu. Vertexy má síce inicializované, ale samotné vertexy inicializované nie sú -- ich atribúty `x` a `y` sú `null`.

Taktiež definícia stavu objektu pristupovaním do väčších hĺbok objektového grafu (`t.getVertexA().setX(..)`) môže byť nebezpečná. To preto, že v tom prípade volajúca metóda spolieha na stav, ktorý si sama nedefinovala -- spolieha na to, že vertexy v `Triangle` sú po skonštruovaní inicializované. 

Vhodnejšie teda je spoliehať len na stav, ktorý volajúca metóda sama definuje. Teda napríklad
{% highlight java %}
Vertex2D vertA = new Vertex2D();
vertA.setX(1);
vertA.setY(2);
t.setVertexA(vertA);
{% endhighlight %}


Pri písaní triedy (deklarácii jej atribútov, metód) si treba predstavovať, že jej používateľ nebude vidieť jej zdrojáky, len jej javadoc, teda nebude poznať také detaily, ako stav atribútov po skonštruovaní objektu.

A z druhej strany tak isto -- pri písaní metódy a používaní iných tried si treba predstavovať, že nevidíme jej zdrojáky, len jej javadoc.

A keby som už v tom javadocu videl, že trieda má metódu `getVertexA()`, musím sa zamyslieť -- _vráti mi daná metóda v tomto čase nejakú rozumnú hodnotu?_.