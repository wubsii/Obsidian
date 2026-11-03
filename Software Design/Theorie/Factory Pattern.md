**Kategorie:** Erzeugungsmuster (Creational Pattern)

## Was ist das Factory Pattern?

Das Factory Pattern kapselt die Erzeugung von Objekten, sodass der aufrufende Code nicht selbst alle konkreten Klassen kennen oder direkt instanziieren muss.

Bei der Factory Method wird eine Schnittstelle zur Objekterzeugung definiert. Unterklassen entscheiden, welche konkrete Klasse erzeugt wird.

## Welches Problem löst es?

Ein Programm soll unterschiedliche Fahrzeugtypen herstellen können, beispielsweise:

- PKW
- LKW
- Sportwagen

Ohne Factory müsste der aufrufende Code selbst entscheiden, welche konkrete Klasse mit `new` erzeugt wird.

Dadurch würde er direkt von den konkreten Klassen abhängen.

Eine Factory kapselt diese Entscheidung.

## Aufbau bei der Factory Method

- **Product:** Gemeinsames Interface der erzeugten Objekte.
- **Concrete Product:** Konkrete Implementierung des Products.
- **Creator:** Definiert die Factory Method.
- **Concrete Creator:** Entscheidet, welches konkrete Product erzeugt wird.

## Beispiel in Java

```java
interface Fahrzeug {
    void hupen();
}

class PKW implements Fahrzeug {
    public void hupen() {
        System.out.println("PKW hupt");
    }
}

class LKW implements Fahrzeug {
    public void hupen() {
        System.out.println("LKW hupt");
    }
}

abstract class FahrzeugFabrik {
    public abstract Fahrzeug erstelleFahrzeug();
}

class PKWFabrik extends FahrzeugFabrik {
    public Fahrzeug erstelleFahrzeug() {
        return new PKW();
    }
}

class LKWFabrik extends FahrzeugFabrik {
    public Fahrzeug erstelleFahrzeug() {
        return new LKW();
    }
}
```

Verwendung:

```java
FahrzeugFabrik fabrik = new PKWFabrik();

Fahrzeug fahrzeug = fabrik.erstelleFahrzeug();
fahrzeug.hupen();
```

Der aufrufende Code verwendet das Interface `Fahrzeug` und muss die Erzeugung nicht selbst durchführen.

## Vorteile

- Die Objekterzeugung wird zentralisiert.
- Der aufrufende Code ist weniger von konkreten Klassen abhängig.
- Neue Produktvarianten können leichter ergänzt werden.
- Die Erzeugungslogik ist besser getrennt.

## Nachteile

- Es entstehen zusätzliche Klassen.
- Bei vielen Produktvarianten kann die Struktur umfangreich werden.

## Eselsbrücke

**Factory = Fabrik.**

Du bestellst ein Fahrzeug, und die Fabrik entscheidet, welches konkrete Fahrzeug erzeugt wird.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Factory Patterns?**

Antwort: Die Erzeugung von Objekten zu kapseln und vom aufrufenden Code zu trennen.

**Frage 2: Warum verwendet man eine Factory?**

Antwort: Damit der aufrufende Code nicht selbst alle konkreten Klassen erzeugen und kennen muss.

**Frage 3: Was ist ein Product?**

Antwort: Ein Product ist das gemeinsame Interface oder die gemeinsame abstrakte Klasse der erzeugten Objekte.

**Frage 4: Was ist eine Factory Method?**

Antwort: Eine Methode, die ein Objekt erzeugt und bei der Unterklassen bestimmen können, welche konkrete Produktklasse erstellt wird.

**Frage 5: Was ist der Unterschied zwischen Factory und Singleton?**

Antwort: Factory kapselt die Erzeugung von Objekten. Singleton stellt sicher, dass nur eine Instanz einer bestimmten Klasse existiert.

**Frage 6: Wie passt Factory zum Dependency Inversion Principle?**

Antwort: Der aufrufende Code kann gegen ein gemeinsames Interface programmieren, statt direkt von konkreten Produktklassen abhängig zu sein.

**Frage 7: Nenne ein Anwendungsbeispiel.**

Antwort: Eine Fahrzeugfabrik erzeugt je nach Bedarf einen PKW, LKW oder Sportwagen.

**Merksatz:** Factory kapselt die Entscheidung, welches Objekt erzeugt wird.