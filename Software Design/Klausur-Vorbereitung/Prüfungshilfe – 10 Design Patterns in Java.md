# Allgemeine Vorgehensweise bei einer Prüfungsaufgabe

1. **Aufgabenstellung markieren:** Was soll erreicht werden?
2. **Schlüsselwörter suchen:** austauschbar, erweitern, benachrichtigen, erzeugen, übersetzen usw.
3. **Klassen bestimmen:** Welche Objekte und Interfaces werden benötigt?
4. **Verbindungen zeichnen:** Wer implementiert welches Interface? Wer erbt von wem? Wer speichert oder verwendet wen?
5. **Warum erklären:** Welches Problem löst jede Verbindung?
6. **Methoden festlegen:** Welche Methoden gehören ins Interface, in die Oberklasse oder in die konkreten Klassen?
7. **Implementieren:** Erst die Interfaces und Oberklassen, danach die konkreten Klassen und zuletzt den Testcode.

## Wie erkenne ich das richtige Design Pattern?

Achte in der Aufgabenstellung auf diese Hinweise:

| Hinweis in der Aufgabe                                         | Design Pattern                                                       |
| -------------------------------------------------------------- | -------------------------------------------------------------------- |
| Verhalten soll austauschbar sein                               | [[#1. Strategy Pattern – Strategie\|Strategy]]                       |
| Ein Objekt soll zusätzliche Funktionen erhalten                | [[#2. Decorator Pattern – Dekorierer\|Decorator]]                    |
| Mehrere Objekte sollen über Änderungen informiert werden       | [[#3. Observer Pattern – Beobachter\|Observer]]                      |
| Es soll nur eine einzige Instanz geben                         | [[#4. Singleton Pattern – Einzelstück\|Singleton]]                   |
| Objekte sollen über eine Methode erzeugt werden                | [[#5. Factory Method Pattern – Fabrikmethode\|Factory Method]]       |
| Befehle sollen als Objekte gespeichert oder ausgeführt werden  | [[#6. Command Pattern – Befehl\|Command]]                            |
| Zwei inkompatible Schnittstellen sollen zusammenarbeiten       | [[#7. Adapter Pattern – Adapter\|Adapter]]                           |
| Ein kompliziertes System soll einfacher bedienbar sein         | [[#8. Facade Pattern – Fassade\|Facade]]                             |
| Der Ablauf bleibt gleich, einzelne Schritte unterscheiden sich | [[#9. Template Method Pattern – Schablonenmethode\|Template Method]] |
| Eine Sammlung soll einheitlich durchlaufen werden              | [[#10. Iterator Pattern – Iterator\|Iterator]]                       |

---

# 1. Strategy Pattern – Strategie

## Erkennungsmerkmale
- Verschiedene Möglichkeiten, dieselbe Aufgabe auszuführen.
- Das Verhalten soll zur Laufzeit austauschbar sein.
- Eine Klasse soll nicht selbst alle Varianten mit `if` oder `switch` unterscheiden müssen.

**Beispiel:** Ein Zahlungsprogramm unterstützt Kreditkarte, PayPal und Überweisung.

## Klassen und Verbindungen

- **Context:** Verwendet eine Strategie.
- **Strategy:** Interface mit einer gemeinsamen Methode.
- **ConcreteStrategyA / ConcreteStrategyB:** Implementieren das Strategy-Interface.

**Verbindung:**

`Context → Strategy ← ConcreteStrategyA / ConcreteStrategyB`

**Warum?**

Der Context kennt nur das Interface und nicht die konkrete Strategie. Deshalb kann eine Strategie ausgetauscht werden, ohne den Context umzuschreiben.

## Typische Methoden
- `ausfuehren()`
- `setStrategie()`

## Java-Grundaufbau

```java
interface Strategie {
    void ausfuehren();
}

class StrategieA implements Strategie {
    public void ausfuehren() {
        System.out.println("Strategie A");
    }
}

class Kontext {
    private Strategie strategie;

    public void setStrategie(Strategie strategie) {
        this.strategie = strategie;
    }

    public void starten() {
        strategie.ausfuehren();
    }
}
```

## Vorgehen in der Prüfung
1. Gemeinsames Interface erstellen.
2. Jede Variante implementiert das Interface.
3. Context speichert eine Variable vom Interface-Typ.
4. Context ruft die Methode der gewählten Strategie auf.

**Merksatz:** Ein Interface, mehrere austauschbare Verhaltensweisen.

---

# 2. Decorator Pattern – Dekorierer

## Erkennungsmerkmale
- Ein Objekt soll zusätzliche Funktionen erhalten.
- Die ursprüngliche Klasse soll nicht verändert werden.
- Funktionen sollen flexibel kombiniert werden können.

**Beispiel:** Ein Kaffee kann mit Milch, Zucker oder Sahne erweitert werden.

## Klassen und Verbindungen

- **Component:** Gemeinsames Interface.
- **ConcreteComponent:** Das ursprüngliche Objekt.
- **Decorator:** Implementiert Component und speichert ein Component-Objekt.
- **ConcreteDecorator:** Fügt eine konkrete Erweiterung hinzu.

**Verbindung:**

`ConcreteComponent → Component ← Decorator ← ConcreteDecorator`

Zusätzlich enthält der Decorator ein Objekt vom Typ `Component`.

**Warum?**

Der Decorator hat denselben Typ wie das ursprüngliche Objekt. Deshalb kann er dieses ersetzen und dessen Verhalten erweitern. Mehrere Decorators können ineinander verschachtelt werden.

## Typische Methoden
- `kosten()`
- `beschreibung()`

## Java-Grundaufbau

```java
interface Component {
    void ausfuehren();
}

class Grundobjekt implements Component {
    public void ausfuehren() {
        System.out.println("Grundfunktion");
    }
}

class Decorator implements Component {
    protected Component objekt;

    public Decorator(Component objekt) {
        this.objekt = objekt;
    }

    public void ausfuehren() {
        objekt.ausfuehren();
    }
}

class Erweiterung extends Decorator {
    public Erweiterung(Component objekt) {
        super(objekt);
    }

    public void ausfuehren() {
        super.ausfuehren();
        System.out.println("Zusätzliche Funktion");
    }
}
```

## Vorgehen in der Prüfung
1. Gemeinsames Component-Interface erstellen.
2. Grundobjekt implementiert das Interface.
3. Decorator implementiert ebenfalls das Interface.
4. Decorator speichert ein Component-Objekt.
5. Konkreter Decorator ergänzt das Verhalten.

**Merksatz:** Ein Objekt wird eingepackt und dadurch erweitert.

---

# 3. Observer Pattern – Beobachter

## Erkennungsmerkmale
- Mehrere Objekte sollen über Änderungen informiert werden.
- Beobachter können sich registrieren und abmelden.
- Ein Objekt löst Benachrichtigungen aus.

**Beispiel:** Mehrere Personen erhalten eine Nachricht, wenn ein neuer Beitrag veröffentlicht wird.

## Klassen und Verbindungen

- **Subject:** Verwaltet die registrierten Observer.
- **Observer:** Interface mit einer Aktualisierungsmethode.
- **ConcreteObserver:** Implementiert Observer.

**Verbindung:**

`Subject → Observer ← ConcreteObserver`

Ein Subject kann mehrere Observer verwalten.

**Warum?**

Das Subject muss nicht wissen, welche konkreten Klassen benachrichtigt werden. Es kennt nur das Observer-Interface und kann dadurch beliebig viele passende Beobachter informieren.

## Typische Methoden
- `registrieren()`
- `abmelden()`
- `benachrichtigen()`
- `aktualisieren()`

## Java-Grundaufbau

```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void aktualisieren();
}

class Beobachter implements Observer {
    public void aktualisieren() {
        System.out.println("Änderung erhalten");
    }
}

class Subject {
    private List<Observer> beobachter = new ArrayList<>();

    public void registrieren(Observer o) {
        beobachter.add(o);
    }

    public void abmelden(Observer o) {
        beobachter.remove(o);
    }

    public void benachrichtigen() {
        for (Observer o : beobachter) {
            o.aktualisieren();
        }
    }
}
```

## Vorgehen in der Prüfung
1. Observer-Interface erstellen.
2. Konkrete Beobachter implementieren das Interface.
3. Subject verwaltet eine Liste von Observern.
4. Bei einer Änderung ruft das Subject die Aktualisierungsmethode aller Observer auf.

**Merksatz:** Ein Subject informiert alle registrierten Beobachter.

---

# 4. Singleton Pattern – Einzelstück

## Erkennungsmerkmale
- Von einer Klasse darf es nur ein Objekt geben.
- Alle verwendenden Klassen sollen dieselbe Instanz erhalten.
- Die Instanz wird zentral bereitgestellt.

**Beispiel:** Eine zentrale Konfiguration oder ein gemeinsamer Programmmanager.

## Klassen und Verbindungen

- **Singleton:** Verwaltet seine einzige Instanz selbst.
- **Andere Klassen:** Greifen über `getInstance()` darauf zu.

**Verbindung:**

`Andere Klassen → Singleton.getInstance() → einzige Instanz`

**Warum?**

Der private Konstruktor verhindert, dass andere Klassen beliebig neue Instanzen erstellen. Die statische Methode gibt die kontrollierte Instanz zurück.

## Typische Bestandteile
- `private` Konstruktor
- `private static` Instanz
- `public static getInstance()`

## Java-Grundaufbau

```java
class Singleton {
    private static Singleton instanz = new Singleton();

    private Singleton() {
    }

    public static Singleton getInstance() {
        return instanz;
    }
}
```

Verwendung:

```java
Singleton s1 = Singleton.getInstance();
Singleton s2 = Singleton.getInstance();
```

`s1` und `s2` verweisen hier auf dasselbe Objekt.

## Vorgehen in der Prüfung
1. Konstruktor auf `private` setzen.
2. Statische Instanz innerhalb der Klasse erstellen.
3. Öffentliche statische Methode `getInstance()` anbieten.
4. Andere Klassen verwenden diese Methode statt `new`.

**Merksatz:** Privater Konstruktor, eine Instanz, zentraler Zugriff.

---

# 5. Factory Method Pattern – Fabrikmethode

## Erkennungsmerkmale
- Objekte sollen erzeugt werden, ohne die konkrete Klasse direkt festzulegen.
- Unterklassen sollen entscheiden, welches Produkt erstellt wird.
- Mehrere konkrete Produkte besitzen eine gemeinsame Schnittstelle.

**Beispiel:** Eine Fabrik erstellt unterschiedliche Dokumenttypen.

## Klassen und Verbindungen

- **Product:** Gemeinsames Produkt-Interface.
- **ConcreteProduct:** Implementiert Product.
- **Creator:** Definiert eine Factory-Methode.
- **ConcreteCreator:** Überschreibt die Factory-Methode und erzeugt ein konkretes Produkt.

**Verbindung:**

`ConcreteCreator → ConcreteProduct → Product`

Der Creator stellt die Erzeugungsmethode bereit.

**Warum?**

Der Code, der das Produkt verwendet, muss nicht selbst entscheiden, welche konkrete Klasse erzeugt wird. Die konkrete Creator-Unterklasse übernimmt diese Entscheidung.

## Typische Methoden
- `erzeugeProdukt()`
- eine Methode, die das Produkt verwendet

## Java-Grundaufbau

```java
interface Produkt {
    void anzeigen();
}

class ProduktA implements Produkt {
    public void anzeigen() {
        System.out.println("Produkt A");
    }
}

abstract class Creator {
    public abstract Produkt erzeugeProdukt();
}

class CreatorA extends Creator {
    public Produkt erzeugeProdukt() {
        return new ProduktA();
    }
}
```

## Vorgehen in der Prüfung
1. Product-Interface erstellen.
2. Konkrete Produkte implementieren das Interface.
3. Creator definiert die Factory-Methode.
4. ConcreteCreator überschreibt sie und erzeugt ein konkretes Produkt.

**Merksatz:** Die Unterklasse entscheidet, welches Produkt erzeugt wird.

---

# 6. Command Pattern – Befehl

## Erkennungsmerkmale
- Eine Aktion soll als Objekt dargestellt werden.
- Befehle sollen gespeichert, weitergegeben oder später ausgeführt werden.
- Der Auslöser einer Aktion soll von der eigentlichen Ausführung getrennt sein.
- Eventuell sollen Befehle rückgängig gemacht werden können.

**Beispiel:** Eine Fernbedienung schaltet einen Fernseher ein oder wechselt den Kanal.

## Klassen und Verbindungen

- **Invoker:** Löst einen Befehl aus und speichert gegebenenfalls das Command-Objekt.
- **Command:** Gemeinsames Befehls-Interface.
- **ConcreteCommand:** Implementiert Command und kennt den Receiver.
- **Receiver:** Führt die eigentliche Aktion aus.

**Verbindung:**

`Invoker → Command ← ConcreteCommand → Receiver`

**Warum?**

Der Invoker muss nicht wissen, wie die Aktion umgesetzt wird. Der konkrete Befehl verbindet den Aufruf mit dem Objekt, das die Arbeit tatsächlich ausführt.

## Typische Methoden
- `ausfuehren()`
- optional `undo()`

## Java-Grundaufbau

```java
interface Kommando {
    void ausfuehren();
}

class Fernseher {
    public void einschalten() {
        System.out.println("Fernseher eingeschaltet");
    }
}

class EinschaltenKommando implements Kommando {
    private Fernseher fernseher;

    public EinschaltenKommando(Fernseher fernseher) {
        this.fernseher = fernseher;
    }

    public void ausfuehren() {
        fernseher.einschalten();
    }
}

class Fernbedienung {
    private Kommando kommando;

    public void setKommando(Kommando kommando) {
        this.kommando = kommando;
    }

    public void druecken() {
        kommando.ausfuehren();
    }
}
```

## Vorgehen in der Prüfung
1. Command-Interface mit `ausfuehren()` erstellen.
2. Receiver enthält die eigentliche Funktion.
3. ConcreteCommand speichert den Receiver.
4. ConcreteCommand ruft die passende Receiver-Methode auf.
5. Invoker speichert und startet das Kommando.

**Merksatz:** Der Invoker löst aus, das Command vermittelt, der Receiver arbeitet.

---

# 7. Adapter Pattern – Adapter

## Erkennungsmerkmale
- Zwei Klassen besitzen inkompatible Schnittstellen.
- Eine vorhandene Klasse soll weiterverwendet werden.
- Der Client erwartet eine andere Methode als die vorhandene Klasse anbietet.

**Beispiel:** Ein Adapter verbindet ein Gerät mit einem Anschluss, der nicht direkt passt.

## Klassen und Verbindungen

- **Client:** Verwendet die gewünschte Schnittstelle.
- **Target:** Interface, das der Client erwartet.
- **Adapter:** Implementiert Target und kennt den Adaptee.
- **Adaptee:** Vorhandene Klasse mit einer anderen Schnittstelle.

**Verbindung:**

`Client → Target ← Adapter → Adaptee`

**Warum?**

Der Client kann mit dem Target arbeiten. Der Adapter übersetzt dessen Methodenaufrufe in Aufrufe, die der Adaptee versteht.

## Typische Bestandteile
- Target-Methode, zum Beispiel `ausgeben()`
- Adapter implementiert Target
- Adapter ruft eine passende Adaptee-Methode auf

## Java-Grundaufbau

```java
interface Target {
    void ausgeben();
}

class Adaptee {
    public void spezielleAusgabe() {
        System.out.println("Spezielle Ausgabe");
    }
}

class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    public void ausgeben() {
        adaptee.spezielleAusgabe();
    }
}
```

## Vorgehen in der Prüfung
1. Target-Interface entsprechend der erwarteten Schnittstelle erstellen.
2. Adapter implementiert Target.
3. Adapter speichert den Adaptee.
4. Adapter übersetzt den Aufruf in die vorhandene Methode.

**Merksatz:** Der Adapter übersetzt eine Schnittstelle in eine andere.

---

# 8. Facade Pattern – Fassade

## Erkennungsmerkmale
- Ein System besteht aus mehreren Klassen.
- Mehrere Schritte müssen in einer bestimmten Reihenfolge aufgerufen werden.
- Die Verwendung des Systems soll vereinfacht werden.

**Beispiel:** Ein Heimkinosystem wird mit einem einzigen Aufruf gestartet.

## Klassen und Verbindungen

- **Client:** Verwendet die Facade.
- **Facade:** Bietet eine vereinfachte Schnittstelle.
- **Subsystem-Klassen:** Erledigen die einzelnen Aufgaben.

**Verbindung:**

`Client → Facade → Subsystem-Klassen`

**Warum?**

Der Client muss die einzelnen Subsysteme nicht selbst koordinieren. Die Facade ruft die benötigten Methoden in der richtigen Reihenfolge auf.

## Typische Methoden
- `starten()`
- `beenden()`
- andere vereinfachende Methoden, passend zur Aufgabe

## Java-Grundaufbau

```java
class Licht {
    public void einschalten() {
        System.out.println("Licht an");
    }
}

class Projektor {
    public void einschalten() {
        System.out.println("Projektor an");
    }
}

class HeimkinoFacade {
    private Licht licht = new Licht();
    private Projektor projektor = new Projektor();

    public void starten() {
        licht.einschalten();
        projektor.einschalten();
    }
}
```

## Vorgehen in der Prüfung
1. Subsystem-Klassen mit ihren jeweiligen Aufgaben erstellen.
2. Facade speichert oder verwendet diese Klassen.
3. Facade bietet eine einfache Methode an.
4. Diese Methode koordiniert die notwendigen Aufrufe.
5. Client verwendet nur die Facade.

**Merksatz:** Die Facade vereinfacht den Zugriff auf mehrere Klassen.

---

# 9. Template Method Pattern – Schablonenmethode

## Erkennungsmerkmale
- Der allgemeine Ablauf ist für mehrere Varianten gleich.
- Einzelne Schritte unterscheiden sich.
- Unterklassen sollen bestimmte Schritte anpassen.
- Die Reihenfolge des Gesamtalgorithmus soll vorgegeben bleiben.

**Beispiel:** Verschiedene Getränke werden nach demselben Grundablauf zubereitet.

## Klassen und Verbindungen

- **AbstractClass:** Definiert die Template-Methode und die einzelnen Schritte.
- **ConcreteClassA / ConcreteClassB:** Erben von AbstractClass und implementieren oder überschreiben bestimmte Schritte.

**Verbindung:**

`ConcreteClassA / ConcreteClassB → AbstractClass`

**Warum?**

Die Oberklasse legt die Reihenfolge fest. Unterklassen passen einzelne Schritte an, ohne den grundlegenden Ablauf neu definieren zu müssen.

## Typische Methoden
- Template-Methode, zum Beispiel `zubereiten()`
- einzelne Schritte, zum Beispiel `wasserErhitzen()`
- abstrakte Methoden für variable Schritte

## Java-Grundaufbau

```java
abstract class Getraenk {
    public final void zubereiten() {
        wasserErhitzen();
        zutatHinzufuegen();
        servieren();
    }

    protected void wasserErhitzen() {
        System.out.println("Wasser erhitzen");
    }

    protected abstract void zutatHinzufuegen();

    protected void servieren() {
        System.out.println("Getränk servieren");
    }
}

class Tee extends Getraenk {
    protected void zutatHinzufuegen() {
        System.out.println("Tee hinzufügen");
    }
}
```

## Vorgehen in der Prüfung
1. Abstrakte Oberklasse erstellen.
2. Template-Methode mit festgelegter Reihenfolge definieren.
3. Gemeinsame Schritte in der Oberklasse implementieren.
4. Variable Schritte als abstrakte oder überschreibbare Methoden definieren.
5. Unterklassen implementieren oder überschreiben diese Schritte.

**Merksatz:** Die Oberklasse bestimmt den Ablauf, Unterklassen passen einzelne Schritte an.

---

# 10. Iterator Pattern – Iterator

## Erkennungsmerkmale
- Elemente einer Sammlung sollen nacheinander durchlaufen werden.
- Der Client soll die interne Datenstruktur nicht kennen müssen.
- Es gibt eine Methode für das nächste Element und eine Prüfung, ob noch Elemente vorhanden sind.

**Beispiel:** Alle Artikel einer Einkaufstasche werden nacheinander ausgegeben.

## Klassen und Verbindungen

- **Aggregate:** Schnittstelle für eine Sammlung.
- **ConcreteAggregate:** Enthält die Elemente und stellt einen Iterator bereit.
- **Iterator:** Definiert die Methoden zum Durchlaufen.
- **ConcreteIterator:** Verwaltet die aktuelle Position.
- **Client:** Verwendet den Iterator.

**Verbindung:**

`Client → Iterator ← ConcreteIterator → ConcreteAggregate`

Die Sammlung stellt einen passenden Iterator bereit.

**Warum?**

Der Client kann die Sammlung durchlaufen, ohne wissen zu müssen, ob die Elemente beispielsweise in einer Liste oder einem Array gespeichert sind. Der Iterator kümmert sich um die Position.

## Typische Methoden
- `iterator()`
- `hasNext()`
- `next()`

## Java-Grundaufbau

```java
import java.util.Iterator;
import java.util.List;
import java.util.ArrayList;

class Einkaufstasche {
    private List<String> artikel = new ArrayList<>();

    public void addArtikel(String artikelName) {
        artikel.add(artikelName);
    }

    public Iterator<String> iterator() {
        return artikel.iterator();
    }
}

class Main {
    public static void main(String[] args) {
        Einkaufstasche tasche = new Einkaufstasche();
        tasche.addArtikel("Labello");
        tasche.addArtikel("Handcreme");

        Iterator<String> iterator = tasche.iterator();

        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

## Vorgehen in der Prüfung
1. Sammlung mit mehreren Elementen erstellen.
2. Iterator bereitstellen.
3. Iterator verwaltet die Position.
4. Mit `hasNext()` prüfen, ob noch Elemente vorhanden sind.
5. Mit `next()` das nächste Element abrufen.

**Merksatz:** Der Iterator durchläuft eine Sammlung, ohne ihre interne Struktur offenzulegen.

---

# Wichtige Unterschiede für die Prüfung

## Strategy oder Decorator?
- **Strategy:** Tauscht das Verhalten aus.
- **Decorator:** Ergänzt das Verhalten eines Objekts.

## Adapter oder Facade?
- **Adapter:** Macht inkompatible Schnittstellen kompatibel.
- **Facade:** Vereinfacht die Nutzung mehrerer Klassen.

## Strategy oder Template Method?
- **Strategy:** Verhalten wird über ein austauschbares Objekt ausgewählt.
- **Template Method:** Der Ablauf steht in der Oberklasse; Unterklassen passen Schritte an.

## Factory Method oder Singleton?
- **Factory Method:** Entscheidet, welches Produkt erzeugt wird.
- **Singleton:** Stellt eine einzige Instanz bereit.

## Observer oder Command?
- **Observer:** Informiert mehrere registrierte Objekte über Änderungen.
- **Command:** Kapselt einen Befehl als Objekt.

---


# Die 10 Merksätze auf einen Blick

1. **Strategy:** Verhalten austauschbar machen.
2. **Decorator:** Objekte flexibel erweitern.
3. **Observer:** Registrierte Beobachter benachrichtigen.
4. **Singleton:** Nur eine Instanz bereitstellen.
5. **Factory Method:** Produkterzeugung an Unterklassen auslagern.
6. **Command:** Befehle als Objekte kapseln.
7. **Adapter:** Schnittstellen kompatibel machen.
8. **Facade:** Komplexe Abläufe vereinfachen.
9. **Template Method:** Ablauf vorgeben, Schritte anpassen.
10. **Iterator:** Sammlung einheitlich durchlaufen.
