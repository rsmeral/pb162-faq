---
layout: post
title: Ako vzniká inštancia
tags: [it02, java]
---

Narazil som v diskusnom fóre na zaujímavý problém: 

> cannot reference &lt;var&gt; before supertype constructor has been called

Nebudem sa zameriavať na to, za akých okolností môžeme toto varovanie uvidieť, ale skôr na jeho význam.
Ale predsa aspoň krátky príklad:

{% highlight java linenos %}
public class Guitar extends MusicalInstrument {

    public final int DEFAULT_NUM_OF_STRINGS = 6;

    private int numOfStrings;

    public Guitar(int numOfStrings) {
        this.numOfStrings = numOfStrings;
    }

    public Guitar() {
        this(DEFAULT_NUM_OF_STRINGS);
    }
    
}
{% endhighlight %}

Na riadku 12 sa stane zmienená chyba, kvôli zabudnutému modifikátoru `static` v deklarácii na riadku 3. Na to aby sme pochopili, prečo nemôžeme odkazovať na _instance variable_ predtým, než sa zavolá rodičovský konštruktor, musíme sa pozrieť na to, ako vzniká inštancia.

### Inicializácia inštancií

Presný popis vzniku inštancie triedy je v JLS, v kapitole [12.5. Creation of New Class Instances](http://docs.oracle.com/javase/specs/jls/se7/html/jls-12.html#jls-12.5).

Pokúsim sa o popis menej detailný, ale zrozumiteľnejší než ten v JLS.

Pri zavolaní konštruktora sa deje nasledovné:
 
1. **Skonštruuje sa hierarchia nadtried**
    
    V každom konštruktore je na začiatku implicitné (alebo explicitné) volanie konštruktora rodičovskej triedy (`super()`), **s jednou výnimkou** -- ak voláme iný konštruktor samotnej triedy pomocou `this()`. 

    Hneď v tomto bode môžme vidieť príčinu zmienenej chyby -- v momente, keď sa volá `this(DEFAULT_NUM_OF_STRINGS)`, v procese vzniku inštancie sme sa ešte nedostali ani k zavolaniu super-konštruktora a týmpádom ani k inicializácii, a premenná `DEFAULT_NUM_OF_STRINGS` teda nemôže byť referencovaná. 
    
2. **Vykoná sa inicializácia stavu (atribútov) objektu**

    Atribúty môžu byť inicializované dvoma spôsobami:
        
    1. v inicializátoroch spolu s deklaráciou atribútu -- tak ako na riadku 3 v predošlom príklade, alebo
    2. v inicializačných blokoch:
            
            {
                int count = 3 + 3;
                numOfStrings = count;
            }

    Táto fáza je zaujímavá tým, že v nej **záleží na poradí deklarácie**. Ak by sme deklarovali uvedený blok ešte pred deklaráciou atribútu `numOfStrings`, kód by sa neskompiloval, lebo by obsahoval neplatnú _forward reference_ -- odkaz na premennú, ktorá ešte nebola deklarovaná.

3. **Vykoná sa telo konštruktora**


To je veľmi zjednodušená verzia procesu inicializácie inštancie. Tento proces môže mať rôzne nečakané implikácie, napríklad keď v rodičovskom konštruktore voláme metódy, ktoré sú v potomkovi preťažené (JLS, 12.5-2.) :smiley: 
    
  


*[JLS]:     Java Language Specification