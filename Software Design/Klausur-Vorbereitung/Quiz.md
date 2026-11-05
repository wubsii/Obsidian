  
## Pattern erkennen

  

```quiz

Ein Getränkeautomat soll Kaffee mit beliebig vielen kombinierbaren Zusätzen (Milch, Sirup, Schaum) verkaufen, wobei sich die Kosten addieren. Welches Pattern löst das am besten?

[c] Decorator
[ ] Strategy
[w] Strategy
[ ] Template Method

[w] Template Method

[ ] Factory Method

  

Der **Decorator** umhüllt ein Objekt mit demselben Supertyp, delegiert an das umhüllte Objekt und addiert den eigenen Anteil. Dadurch sind beliebige Kombinationen stapelbar.

  

Strategy würde das gesamte Verhalten ersetzen statt es zu ergänzen. Template Method arbeitet mit Vererbung und würde zu einer Klassenexplosion führen. Factory Method regelt nur die Objekterzeugung.

```

  

```quiz

Ein Manager soll seine Provisionsberechnung zur Laufzeit zwischen „10 % vom Gewinn“ und „5 % vom Umsatz“ wechseln können. Welche Lösung passt am besten?

[c] Ein Strategy-Objekt als Attribut des Managers, per Setter austauschbar

[ ] Je eine Manager-Subklasse pro Berechnungsart, fest beim Erzeugen

[ ] Ein Decorator, der mehrere Provisionen aufeinander stapelt

[w] Ein Decorator, der mehrere Provisionen aufeinander stapelt

  

**Strategy** kapselt die austauschbare Berechnung hinter einem Interface. Der Manager *hat* eine Strategie (has-a) und kann sie zur Laufzeit wechseln.

  

Subklassen und Template Method legen das Verhalten zur Übersetzungszeit fest. Ein Decorator *ergänzt* Verhalten, er ersetzt es nicht.

```

  

```quiz

Ein Verlag informiert alle Abonnenten automatisch, sobald eine neue Ausgabe erscheint. Welches Pattern und welche Rolle hat der Verlag?

[ ] Command, der Verlag ist der Invoker

[ ] Observer, der Verlag ist der Observer

[ ] Command, der Verlag ist der Receiver

[c] Observer, der Verlag ist das Subject

[r] Observer, der Verlag ist das Subject

Beim **Observer** ist der Verlag das **Subject** (Publisher). Die Abonnenten sind die Observer, die sich registrieren und bei Änderungen benachrichtigt werden.

  

Command würde eine einzelne Aktion als Objekt verpacken, nicht viele Empfänger über eine Änderung informieren.

```

  

```quiz

Zwei Klassen Kaffee und Tee haben fast dieselbe Zubereitung. Der Ablauf soll in einer Oberklasse fest vorgegeben sein, nur einzelne Schritte unterscheiden sich. Welches Pattern passt?

[ ] Strategy

[c] Template Method

[ ] Decorator

[ ] Adapter

[w] Adapter

Die **Template Method** legt das Skelett des Algorithmus in einer (meist `final`) Methode der Oberklasse fest. Subklassen füllen nur einzelne Schritte aus.

  

Strategy wäre die Alternative mit Komposition, wenn der gesamte Algorithmus austauschbar sein soll. Hier steht aber der *Ablauf* fest, und die Unterschiede liegen in einzelnen Schritten.

```

  

```quiz

Eine Klasse `Turkey` hat `gobble()`, der Client erwartet aber ein `Duck`-Interface mit `quack()`. Welches Pattern löst das Problem?

[ ] Decorator

[ ] Facade

[c] Adapter

[ ] Strategy

  

Der **Adapter** wandelt ein vorhandenes Interface in das vom Client erwartete um. Der `TurkeyAdapter` implementiert `Duck` und ruft intern `gobble()` auf.

  

Der Decorator würde das Interface unverändert lassen und nur Verhalten hinzufügen. Eine Facade vereinfacht viele Klassen, sie wandelt kein einzelnes Interface um.

```

  

