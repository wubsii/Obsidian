**Kategorie:** Strukturmuster (Structural Pattern)

## Was ist das Facade Pattern?

Das Facade Pattern stellt eine vereinfachte, einheitliche Schnittstelle für ein komplexes Subsystem bereit.

Die Fassade bündelt mehrere Aufrufe und ermöglicht dem Client, eine komplexe Funktion über eine einfache Methode zu verwenden.

## Welches Problem löst es?

Um einen Film im Heimkino zu starten, müssen möglicherweise mehrere Geräte bedient werden:

- Popcornmaschine einschalten
- Leinwand aktivieren
- Projektor einschalten
- Soundsystem starten

Ohne Facade müsste der Client jede einzelne Klasse und ihre Methoden kennen.

Mit Facade genügt beispielsweise ein Aufruf von `filmStarten()`.

## Aufbau

- **Facade:** Bietet eine vereinfachte Schnittstelle.
- **Subsystem-Klassen:** Führen die einzelnen Aufgaben aus.
- **Client:** Verwendet die Fassade statt alle Subsysteme direkt anzusprechen.

## Beispiel in Java

```java
class Projektor {
    public void einschalten() {
        System.out.println("Projektor eingeschaltet");
    }
}

class Soundsystem {
    public void starten() {
        System.out.println("Soundsystem gestartet");
    }
}

class Leinwand {
    public void herunterfahren() {
        System.out.println("Leinwand heruntergefahren");
    }
}

class HeimkinoFacade {
    private Projektor projektor = new Projektor();
    private Soundsystem soundsystem = new Soundsystem();
    private Leinwand leinwand = new Leinwand();

    public void filmStarten() {
        leinwand.herunterfahren();
        projektor.einschalten();
        soundsystem.starten();
    }
}
```

Verwendung:

```java
HeimkinoFacade heimkino = new HeimkinoFacade();

heimkino.filmStarten();
```

Der Client muss die einzelnen Geräte nicht direkt steuern.

## Vorteile

- Komplexe Abläufe werden vereinfacht.
- Der Client benötigt weniger Wissen über das Subsystem.
- Die Benutzung wird übersichtlicher.
- Die Abhängigkeiten zwischen Client und Subsystem können reduziert werden.

## Nachteile

- Die Fassade kann zu viele Aufgaben übernehmen.
- Bei schlechter Gestaltung entsteht eine zentrale Klasse, die schwer wartbar wird.
- Für einfache Subsysteme kann sie unnötig sein.

## Eselsbrücke

**Facade = Fassade eines Hauses.**

Du siehst eine einfache Vorderseite, obwohl sich dahinter viele Räume und Komponenten befinden.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Facade Patterns?**

Antwort: Eine vereinfachte Schnittstelle für ein komplexes Subsystem bereitzustellen.

**Frage 2: Warum verwendet man eine Fassade?**

Antwort: Damit der Client nicht alle einzelnen Klassen und deren Methoden kennen und selbst aufrufen muss.

**Frage 3: Muss die Fassade die Subsystem-Klassen ersetzen?**

Antwort: Nein. Die Subsystem-Klassen bleiben bestehen. Die Fassade vereinfacht lediglich ihren Zugriff.

**Frage 4: Was ist der Unterschied zwischen Facade und Adapter?**

Antwort: Facade vereinfacht den Zugriff auf mehrere Komponenten. Adapter macht eine inkompatible Schnittstelle passend.

**Frage 5: Kann man die Subsysteme weiterhin direkt verwenden?**

Antwort: Ja. Eine Fassade bietet einen vereinfachten Zugriff, muss aber nicht sämtliche direkten Zugriffe verhindern.

**Frage 6: Nenne ein Anwendungsbeispiel.**

Antwort: Eine Heimkino-Fassade startet Projektor, Soundsystem und Leinwand über eine einzige Methode.

**Merksatz:** Facade vereinfacht die Verwendung eines komplexen Systems.
