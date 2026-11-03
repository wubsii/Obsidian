**Kategorie:** Verhaltensmuster (Behavioral Pattern)

## Was ist das Iterator Pattern?

Das Iterator Pattern ermöglicht es, nacheinander auf die Elemente einer Datenstruktur zuzugreifen, ohne deren interne Struktur kennen zu müssen.

Der Iterator verwaltet dabei die aktuelle Position innerhalb der Sammlung.

## Welches Problem löst es?

Ein Programm besitzt eine Sammlung von Objekten, beispielsweise eine Liste mit Namen.

Der Client soll alle Elemente durchlaufen können, ohne wissen zu müssen, wie die Sammlung intern gespeichert wird.

Der Iterator stellt dafür eine einheitliche Schnittstelle bereit.

## Aufbau

- **Iterator:** Definiert die Methoden zum Durchlaufen der Elemente.
- **Concrete Iterator:** Implementiert die Iteration und verwaltet die aktuelle Position.
- **Aggregate / Collection:** Stellt eine Sammlung von Elementen bereit.
- **Concrete Aggregate:** Die konkrete Sammlung, beispielsweise eine Liste.
- **Client:** Verwendet den Iterator, um die Elemente zu durchlaufen.

## Wichtige Methoden in Java

- `hasNext()` – Prüft, ob ein weiteres Element vorhanden ist.
- `next()` – Gibt das nächste Element zurück und bewegt die Position weiter.
- `remove()` – Kann je nach Implementierung das zuletzt zurückgegebene Element entfernen.

Das Interface `Iterable` ermöglicht es, Objekte in einer erweiterten `for`-Schleife zu verwenden.

## Beispiel in Java

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

class Main {
    public static void main(String[] args) {
        List<String> namen = new ArrayList<>();

        namen.add("Anna");
        namen.add("Max");
        namen.add("Lisa");

        Iterator<String> iterator = namen.iterator();

        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

Ausgabe:

```text
Anna
Max
Lisa
```

Die Schleife muss nicht wissen, wie die Liste intern aufgebaut ist.

## Vorteile

- Einheitlicher Zugriff auf Elemente.
- Die interne Struktur der Sammlung bleibt verborgen.
- Die Sammlung und die Iteration werden voneinander getrennt.
- Elemente können nacheinander verarbeitet werden.

## Nachteile

- Zusätzlicher Aufwand für eigene Iterator-Implementierungen.
- Bei ungültiger Verwendung von `next()` kann eine `NoSuchElementException` auftreten.
- Änderungen an einer Sammlung während der Iteration können je nach Implementierung Probleme verursachen.

## Eselsbrücke

**Iterator = Schritt für Schritt durchgehen.**

Wie eine Einkaufsliste: Du gehst einen Eintrag nach dem anderen durch, ohne wissen zu müssen, wie die Liste intern gespeichert ist.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Iterator Patterns?**

Antwort: Auf die Elemente einer Datenstruktur nacheinander zuzugreifen, ohne ihre interne Struktur kennen zu müssen.

**Frage 2: Was macht `hasNext()`?**

Antwort: Die Methode prüft, ob noch ein weiteres Element vorhanden ist.

**Frage 3: Was macht `next()`?**

Antwort: Die Methode liefert das nächste Element und bewegt die Position des Iterators weiter.

**Frage 4: Was ist der Unterschied zwischen `Iterator` und `Iterable`?**

Antwort: `Iterator` ermöglicht das Durchlaufen einer Sammlung. `Iterable` stellt die Methode `iterator()` bereit und ermöglicht dadurch unter anderem die Verwendung einer erweiterten `for`-Schleife.

**Frage 5: Warum verwendet man einen Iterator?**

Antwort: Der Client kann Elemente einheitlich durchlaufen, ohne von der internen Implementierung der Sammlung abhängig zu sein.

**Frage 6: Was passiert, wenn `next()` aufgerufen wird, obwohl kein Element mehr vorhanden ist?**

Antwort: Bei Java-Iteratoren wird normalerweise eine `NoSuchElementException` ausgelöst.

**Frage 7: Nenne ein Anwendungsbeispiel.**

Antwort: Alle Namen einer Liste nacheinander ausgeben oder alle Produkte eines Warenkorbs durchlaufen.

**Merksatz:** Iterator ermöglicht das Durchlaufen einer Sammlung, ohne ihre interne Struktur kennen zu müssen.