## Prinzipien

  

```quiz

Warum ist es ein Problem, `fly()` in der Oberklasse `Ente` zu definieren, wenn es auch Gummienten gibt?

[ ] Weil Oberklassen keine Methoden mit Implementierung haben dürfen

[ ] Weil Gummienten dann kein `quack()` erben können

[c] Weil auch Gummienten automatisch fliegen würden

[ ] Weil `fly()` dann nicht mehr überschrieben werden kann

  

Alle Subklassen erben `fly()`, daher fliegen auch Gummienten. Das ist das Ausgangsproblem der Folien. Die Lösung ist, das veränderliche Verhalten in ein eigenes Interface auszulagern (**Strategy**).

```

  

```quiz

Welcher Punkt ist KEIN Nachteil davon, `fly()` in jeder Enten-Subklasse einzeln zu überschreiben?

[ ] Gleicher Code steht in mehreren Subklassen

[ ] Das Verhalten lässt sich zur Laufzeit nicht ändern

[ ] Eine Änderung kann unbeabsichtigt andere Enten treffen

[c] Java erlaubt kein Überschreiben von Oberklassenmethoden

  

Java erlaubt das Überschreiben von Methoden problemlos, das ist also kein Nachteil, sondern eine falsche Aussage. Die anderen drei Punkte sind echte Probleme der Vererbungslösung: duplizierter Code, keine Laufzeitänderung, unerwartete Seiteneffekte.

```

  

```quiz

Ein neues Zusatzprodukt „Soja“ soll hinzugefügt werden, ohne eine bestehende Klasse zu verändern. Welches Prinzip wird dadurch erfüllt?

[c] Open-Closed-Prinzip

[ ] Dependency Inversion

[ ] Kohärenz

[ ] Komposition vor Vererbung

  

Das **Open-Closed-Prinzip** verlangt: offen für Erweiterung, geschlossen für Veränderung. Beim Decorator kommt eine neue Klasse hinzu, ohne dass bestehende Klassen angefasst werden.

  

Komposition vor Vererbung ist das *Mittel*, mit dem der Decorator das erreicht. Gefragt war aber nach dem Prinzip, das hier erfüllt wird.

```

  

```quiz

`PizzaStore.orderPizza()` arbeitet nur mit dem Typ `Pizza`, nie mit konkreten Klassen wie `NYStyleCheesePizza`. Welches Prinzip steckt dahinter?

[ ] Kohärenz

[ ] Komposition vor Vererbung

[c] Dependency Inversion

[ ] Kapsle, was sich ändert

  

**Dependency Inversion**: Hochrangige Klassen hängen von Abstraktionen ab, nicht von konkreten Klassen. Die Factory Method sorgt dafür, dass die Erzeugung der konkreten Pizza in den Subklassen liegt.

```

  

```quiz

Welche Deklaration folgt dem Prinzip „gegen ein Interface programmieren“ am besten?

[ ] `FliegtMitFluegeln fv = new FliegtMitFluegeln();`

[ ] `Object fv = new FliegtMitFluegeln();`

[c] `Flugverhalten fv = new FliegtMitFluegeln();`

[ ] `FliegtMitFluegeln fv = new Flugverhalten();`

  

Der deklarierte Typ ist das Interface `Flugverhalten`, die konkrete Klasse kommt nur rechts bei `new` vor.

  

`Object` ist zwar abstrakt, bietet aber keine Methode `fliegen()`. Die letzte Variante kompiliert gar nicht, weil man ein Interface nicht instanziieren kann.

```

  

```quiz

Welche Aussage über die Kopplung beim Observer Pattern stimmt?

[ ] Das Subject muss alle konkreten Observer-Klassen importieren

[c] Das Subject kennt nur das Observer-Interface

[ ] Neue Observer erfordern eine Änderung am Subject

[ ] Observer müssen im Konstruktor des Subjects erzeugt werden

  

Das Subject kennt nur das Interface. Dadurch lassen sich neue Observer zur Laufzeit hinzufügen, ohne das Subject zu ändern: **lose Kopplung**.

```

  

