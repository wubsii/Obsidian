
*Basierend auf Folienset 1–6 (Strategy, Decorator, Observer, Singleton, Factory, Command, Adapter, Facade, Template, Iterator) und der Nachklausur 2020. Einige Folien bestanden nur aus Diagrammen; diese Teile sind mit der Standardstruktur aus Head First / GoF ergänzt.*

  

## 1. Überblick in 60 Sekunden

  

| Pattern | Art | Kernidee in einem Satz | Schlüsselwörter in der Angabe |

| --- | --- | --- | --- |

| **Strategy** | Verhaltensmuster | Algorithmus zur Laufzeit austauschen; Objekt HAT ein Verhalten (Interface) | Verhalten ändert sich zur Laufzeit, Familie von Algorithmen, Provision 10% vs. 5%, Flugverhalten |

| **Decorator** | Strukturmuster | Objekt (gleicher Supertyp) umhüllen, um dynamisch Verantwortung hinzuzufügen | stapelbare Extras, Milch + Sirup + Schaum, Kosten summieren sich, Wrapper |

| **Observer** | Verhaltensmuster | Eins-zu-viele: Subject informiert alle registrierten Observer | registrieren/abmelden, Abonnenten, alle Clients informieren, Events, Abo |

| **Singleton** | Erzeugungsmuster | Genau eine Instanz + globaler Zugriffspunkt | Einstellungen, Logging, Cache, DB-Verbindung |

| **Factory Method** | Erzeugungsmuster | Abstrakte Erzeugungsmethode im Creator; Subklassen entscheiden, welche Klasse erzeugt wird | Fabrik, createX, enum wählt Produkt, regionale Varianten, Franchise |

| **Command** | Verhaltensmuster | Befehl als Objekt: Warteschlange, Log, Undo | Fernbedienung, Knöpfe, undo, execute() |

| **Adapter** | Strukturmuster | Interface in das vom Client erwartete umwandeln | inkompatibles Interface, Truthahn→Ente, Mediaplayer |

| **Facade** | Strukturmuster | Ein einfaches Interface vor einem komplexen Subsystem | Filmabend, startMovie(), viele Aufrufe vereinfachen |

| **Template Method** | Verhaltensmuster | Algorithmus-Skelett in finaler Methode der Oberklasse; Subklassen füllen Schritte | Kaffee/Tee, duplizierter Code bei ähnlichen Rezepten |

| **Iterator** | Verhaltensmuster | Sequentieller Zugriff, ohne den Aufbau der Datenstruktur zu kennen | hasNext(), next(), Iterable, for-each |

  

**Drei Kategorien:** Verhaltensmuster (Behavioral) = Verhalten von Klassen, Zusammenarbeit und Nachrichtenaustausch zwischen Objekten. Erzeugungsmuster (Creational) = Objekterzeugung: variieren, welches Objekt erzeugt wird, bzw. andere Objekte zur Erzeugung verwenden. Strukturmuster (Structural) = Klassen oder Objekte werden zu einer größeren Struktur kombiniert (Vereinfachung der Struktur).

  

**Ein Pattern** = eine Lösung zu einem immer wiederkehrenden Problem; ein Konzept, kein fertiger Code. Ursprung: Gang of Four, 90er, Buch *Design Patterns: Elements of Reusable Object-Oriented Software*.

  

**Anforderungen an Software Design:** Erweiterbarkeit, Wartbarkeit, Wiederverwendbarkeit, Testbarkeit.

  

## 2. Was ist was? (die verwechselbaren Paare)

  

**Strategy vs. Decorator vs. Template Method** – alle ändern Verhalten, aber unterschiedlich:

  

- **Strategy**: ersetzt den *ganzen* Algorithmus. Komposition (has-a), änderbar zur *Laufzeit*.

- **Decorator**: *fügt* Verhalten um ein bestehendes Objekt *hinzu*. Umhüllt es, gleicher Supertyp, stapelbar, zur Laufzeit.

- **Template Method**: Ablauf steht fix in der Oberklasse (`final`); Subklassen überschreiben einzelne Schritte. *Vererbung*, zur Übersetzungszeit festgelegt.

  

**Adapter vs. Facade vs. Decorator** – alle umhüllen etwas:

  

