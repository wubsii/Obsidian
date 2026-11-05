# Software Design – Die Kurzfassung

*Von oben nach unten lesen. Jedes Pattern = ein Bild + ein Satz. Sonst nichts.*

## Schritt 1: Die 3 Gruppen

| Gruppe        | Welche Frage beantwortet sie?          | Patterns                                                                 |
| ------------- | -------------------------------------- | ------------------------------------------------------------------------ |
| **Erzeugung** | Wie erzeuge ich Objekte?               | Singleton, Factory                                                       |
| **Struktur**  | Wie kombiniere ich Objekte?            | Decorator, Adapter, Facade (AFD)                                         |
| **Verhalten** | Wie handeln und kommunizieren Objekte? | Strategy, Observer, Command, Template, Iterator (Cat Idle On Sofa Today) |

## Schritt 2: Ein Bild pro Pattern

**Strategy** – Die Waffe im Spiel wechseln. Ein Objekt *hat* ein Verhalten und du kannst es zur Laufzeit austauschen.

**Decorator** – Ein Geschenk in Schichten einpacken. Objekt umhüllen, etwas hinzufügen, gleicher Typ, beliebig oft stapelbar (Kaffee + Milch + Sirup).

**Observer** – Die Abo-Glocke bei YouTube. Eine Quelle, viele Abonnenten. Es passiert etwas → alle werden informiert.

**Singleton** – Es gibt nur einen Präsidenten. Genau ein Objekt, nie mehr. Alle bekommen dasselbe.

**Factory Method** – Eine Franchise-Küche. Uberall derselbe Ablauf, aber jede Filiale entscheidet selbst, welches Produkt sie herstellt.

**Command** – Ein Bestellzettel im Restaurant. Eine Aktion wird zum Objekt: du kannst sie in eine Warteschlange stellen, loggen oder rückgängig machen.

**Adapter** – Ein Reisestecker-Adapter. Macht etwas mit dem falschen Stecker passend für die Steckdose, die du hast.

**Facade** – Ein einziger „Film-Modus“-Knopf. Ein einfacher Knopf löst 10 komplizierte Dinge im Hintergrund aus.

**Template Method** – Eine Rezeptkarte mit Lücken. Die Reihenfolge der Schritte ist fix (`final`), Subklassen füllen nur bestimmte Schritte aus.

**Iterator** – Die „Weiter“-Taste in einer Playlist. Elemente einzeln durchgehen, ohne zu wissen, wie sie gespeichert sind (`hasNext()`, `next()`).

## Schritt 3: Wort sehen → Pattern wählen

| Wenn in der Angabe steht... | Dann |
| --- | --- |
| „zur Laufzeit ändern“, „verschiedene Algorithmen/Berechnungen“ | **Strategy** |
| „Zusätze“, „Extras“, „kombinieren/stapeln“, „Kosten addieren sich“ | **Decorator** |
| „alle informieren“, „registrieren“, „abonnieren“, „Events“ | **Observer** |
| „nur eine Instanz“ | **Singleton** |
| „Fabrik“, „Produkte erzeugen“, „jede Fabrik stellt ihre eigenen her“ | **Factory** |
| „undo“, „Fernbedienung“, „Warteschlange von Aktionen“ | **Command** |
| „inkompatibel“, „passt nicht“, „Interface umwandeln“ | **Adapter** |
| „vereinfachen“, „ein Aufruf macht alles“ | **Facade** |
| „gleiche Schritte, wenige unterscheiden sich“ | **Template** |
| „alle Elemente durchgehen“, „for-each“ | **Iterator** |

## Schritt 4: Die 5 Verwechslungen (und wie du sie unterscheidest)

1. **Strategy vs. Decorator** → Strategy *ersetzt* das Verhalten. Decorator *fügt oben drauf*.
2. **Strategy vs. Template** → Strategy = Objekt austauschen (Komposition). Template = Schritte überschreiben (Vererbung).
3. **Adapter vs. Facade** → Adapter *wandelt* ein Interface *um*. Facade *vereinfacht* viele.
4. **Observer vs. Command** → Observer *benachrichtigt* viele. Command *verpackt eine Aktion*.
5. **Simple Factory vs. Factory Method** → Simple Factory = eine Klasse mit if/else. Factory Method = abstrakte Methode + Subklassen entscheiden.

## Schritt 5: Die 4 großen Ideen (Theoriefragen)

- **Kapsle, was sich ändert** – den Teil herausziehen, der sich oft ändert. *(Strategy)*
- **Programmiere gegen Interfaces** – den abstrakten Typ verwenden, nicht die konkrete Klasse.
- **Komposition (has-a) vor Vererbung (is-a)** – flexibler, zur Laufzeit austauschbar.
- **Lose Kopplung** – Klassen wissen so wenig wie möglich voneinander. *(Observer)*

Zusatz-Paare: **Open-Closed** = Decorator. **Dependency Inversion** = Factory.

## Schritt 6: Praxisteil – nur zwei Vorlagen

### Factory

```java
abstract class Factory {
    public Product getProduct(ProductType t) {  // fixer Ablauf, Signatur nie ändern
        Product p = createProduct(t);
        if (p != null) { /* Seriennummer */ }
        return p;
    }
    protected abstract Product createProduct(ProductType t);
}
class BootFactory extends Factory {
    protected Product createProduct(ProductType t) {
        return t == ProductType.BOOTS ? new Boots() : null;  // falscher Typ = null
    }
}
```

### Observer

```java
// Client
public void startGame(GameServer s) { server = s; server.register(this); }
public void endGame() { server.unregister(this); server = null; }
public void update(EventData e) { if (/* Bedingung */) { /* ausführen */ } }

// Server
public void newEvents(...) {
    lastEvent = new EventData(...);
    notifyClients();                 // eigene Methode!
}
private void notifyClients() {
    for (GameClient c : new ArrayList<>(clients)) c.update(lastEvent);
}
```

*Die Methodennamen sind geraten. Nimm die echten aus dem Startpaket.*

### Checkliste mit 6 Punkten

1. Vorgegebene Signaturen und Interfaces nie ändern.
2. Bedingungen wörtlich lesen: „mindestens“ = `>=`.
3. Strings mit `.equals()` vergleichen, nicht mit `==`.
4. Bedingung nicht erfüllt = nichts tun.
5. Benachrichtigen in einer eigenen Methode.
6. Ein `Main` schreiben und testen, auch wenn niemand danach fragt.