## Singleton und Factory

  

```quiz

Was verhindert in erster Linie, dass andere Klassen eine zweite Singleton-Instanz erzeugen?

[ ] Ein statisches Attribut `instance`

[ ] Eine `synchronized` Methode `getInstance()`

[ ] Die Deklaration der Klasse als `final`

[c] Ein privater Konstruktor

  

Mit einem **privaten Konstruktor** kann nur die Klasse selbst `new` aufrufen. Das statische Feld speichert die Instanz, verhindert aber keine weiteren `new`-Aufrufe. `synchronized` betrifft nur Thread-Sicherheit, `final` nur die Vererbung.

```

  

```quiz

Was kann passieren, wenn `getInstance()` ohne `synchronized` implementiert ist und mehrere Threads gleichzeitig zugreifen?

[ ] Die Instanz wird nie erzeugt

[ ] Es tritt ein Compilerfehler auf

[c] Zwei Threads sehen `null` und erzeugen zwei Instanzen

[ ] Die Instanz wird bei jedem Aufruf neu erzeugt

  

Beide Threads können `instance == null` gleichzeitig prüfen und dann jeweils `new` aufrufen. Dadurch ist das Singleton verletzt. `synchronized` verhindert das.

```

  

```quiz

Welche Beschreibung trifft auf das Factory Method Pattern zu, aber NICHT auf eine Simple Factory?

[ ] Eine Klasse erzeugt Produkte über eine if/else-Kette

[ ] Es existiert genau eine Instanz der Fabrik

[ ] Der Client ruft `new` direkt auf

[c] Subklassen entscheiden per abstrakter Methode, was erzeugt wird

  

Bei der **Factory Method** ist die Erzeugungsmethode abstrakt im Creator deklariert, und jede Subklasse entscheidet, welches Produkt sie erzeugt. Die Simple Factory (if/else) ist laut Folien noch nicht die richtige Lösung, weil sie nicht über Vererbung erweiterbar ist.

```

  

```quiz

In der Nokia-Angabe ist `getProduct` in `NokiaFactory` konkret, `createProduct` aber abstrakt. Warum?

[ ] Damit Subklassen `getProduct` überschreiben müssen

[ ] Weil abstrakte Methoden keinen Rückgabewert haben dürfen

[c] Damit der Ablauf mit Seriennummer für alle Fabriken gleich bleibt

[ ] Weil Java nur eine abstrakte Methode pro Klasse erlaubt

  

`getProduct` gibt den firmenweiten Ablauf vor (jedes Produkt bekommt eine Seriennummer). Nur die Erzeugung (`createProduct`) variiert und wird an die Subklassen delegiert. Das gleicht dem Aufbau von `orderPizza` und `createPizza`.

```

  

```quiz

`BootFactory.getProduct(ProductType.BASESTATION_4G)` wird aufgerufen. Was soll laut Angabe passieren?

[ ] Es wird eine `BaseStation4G` zurückgegeben

[r] Es wird `null` zurückgegeben

[ ] Es wird eine `Boots`-Instanz zurückgegeben

[ ] Es wird eine Exception geworfen

  

Laut Angabe liefert die BootFactory für alles außer Boots `null`. Deshalb sollte `getProduct` auch nur dann eine Seriennummer vergeben, wenn ein Produkt tatsächlich erzeugt wurde.

```

  

## Observer im Praxisteil

  

```quiz

Ein Client ruft `endGame()` auf. Was muss laut Angabe dabei passieren?

[ ] Nur die Referenz auf den Server wird auf `null` gesetzt

[ ] Nur die Abmeldung beim Server erfolgt

[c] Abmeldung beim Server und danach Referenz auf `null` setzen

[ ] Der Server wird beendet und alle anderen Clients abgemeldet

  

Wird nur die Referenz auf `null` gesetzt, bleibt der Client weiter in der Liste des Servers und bekommt weitere Updates. Man muss sich zuerst abmelden (`unregister`) und erst danach die Referenz löschen, sonst gibt es keine Referenz mehr, über die man sich abmelden könnte.

```

  

```quiz

Warum iteriert man in `notifyClients()` besser über eine Kopie der Client-Liste?

[ ] Weil `ArrayList` nicht in einer for-each-Schleife verwendet werden darf

[c] Weil sich ein Client während `update()` abmelden könnte und sonst eine Exception droht

[ ] Weil `update()` sonst doppelt aufgerufen wird

[ ] Weil das Observer Pattern Kopien vorschreibt

  

Meldet sich ein Client während der Schleife ab (z. B. weil `update()` ein Spielende auslöst), wird die Liste verändert und es gibt eine `ConcurrentModificationException`. Die Kopie vermeidet das.

```

  

```quiz

Ein `AppClient` soll ein Event nur behandeln, wenn „zumindest 20 % Akku“ vorhanden sind. Welche Bedingung ist korrekt?

[ ] `akku > 20`

[ ] `akku <= 20`

[c] `akku >= 20`

[ ] `akku != 20`

  

„Zumindest 20 %“ heißt: 20 % oder mehr, also `>= 20`. Genau 20 % muss noch erlaubt sein. Gleiches gilt für „mindestens 1000“ bei der Version.

```

  

```quiz

Der `ConsoleClient` soll nur reagieren, wenn der Systemname ungleich „Nintendo“ ist. Welcher Ausdruck ist korrekt und sicher?

[ ] `systemName != "Nintendo"`

[ ] `systemName.equals("Nintendo")`

[ ] `systemName.compareTo("Nintendo") == 0`

[c] `!"Nintendo".equals(systemName)`

  

Strings vergleicht man in Java mit `equals()`, nicht mit `==`/`!=` (das vergleicht Referenzen). `"Nintendo".equals(systemName)` ist zusätzlich `null`-sicher. Die zweite und dritte Variante prüfen auf *Gleichheit*, gefragt war aber Ungleichheit.

```

  

## Command, Facade, Iterator, Template

  

```quiz

Eine Fernbedienung führt Befehle auf einem Fernseher aus. Welche Rolle im Command Pattern hat der Fernseher?

[ ] Invoker

[ ] Client

[c] Receiver

[ ] Command

  

Der **Receiver** führt die eigentliche Arbeit aus (`channelUp()`). Die Fernbedienung ist der **Invoker**, der nur `execute()` aufruft. Das Command-Objekt verbindet beide, und der Client erzeugt es.

```

  

```quiz

Warum unterstützt das Command Pattern Undo besonders gut?

[ ] Weil der Invoker den Receiver direkt kennt

[ ] Weil `execute()` Änderungen automatisch rückgängig macht

[c] Weil jeder Befehl ein Objekt ist und in einer Historie gespeichert werden kann

[ ] Weil jedes Command zwei Receiver besitzt

  

Da jede Aktion ein eigenes Objekt ist, kann man ausgeführte Commands in einem Stack speichern und später `undo()` aufrufen. Das Rückgängigmachen muss aber in jedem Command selbst implementiert werden, es passiert nicht automatisch.

```

  

```quiz

Was unterscheidet eine Facade grundsätzlich von einem Adapter?

[ ] Eine Facade erbt immer von den Klassen des Subsystems

[c] Eine Facade vereinfacht viele Klassen, ein Adapter passt ein Interface an

[ ] Eine Facade verändert nie den Aufruf an das Subsystem

[ ] Ein Adapter kann nur zur Laufzeit eingesetzt werden

  

Die **Facade** bietet ein einfaches, übergeordnetes Interface vor einem komplexen Subsystem (z. B. `startMovie()`). Der **Adapter** wandelt ein bestehendes Interface in das vom Client erwartete um.

```

  

```quiz

Warum ist `prepareRecipe()` in der Template-Method-Oberklasse als `final` deklariert?

[ ] Damit die Methode schneller ausgeführt wird

[ ] Damit sie nur einmal pro Objekt aufgerufen werden kann

[c] Damit Subklassen den Ablauf nicht ändern, sondern nur einzelne Schritte

[ ] Weil abstrakte Klassen nur finale Methoden haben dürfen

  

`final` verhindert, dass Subklassen die Reihenfolge der Schritte verändern. Sie überschreiben nur die abstrakten Schritte (`brew()`, `addCondiments()`).

```

  

```quiz

Was braucht eine eigene Klasse `Menu`, damit man sie in einer for-each-Schleife verwenden kann?

[ ] Sie muss von `ArrayList` erben

[ ] Sie muss selbst `hasNext()` und `next()` anbieten

[c] Sie muss `Iterable` implementieren und einen Iterator liefern

[ ] Sie muss `Comparable` implementieren

  

for-each verlangt `Iterable` mit der Methode `iterator()`. Der gelieferte `Iterator` bietet `hasNext()` und `next()`. Diese beiden Methoden allein in `Menu` reichen für for-each nicht aus.

```

  

## Rechnen, Java, UML

  

```quiz

`Espresso` kostet 1,99 €, `Milch` als Decorator 0,30 €. Was kostet `new Milch(new Milch(new Espresso()))`?

[ ] 1,99 €

[ ] 2,29 €

[c] 2,59 €

[ ] 0,60 €

  

Jede Milch delegiert an das umhüllte Objekt und addiert 0,30 €: 1,99 + 0,30 + 0,30 = **2,59 €**. 2,29 € wäre nur eine Milch.

```

  

```quiz

Welches Java-Beispiel ist ein typischer Decorator?

[ ] `List.of(1, 2, 3)`

[ ] `Collections.sort(liste)`

[c] `new BufferedReader(new FileReader(datei))`

[ ] `Math.max(a, b)`

  

Der `BufferedReader` umhüllt einen anderen `Reader` (gleicher Supertyp) und ergänzt Pufferung. Das ist das klassische Decorator-Beispiel aus `java.io`.

```

  

```quiz

Welche UML-Beziehung beschreibt: „Ein Teil gehört höchstens einem Ganzen und hat dieselbe Lebensdauer“?

[ ] Aggregation mit hohler Raute

[ ] Vererbung mit hohlem Dreieck

[ ] Assoziation mit Pfeil

[c] Komposition mit gefüllter Raute

  

**Komposition** ist die strengere Form der Teil-Ganzes-Beziehung (gefüllte Raute): Teil gehört höchstens einem Ganzen, gemeinsame Lebensdauer. Die Aggregation (hohle Raute) ist lockerer.

```

  

```quiz

Wie wird in UML die Implementierung eines Interfaces durch eine Klasse dargestellt?

[ ] Durchgezogene Linie mit hohlem Dreieck

[c] Strichlierte Linie mit hohlem Dreieck

[ ] Durchgezogene Linie mit gefüllter Raute

[ ] Strichlierte Linie mit hohler Raute

  

Interface-Implementierung = **strichlierte** Linie mit hohlem Dreieck. Vererbung (is-a) ist dieselbe Spitze, aber mit durchgezogener Linie.

```

  

```quiz

Welche Zuordnung zu den drei Musterkategorien ist korrekt?

[ ] Decorator gehört zu den Verhaltensmustern

[ ] Observer gehört zu den Strukturmustern

[ ] Facade gehört zu den Erzeugungsmustern

[c] Singleton gehört zu den Erzeugungsmustern

  

Erzeugung: Singleton, Factory. Struktur: Decorator, Adapter, Facade. Verhalten: Strategy, Observer, Command, Template Method, Iterator.

```