- **Adapter**: ändert das Interface, damit eine inkompatible Klasse zu dem passt, was der Client erwartet. Meist EIN Objekt.

- **Facade**: vereinfacht die Benutzung VIELER Klassen hinter einem neuen, einfacheren Interface.

- **Decorator**: behält das GLEICHE Interface und fügt Verhalten hinzu.

  

**Simple Factory vs. Factory Method** – die Folien sagen ausdrücklich, die Simple Factory ist *noch nicht die richtige Lösung*:

  

- **Simple Factory**: eine Klasse mit einer Erzeugungsmethode voller if/else. Einfach, aber nicht per Vererbung erweiterbar.

- **Factory Method**: Creator-Klasse mit fixem Ablauf plus *abstrakter* Erzeugungsmethode; jede Subklasse (z. B. NY-, Chicago-Store) entscheidet, was erzeugt wird.

  

**Observer vs. Command**:

  

- **Observer**: eine Quelle *schickt Benachrichtigungen* über eine Änderung an viele Listener.

- **Command**: verpackt eine *Aktion* (samt Empfänger) als Objekt, der Invoker weiß nicht, was sie tut; ermöglicht Queue/Log/Undo.

  

**Strategy vs. Command**: Strategy = austauschbarer Algorithmus in einem Objekt. Command = eine *Anfrage*, die später ausgeführt (und ggf. rückgängig gemacht) wird.

  

**Vererbung vs. Komposition**: is-a (Vererbung, UML: hohles Dreieck) vs. has-a (Komposition). Regel der Folien: *Bevorzuge has-a gegenüber is-a*, weil man Verhalten zur Laufzeit austauschen kann.

  

## 3. Design-Prinzipien (typische Theoriefragen)

  

| Prinzip | Bedeutung | Wo es vorkommt |

| --- | --- | --- |

| **Kapsle, was sich ändert** (*das* Design-Prinzip) | Aspekte, die sich häufig ändern, von jenen trennen, die gleich bleiben | Strategy |

| **Programmiere gegen ein Interface (Supertyp), nicht gegen eine konkrete Implementierung** | Deklarierter Typ ist abstrakte Klasse/Interface; die Klasse muss nichts über das konkrete Objekt wissen | Strategy, Observer, Factory |

| **Bevorzuge has-a (Komposition) gegenüber is-a (Vererbung)** | Flexibler; Verhalten zur Laufzeit austauschbar; wird oft in Patterns verwendet | Strategy, Decorator |

| **Lose Kopplung** | Abhängigkeiten zwischen Teilsystemen sind minimal; Änderung des einen erzwingt keine Änderung des anderen | Observer (Subject kennt nur das Observer-Interface) |

| **Kohärenz** | Jedes Teilsystem hat eine klar umrissene Verantwortung; weniger Komplexität, einfachere Wartung | allgemein |

| **Open-Closed** | Klassen offen für Erweiterung, geschlossen für Veränderung | Decorator |

| **Dependency Inversion** | Hänge von Abstraktionen ab, nicht von konkreten Klassen | Factory (PizzaStore hängt von Pizza ab, nicht von konkreten Pizzen) |

  

**Warum das Enten-Beispiel wichtig ist:** `fliegen()` in der Oberklasse Ente ließ auch Gummienten fliegen. `fliegen()` pro Subklasse zu überschreiben bringt duplizierten Code, keine Änderung zur Laufzeit, keine zentrale Übersicht und nicht-lokale Seiteneffekte. `fliegen()` in ein Interface auszulagern erzwingt ebenfalls duplizierten Code. Lösung: das veränderliche Verhalten in ein eigenes Interface auslagern (Strategy).

  

## 4. UML-Wiederholung

  

- **Abstrakte Klasse:** Name *kursiv* oder `{abstract}`. **Interface:** `<<interface>>`.

- **Vererbung (is-a):** durchgezogene Linie, hohles Dreieck. **Interface-Implementierung:** strichlierte Linie, hohles Dreieck.

- **Assoziation:** Linie mit Bezeichnung, Leserichtung, Navigierbarkeit (Pfeil), Rollennamen. Multiplizitäten: `1`, `0..1`, `1..4`, `*`, `1..*`.

- **Aggregation:** Teil-Ganzes-Beziehung (*besteht aus / ist Teil von*), hohle Raute, Pfeile unüblich.

- **Komposition (im UML-Sinn):** strenger. Ein Teil gehört höchstens einem Ganzen, gemeinsame Lebensdauer, gefüllte Raute. Auch has-a genannt.

  

## 5. Die Patterns im Detail

  

### Strategy

  

**Definition:** Das Strategy Pattern erlaubt es, einen Algorithmus (eine Familie von Algorithmen) unabhängig von der ihn nutzenden Klasse (= Client) zu variieren.

  

```java

interface Flugverhalten { void fliegen(); }

class FliegtMitFluegeln implements Flugverhalten { public void fliegen() { /* ... */ } }

  

abstract class Ente {

    protected Flugverhalten flugverhalten;                 // HAS-A

    void performFliegen() { flugverhalten.fliegen(); }     // delegieren

    void setFlugverhalten(Flugverhalten fv) { flugverhalten = fv; } // Laufzeitänderung

}

```

  

**Übung:** Provision (der Manager hat eine Provisions-Strategie: 10% des Gewinns oder 5% des Umsatzes, zur Laufzeit änderbar; Mitarbeiter haben nur Name, Umsatz, Gewinn).

  

### Decorator (Wrapper)

  

**Definition:** Das Decorator Pattern fügt dynamisch zusätzliche Verantwortung zu einem Objekt hinzu. Decorator sind flexible Alternativen zur Ableitung, um Funktionalität zu erweitern. **Regeln:** Decorator haben den gleichen Supertyp wie die Objekte, die sie dekorieren; mehrfache Verwendung möglich; ein Decorator kann anstelle des Originals verwendet werden; er führt eigenes Verhalten kurz vor/nach der Delegation an das dekorierte Objekt aus; dynamisch zu jedem Zeitpunkt möglich.

  

```java

abstract class Getraenk { abstract double kosten(); }

class Espresso extends Getraenk { double kosten() { return 1.99; } }

abstract class ZutatDecorator extends Getraenk { }

class Milch extends ZutatDecorator {

    private final Getraenk getraenk;                   // umhüllt gleichen Supertyp

    Milch(Getraenk g) { getraenk = g; }

    double kosten() { return getraenk.kosten() + 0.30; }   // delegieren + addieren

}

Getraenk g = new Milch(new Milch(new Espresso()));     // doppelt Milch

```

  

**Java-Beispiel:** `new BufferedReader(new FileReader(...))` (java.io-Streams). **Warum:** verhindert Klassenexplosion (KaffeeMitMilchUndSoja...) und folgt dem Open-Closed-Prinzip.

  

### Observer

  

**Definition:** Das Observer Pattern definiert eine eins-zu-viele Abhängigkeit zwischen Objekten, sodass bei einer Änderung eines Objekts alle abhängigen Objekte informiert und aktualisiert werden. Analogie: Zeitungsabo (Verlag veröffentlicht; Abonnent\*innen registrieren sich und bekommen neue Ausgaben; sie bestellen das Abo ab, wenn sie nicht mehr interessiert sind). **Rollen:** Subject (Publisher) + Observer (Subscriber). **Lose Kopplung:** Das Subject weiß nur, dass das Observer-Interface implementiert wird; neue Observer können zur Laufzeit hinzugefügt werden, ohne das Subject anzufassen; beide sind unabhängig wiederverwendbar; Änderungen an einem haben keinen Einfluss auf den anderen.

  

```java

interface Observer { void update(Daten d); }

interface Subject { void registrieren(Observer o); void abmelden(Observer o); }

  

class Server implements Subject {

    private final List<Observer> observers = new ArrayList<>();

    private Daten letzte;

    public void registrieren(Observer o) { observers.add(o); }

    public void abmelden(Observer o)     { observers.remove(o); }

    private void benachrichtigen() {

        for (Observer o : new ArrayList<>(observers)) o.update(letzte); // Kopie!

    }

}

```

  

**Übungen:** Medienverlag, PodcastServer (Notebook/Smartphone/Smartwatch), Wetterstation.

  

### Singleton

  

**Definition:** Versichere, dass nur genau eine Instanz einer Klasse existiert. Stelle einen globalen Zugriffspunkt auf diese Instanz zur Verfügung. **Verwendung:** Einstellungen, Logging, Caches, grafische Komponenten, Verbindungen zu Datenbank/Netzwerk.

  

