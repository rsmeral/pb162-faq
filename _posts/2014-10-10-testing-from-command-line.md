--- 
layout: post
title: Testovanie z príkazového riadku
---

<span class="lead">JUnit testy je možné jednoducho spúšťať z príkazového riadku.</span>

Predpokladajme, že projekt máme v adresári `pb162-2014`.

Stiahneme si JUnit a jeho závislosť Hamcrest Core:

* [`junit.jar`](http://search.maven.org/remotecontent?filepath=junit/junit/4.11/junit-4.11.jar)
* [`hamcrest-core.jar`](http://search.maven.org/remotecontent?filepath=org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar)


Najprv skompilujeme zdrojáky, buď cez BlueJ, alebo zhruba takto:

    find pb162-2014 -name *.java | xargs javac -cp junit-4.11.jar:hamcrest-core-1.3.jar:pb162-2014

A potom už môžeme pustiť testy. V JUnit JARe sa nachádza trieda `org.junit.runner.JUnitCore`, ktorá spúšťa testy, a jej argumentom je FQCN testovacej triedy. Takže takto:
    
    java -cp junit-4.10.jar:hamcrest-core-1.3.jar:pb162-2014 org.junit.runner.JUnitCore cz.muni.fi.pb162.project.test.ProjectTest

Výstupom by v ideálnom prípade malo byť
    
    OK (3 tests)

Well done!! :hatched_chick: :boom: :clap: :thumbsup: 

*[FQCN]:        Fully Qualified Class Name
