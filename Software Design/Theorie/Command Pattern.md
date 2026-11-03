**Kategorie:** Verhaltensmuster (Behavioral Pattern)

## Was ist das Command Pattern?

Das Command Pattern kapselt einen Befehl als eigenes Objekt.

Dadurch werden die Erstellung eines Auftrags und seine tatsächliche Ausführung voneinander getrennt.

Ein Befehl kann gespeichert, protokolliert, in eine Warteschlange gestellt oder – bei entsprechender Implementierung – rückgängig gemacht werden.

## Welches Problem löst es?

Eine Fernbedienung soll unterschiedliche Geräte steuern können.

Ohne Command müsste die Fernbedienung die konkreten Geräte und deren Methoden direkt kennen.

Mit Command erhält jede Aktion ein eigenes Kommandoobjekt.

## Aufbau

- **Command:** Interface mit einer Methode zur Ausführung.
- **Concrete Command:** Implementiert einen konkreten Befehl.
- **Receiver:** Führt die eigentliche Aktion aus.
- **Invoker:** Löst den Befehl aus.
- **Client:** Erstellt die Objekte und verbindet sie miteinander.

## Beispiel in Java

```java
interface Kommando {
    void ausfuehren();
}

class TV {
    public void einschalten() {
        System.out.println("TV eingeschaltet");
    }
}

class EinschaltenKommando implements Kommando {
    private TV tv;

    public EinschaltenKommando(TV tv) {
        this.tv = tv;
    }

    public void ausfuehren() {
        tv.einschalten();
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

Verwendung:

```java
TV tv = new TV();

Kommando kommando = new EinschaltenKommando(tv);

Fernbedienung fernbedienung = new Fernbedienung();
fernbedienung.setKommando(kommando);

fernbedienung.druecken();
```

Ausgabe:

```text
TV eingeschaltet
```

## Undo-Funktion

Ein Command kann zusätzlich eine Methode wie `undo()` besitzen.

Damit eine Aktion rückgängig gemacht werden kann, muss das Kommando beispielsweise den vorherigen Zustand speichern.

Beispiel: Eine Fernbedienung erhöht den Kanal und kann danach zum vorherigen Kanal zurückkehren.

## Vorteile

- Befehle werden als Objekte behandelt.
- Invoker und Receiver sind voneinander entkoppelt.
- Befehle können gespeichert oder protokolliert werden.
- Warteschlangen und Undo-Funktionen können umgesetzt werden.

## Nachteile

- Für jeden Befehl können zusätzliche Klassen entstehen.
- Die Struktur kann bei sehr vielen Befehlen umfangreich werden.

## Eselsbrücke

**Command = Kommando oder Auftrag.**

Wie bei einer Essensbestellung: Die Bestellung beschreibt den Auftrag, während die Küche ihn ausführt.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Command Patterns?**

Antwort: Einen Befehl als Objekt zu kapseln und dadurch Auftragserteilung und Ausführung voneinander zu trennen.

**Frage 2: Welche Aufgabe hat der Invoker?**

Antwort: Er löst einen Befehl aus, ohne die konkrete Ausführung selbst übernehmen zu müssen.

**Frage 3: Welche Aufgabe hat der Receiver?**

Antwort: Er führt die eigentliche Aktion aus, beispielsweise das Einschalten eines Fernsehers.

**Frage 4: Welche Aufgabe hat das Command-Interface?**

Antwort: Es definiert eine gemeinsame Methode, über die alle konkreten Befehle ausgeführt werden können.

**Frage 5: Wie kann man eine Undo-Funktion umsetzen?**

Antwort: Das Kommando speichert den vorherigen Zustand oder die notwendigen Informationen, um die Aktion rückgängig zu machen.

**Frage 6: Was ist ein typisches Anwendungsbeispiel?**

Antwort: Eine Fernbedienung, ein Menüsystem, eine Warteschlange von Aufgaben oder eine Undo-Funktion in einem Texteditor.

**Frage 7: Was ist der Vorteil gegenüber direkten Methodenaufrufen?**

Antwort: Der Aufrufer muss die konkreten Empfänger und deren Methoden nicht direkt kennen. Befehle können außerdem als Objekte gespeichert und verwaltet werden.

**Merksatz:** Command macht aus einem Befehl ein Objekt.