```java

public class Einstellungen {

    private static Einstellungen instance;

    private Einstellungen() { }                          // niemand sonst kann es erzeugen

    public static synchronized Einstellungen getInstance() { // synchronized = thread-sicher

        if (instance == null) instance = new Einstellungen();

        return instance;

    }

}

```

  

### Factory Method

  

**Definition:** Das Factory Pattern definiert eine Schnittstelle, um Objekte zu erzeugen, lässt aber Subklassen entscheiden, welche Klasse zu erzeugen ist. Die Factory Methode ermöglicht es, die Erzeugung von Objekten an Subklassen zu delegieren. **Pizza-Story:** Der obere Teil (welche Pizza?) ändert sich, der untere (vorbereiten, backen, schneiden, verpacken) bleibt gleich. Franchise-Filialen haben ihre eigene `createPizza`, nutzen aber den gemeinsamen `orderPizza`-Ablauf.

  

```java

abstract class PizzaStore {

    public Pizza orderPizza(String typ) {    // fixer Ablauf, für alle gleich

        Pizza p = createPizza(typ);          // die Factory-Methode

        p.prepare(); p.bake(); p.cut(); p.box();

        return p;

    }

    protected abstract Pizza createPizza(String typ);

}

class NYPizzaStore extends PizzaStore {

    protected Pizza createPizza(String typ) { /* NY-Varianten */ return null; }

}

```

  

**Übung:** Krisentrotz-Autos (PKW/LKW/Sportwagen, Fabrik in Deutschland und England, enum bestimmt den Typ, jedes Auto führt nach der Produktion hupen()/waschen() aus).

  

### Command

  

**Definition:** Das Command Pattern kapselt einen Befehl als ein Objekt. Damit kann man ihn in eine Warteschlange stellen, loggen und Operationen rückgängig machen. **Metapher:** Bestellzettel im Restaurant: trennt das *Erstellen* des Auftrags vom *Ausführer*. **Vier Rollen:** Client (erstellt das Command), Invoker (Fernbedienung, ruft `execute()` auf), Command (Interface), Receiver (TV, erledigt die eigentliche Arbeit).

  

```java

interface Command { void execute(); void undo(); }

class KanalAufCommand implements Command {

    private final TV tv;                             // Receiver

    KanalAufCommand(TV tv) { this.tv = tv; }

    public void execute() { tv.kanalAuf(); }

    public void undo()    { tv.kanalAb(); }

}

class Fernbedienung {

    Command[] slots = new Command[10];               // ein Command pro Knopf

    Deque<Command> history = new ArrayDeque<>();     // für Undo

    void druecke(int i) { slots[i].execute(); history.push(slots[i]); }

    void undo() { if (!history.isEmpty()) history.pop().undo(); }

}

```

  

### Adapter

  

**Definition:** Der Adapter konvertiert das Interface einer Klasse in ein anderes Interface, welches der Client erwartet. Er lässt Klassen gemeinsam arbeiten, die sonst inkompatible Interfaces hätten.

  

```java

class TurkeyAdapter implements Duck {         // setzt das ZIEL-Interface um

    private final Turkey turkey;              // umhüllt das Adaptee

    TurkeyAdapter(Turkey t) { turkey = t; }

    public void quack() { turkey.gobble(); }

    public void fly()   { turkey.fly(); turkey.fly(); }

}

```

  

**Übung:** Mediaplayer (siehe Moodle).

  

### Facade

  

**Definition:** Die Facade bietet ein einheitliches Interface für eine Menge an Interfaces in einem Subsystem. Sie definiert ein hochleveliges Interface, um die Subsysteme einfacher benutzen zu können.

  

```java

class HomeTheaterFacade {

    PopcornPopper popper; Screen screen; Projector projector; Amplifier amp;

    void startMovie(String film) { popper.on(); popper.pop(); screen.down(); projector.on(); amp.on(); }

    void endMovie() { /* alles umgekehrt */ }

}

```

  

### Template Method

  

**Definition:** Das Template Method Pattern definiert ein Skelett für einen Algorithmus in einer Methode, wobei Schritte an die Subklassen delegiert werden. Subklassen redefinieren gewisse Schritte, ohne die Struktur zu verändern.

  

```java

abstract class CaffeineBeverage {

    final void prepareRecipe() {        // final: Subklassen dürfen den Ablauf nicht ändern

        boilWater();                    // bei allen gleich

        brew();                         // unterschiedlich -> abstrakt

        pourInCup();                    // bei allen gleich

        addCondiments();                // unterschiedlich -> abstrakt

    }

    abstract void brew();

    abstract void addCondiments();

    void boilWater() { }

    void pourInCup() { }

}

```

  

**Zweck:** duplizierten Code vermeiden (Kaffee vs. Tee).

  

### Iterator

  

**Definition:** Das Iterator Pattern erlaubt es, auf die Elemente einer Datenstruktur sequentiell zuzugreifen, ohne den Aufbau der Datenstruktur zu kennen.

  

```java

class MenuIterator implements Iterator<Item> {     // verwaltet intern die Position

    private final Item[] items; private int pos = 0;

    MenuIterator(Item[] items) { this.items = items; }

    public boolean hasNext() { return pos < items.length; }

    public Item next() { return items[pos++]; }

}

class Menu implements Iterable<Item> {            // ermöglicht for-each

    private Item[] items;

    public Iterator<Item> iterator() { return new MenuIterator(items); }

}

```

  

`hasNext()`, `next()`, optional `remove()`. **Iterable** = die Klasse kann in einer for-each-Schleife verwendet werden, weil `iterator()` einen passenden Iterator zurückliefert.

  

## 6. Praxisteil: die Nachklausur 2020, gelöst

  

Die Klausur bestand aus **Factory (50%)** und **Observer (50%)**, mit einem Startpaket auf Moodle. Alle Unterlagen erlaubt, Abgabe als ZIP.

  

### Beispiel 1 – Nokia (Factory Method)

  

Aufgaben: `abstract String getSpeed()` in `Product` ergänzen; `Boots` („by foot“), `BaseStation3G/4G/5G` erstellen; `NokiaFactory` abstrakt machen mit abstrakter Erzeugungsmethode; `BootFactory` und `BaseStationFactory` implementieren; eigenständiges `Main` schreiben.

  

```java

public abstract class NokiaFactory {

    public Product getProduct(ProductType type) {     // Signatur NICHT ändern

        Product p = createProduct(type);              // Subklasse entscheidet

        if (p != null) { /* Seriennummer vergeben: vorhandene Logik beibehalten */ }

        return p;

    }

    protected abstract Product createProduct(ProductType type);

}

public class BootFactory extends NokiaFactory {

    protected Product createProduct(ProductType t) {

        return t == ProductType.BOOTS ? new Boots() : null;   // sonst null

    }

}

public class BaseStationFactory extends NokiaFactory {

    protected Product createProduct(ProductType t) {

        switch (t) {

            case BASESTATION_3G: return new BaseStation3G();

            case BASESTATION_4G: return new BaseStation4G();

            case BASESTATION_5G: return new BaseStation5G();

            default: return null;

        }

    }

}

```

  

*Die Enum-Konstanten sind geraten; nimm die aus dem Startpaket.* **Main:** jede Fabrik für jeden ProductType fragen und das Ergebnis ausgeben; die Boots-Fabrik muss für Basisstationen null liefern und umgekehrt.

  

### Beispiel 2 – Rollenspiel (Observer)

  

*Die Interfaces GameClient/GameServer habe ich nicht gesehen. Die Methodennamen unten sind Annahmen; übernimm die echten aus dem Startpaket.*

  

```java

public class RoleplayServer implements GameServer {

    private final List<GameClient> clients = new ArrayList<>();

    private EventData lastEvent;

  

    public void register(GameClient c)   { clients.add(c); }

    public void unregister(GameClient c) { clients.remove(c); }

  

    public void newEvents(/* Parameter */) {

        lastEvent = new EventData(/* ... */);   // 1. erzeugen + merken

        notifyClients();                         // 2. über EIGENE Methode

    }

    private void notifyClients() {

        for (GameClient c : new ArrayList<>(clients)) c.update(lastEvent);

    }

}

  

public class AppClient implements GameClient {

    private GameServer server;

    public void startGame(GameServer s) { server = s; server.register(this); }

    public void endGame() { server.unregister(this); server = null; }

    public void update(EventData e) {

        if (akku >= 20 && version >= 1000) {            // 'zumindest' = >=

            System.out.println(e.getDescription());

            lastEventURL = e.getUrl();

        }

    }

}

// ConsoleClient: gleich, aber Bedingung ist  !"Nintendo".equals(systemName)

```

  

### Stolperfallen

  

- Vorgegebene Signaturen/Interfaces NICHT ändern (getProduct, GameClient).

- Registrieren nur in `startGame`; in `endGame` abmelden UND die Referenz auf null setzen.

- Das Benachrichtigen kommt in eine eigene Methode, nicht direkt in `newEvents`.

- Strings mit `.equals()` vergleichen, nie mit `==`.

- Ungleichungen wörtlich lesen: „mindestens 20%“ = `>= 20`; „ungleich Nintendo“ = `!equals`.

- Trifft die Bedingung nicht zu: nichts tun (kein else-Zweig).

- Über eine Kopie der Client-Liste iterieren, damit ein Abmelden während des Updates nicht abstürzt.

- Die JUnit-Tests sind auskommentiert; zum Selbstcheck aktivieren, sie garantieren aber keine Korrektheit.

  

## 7. Wahrscheinliche Theoriefragen

  

| Frage | Kurzantwort |

| --- | --- |

| Welches Pattern für kombinierbare, stapelbare Zusätze? | Decorator |

| Welches Pattern ändert Verhalten zur Laufzeit per has-a? | Strategy |

| Welches Pattern für „alle Clients informieren, wenn sich der Zustand ändert“? | Observer |

| Pattern mit finaler Methode, die den Ablauf vorgibt? | Template Method |

| Pattern mit einem Einstiegspunkt zu vielen Subsystem-Klassen? | Facade |

| Pattern, das inkompatible Interfaces zusammenarbeiten lässt? | Adapter |

| Pattern für Undo und Warteschlangen von Aktionen? | Command |

| Pattern, das genau eine Instanz garantiert? | Singleton (privater Konstruktor + statisches getInstance) |

| Pattern, das den Aufbau einer Sammlung versteckt? | Iterator |

| Welches Pattern verschiebt die Erzeugung in Subklassen? | Factory Method |

| Welches Prinzip zeigt der Decorator? | Open-Closed |

| Welches Prinzip zeigt die Factory? | Dependency Inversion |

| Welches Prinzip zeigt der Observer? | Lose Kopplung |

| Was zeigt das Strategy Pattern? | Kapsle, was sich ändert; gegen Interface programmieren; Komposition vor Vererbung |

| Warum nicht einfach vererben? | Unflexibel, duplizierter Code, keine Laufzeitänderung, Seiteneffekte |

| Aggregation vs. Komposition? | Komposition: Teil gehört höchstens einem Ganzen + gemeinsame Lebensdauer |

| Ist die Simple Factory ein Design Pattern? | Die Folien nennen sie „noch nicht die richtige Lösung“; das Pattern ist die Factory Method |

| Positive Note ab? | Mehr als 50% |

  

**Richtig/Falsch-Fallen:**

  

- Der Decorator ändert das Interface: **falsch** (gleicher Supertyp).

- Adapter und Facade sind dasselbe: **falsch** (ein Interface umgewandelt vs. viele vereinfacht).

- Observer: das Subject muss die konkreten Observer-Klassen kennen: **falsch** (nur das Interface).

- Template Method verwendet Komposition: **falsch** (Vererbung).

- Strategy legt das Verhalten zur Übersetzungszeit fest: **falsch** (Austausch zur Laufzeit).

  

## 8. Lernplan

  

1. Tabelle aus Abschnitt 1 und die verwechselbaren Paare aus Abschnitt 2 auswendig lernen.

2. Jede Definition (Abschnitt 5) in eigenen Worten wiedergeben können.

3. Ohne Unterlagen von null neu programmieren: **Provision (Strategy)**, **Kaffee (Decorator)**, **Podcast / Medienverlag (Observer)**, **Krisentrotz (Factory)**, **TV-Fernbedienung mit Undo (Command)**, **Mediaplayer (Adapter)**.

4. Die Klausur 2020 in unter 120 Minuten ohne Blick auf die Lösung oben nochmal lösen.

5. Bei jeder Übung die Rollen benennen (Subject, Observer, Creator, Receiver, Invoker usw.).