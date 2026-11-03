**Kategorie:** Verhaltensmuster (Behavioral Pattern)

## Was ist das Template Method Pattern?

Das Template Method Pattern definiert das Grundgerüst eines Algorithmus in einer Methode.

Einzelne Schritte werden an Unterklassen delegiert. Diese können bestimmte Schritte unterschiedlich implementieren, ohne die Reihenfolge des gesamten Algorithmus zu verändern.

## Welches Problem löst es?

Kaffee und Tee werden auf ähnliche Weise zubereitet:

1. Wasser kochen.
2. Kaffee aufbrühen oder Tee ziehen lassen.
3. Getränk in eine Tasse gießen.
4. Zusätze hinzufügen.

Die allgemeinen Schritte sind gleich, aber manche Schritte unterscheiden sich.

Anstatt den gesamten Ablauf mehrfach zu implementieren, wird das gemeinsame Grundgerüst in einer Oberklasse definiert.

## Aufbau

- **Abstract Class:** Enthält das Grundgerüst des Algorithmus.
- **Template Method:** Definiert die Reihenfolge der Schritte.
- **Primitive Operations:** Einzelne Schritte, die Unterklassen implementieren oder überschreiben.
- **Concrete Classes:** Stellen die konkreten Varianten bereit.

## Beispiel in Java

```java
abstract class Getraenk {
    public final void zubereiten() {
        wasserKochen();
        zubereitenInWasser();
        tasseFuellen();
        zusatzHinzufuegen();
    }

    private void wasserKochen() {
        System.out.println("Wasser kochen");
    }

    protected abstract void zubereitenInWasser();

    private void tasseFuellen() {
        System.out.println("In die Tasse füllen");
    }

    protected abstract void zusatzHinzufuegen();
}

class Kaffee extends Getraenk {
    protected void zubereitenInWasser() {
        System.out.println("Kaffee aufbrühen");
    }

    protected void zusatzHinzufuegen() {
        System.out.println("Milch und Zucker hinzufügen");
    }
}

class Tee extends Getraenk {
    protected void zubereitenInWasser() {
        System.out.println("Tee ziehen lassen");
    }

    protected void zusatzHinzufuegen() {
        System.out.println("Zitrone hinzufügen");
    }
}
```

Verwendung:

```java
Getraenk kaffee = new Kaffee();
kaffee.zubereiten();

Getraenk tee = new Tee();
tee.zubereiten();
```

Die Reihenfolge bleibt gleich. Nur die konkreten Schritte unterscheiden sich.

## Vorteile

- Gemeinsamer Code wird wiederverwendet.
- Doppelte Implementierungen werden vermieden.
- Die Reihenfolge des Algorithmus bleibt zentral festgelegt.
- Unterklassen können einzelne Schritte unterschiedlich gestalten.

## Nachteile

- Es entsteht eine Abhängigkeit von der Vererbungshierarchie.
- Unterklassen können bei zu vielen überschreibbaren Methoden schwer überschaubar werden.
- Der Algorithmus lässt sich nicht so flexibel durch unabhängige Strategieobjekte austauschen wie beim Strategy Pattern.

## Eselsbrücke

**Template = Vorlage.**

Wie ein Kochrezept: Die Reihenfolge der Arbeitsschritte bleibt gleich, aber einzelne Zutaten oder Zubereitungsschritte unterscheiden sich.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Template Method Patterns?**

Antwort: Das Grundgerüst eines Algorithmus in einer Methode festzulegen und einzelne Schritte von Unterklassen implementieren zu lassen.

**Frage 2: Was ist die Template Method?**

Antwort: Die Methode, welche die Reihenfolge der einzelnen Schritte des Algorithmus definiert.

**Frage 3: Welche Aufgabe hat die abstrakte Klasse?**

Antwort: Sie enthält den gemeinsamen Ablauf und definiert, welche Schritte von Unterklassen umgesetzt werden müssen.

**Frage 4: Was dürfen Unterklassen verändern?**

Antwort: Sie können die vorgesehenen Schritte unterschiedlich implementieren, ohne das Grundgerüst des Algorithmus verändern zu müssen.

**Frage 5: Warum verwendet man dieses Pattern?**

Antwort: Um gemeinsamen Code wiederzuverwenden und doppelte Implementierungen ähnlicher Algorithmen zu vermeiden.

**Frage 6: Was bedeutet `final` bei der Template Method in Java?**

Antwort: Eine mit `final` deklarierte Methode kann von Unterklassen nicht überschrieben werden. Dadurch bleibt der definierte Ablauf geschützt.

**Frage 7: Was ist der Unterschied zwischen Template Method und Strategy?**

Antwort: Template Method legt den Algorithmus mithilfe von Vererbung und einem festen Grundgerüst fest. Strategy kapselt unterschiedliche Algorithmen in separaten Objekten, die ausgetauscht werden können.

**Merksatz:** Template Method legt den Ablauf fest und lässt einzelne Schritte variieren.
