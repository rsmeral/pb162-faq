---
layout: post
title: Verzovanie projektu z príkazového riadku
tags: [cmdline, meta]
---

> Ako sa dostanem k predchádzajúcej verzii zadania??

**Najprv musím upozorniť, že tento postup nie je triviálny a môže potenciálne viesť k strate riešenia, takže je potrebné mať ho zálohované.**

Prvým problémom je, že BlueJ síce vie zobraziť históriu projektu, ale neumožňuje vrátiť sa k starším verziám. Na to je potrebné použiť externý nástroj. Druhým problémom je, že jednotlivé verzie SVN sú navzájom prudko nekompatibilné. BlueJ používa verziu 1.6, zatiaľčo aktuálna verzia dostupných SVN klientov je 1.8, a projekt "checkoutovaný" jednou verziou nie je interoperabilný s klientom verzie inej.

Takže je potrebné zaobstarať si nejakého starého SVN klienta, alebo -- _Java to the rescue!_ -- siahnuť po nástroji menom SVNKit, čo je SVN klient implementovaný čiste v Jave a dokonca ako jeden z mála umožňuje pracovať s repozitármi všetkych verzií. Takže, ukážem stručný postup, ktorý je platný pre linuxové systémy a veľmi podobný aj pre Windowsy, keďže, ako už vieme, Java beží všade, a teda aj SVNKit (a majiteľom Apple produktov sa ospravedlňujem :smirk:

## Postup

* stiahneme SVNKit z <http://www.svnkit.com/org.tmatesoft.svn_1.8.6.standalone.zip> do `$HOME`
* otvoríme terminál v adresári `$HOME`
* rozbalíme SVNKit, napr. pomocou 

      unzip -q org.tmatesoft.svn_1.8.6.standalone.zip

* nastavíme `PATH`, tak aby sme "videli" `jsvn` príkaz

      export PATH=$HOME/svnkit-1.8.6/bin:$PATH

* prejdeme do adresára s projektom

      cd pb162-2014

* funkčnosť si môžeme overiť napr. pomocou `jsvn info`, mali by sa nám zobraziť informácie o repozitári
môžeme si pozrieť zoznam revízií pomocou `jsvn log`
* konečne sa môžme pohybovať medzi revíziami projektu pomocou identifikátorov revízií. Ako vidno z logu, 1. iterácia je 71, druhá iterácia je 72.
* na stav zadania prvej iterácie by sme sa mali dostať pomocou 

      jsvn up -r71

​Rovnako sa potom dostaneme k akejkoľvek ďalšej revízii. Pohyb medzi revíziami by mal zachovať súbory vášho riešenia a manipulovať len súbormi zadania, ale na to sa nespoliehajte a zálohujte.

​Používatelia Windowsu trpiaci alergiou na príkazové riadky môžu siahnuť po grafických nástrojoch ako TortoiseSVN. :turtle: