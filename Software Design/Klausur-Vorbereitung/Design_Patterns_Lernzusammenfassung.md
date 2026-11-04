# Design Patterns -- Lernzusammenfassung

Diese Zusammenfassung enthält die zehn Design Patterns aus unserer
Lernrunde. Zu jedem Pattern findest du die Kategorie, die Hauptaufgabe,
Erkennungsmerkmale, ein Java-/Alltagsbeispiel und einen Merksatz.

## 1. Erzeugungsmuster (Creational Patterns)

Erzeugungsmuster beschäftigen sich damit, **wie Objekte erstellt
werden**.

### Factory Pattern

**Aufgabe:** Kapselt die Erzeugung von Objekten. Eine Factory
entscheidet, welches konkrete Objekt erstellt wird.

**Woran erkenne ich es?** - Es sollen unterschiedliche Objekttypen
erstellt werden. - Eine zentrale Klasse übernimmt die
Objekterstellung. - Der aufrufende Code soll nicht selbst entscheiden
müssen, welche konkrete Klasse mit `new` erstellt wird.

**Beispiel:** Ein Programm kann unterschiedliche Fahrzeuge erstellen:
`Auto`, `Motorrad` oder `LKW`. Eine `FahrzeugFactory` entscheidet anhand
einer Eingabe, welches Objekt erzeugt wird.

**Weitere Anwendungen:** Exportfunktionen (PDF, CSV, Excel),
Zahlungsanbieter, Datenbankverbindungen und Parser.

**Merksatz:** Factory = Objekte erstellen.

### Singleton Pattern

**Aufgabe:** Stellt sicher, dass von einer Klasse nur eine einzige
Instanz existiert und einen zentralen Zugriff darauf bereit.

**Woran erkenne ich es?** - Es soll nur eine Instanz der Klasse geben. -
Mehrere Klassen sollen dieselbe Instanz verwenden. - Der Konstruktor ist
meistens `private`. - Eine statische Methode wie `getInstance()` liefert
die Instanz zurück.

**Beispiel:** Ein zentraler Logger, den verschiedene Programmteile
verwenden, um Meldungen zu protokollieren.

**Weitere Anwendungen:** Zentrale Konfiguration, Logger und gemeinsam
genutzte Ressourcen.

**Merksatz:** Singleton = Nur eine Instanz.

## 2. Strukturmuster (Structural Patterns)

Strukturmuster beschäftigen sich damit, **wie Klassen und Objekte
zusammengesetzt und miteinander verbunden werden**.

### Adapter Pattern

**Aufgabe:** Passt eine Schnittstelle an eine andere an, damit zwei
ansonsten inkompatible Systeme zusammenarbeiten können.

**Woran erkenne ich es?** - Zwei Systeme besitzen unterschiedliche
Schnittstellen. - Ein bestehendes System soll weiterverwendet werden. -
Der bestehende Code soll möglichst nicht verändert werden. - Eine
Adapterklasse übersetzt die Aufrufe.

**Beispiel:** Ein altes Zahlungssystem besitzt `bezahleBetrag(betrag)`,
während das neue System `pay(amount)` erwartet. Ein Adapter verbindet
die beiden Schnittstellen.

**Weitere Anwendungen:** Alte und neue Softwaresysteme verbinden,
externe APIs integrieren und Bibliotheken mit inkompatiblen
Schnittstellen verwenden.

**Merksatz:** Adapter = Schnittstellen anpassen.

### Decorator Pattern

**Aufgabe:** Erweitert ein Objekt flexibel um zusätzliche Funktionen
oder Eigenschaften, ohne die ursprüngliche Klasse verändern zu müssen.

**Woran erkenne ich es?** - Ein Objekt soll zusätzliche Funktionen oder
Eigenschaften erhalten. - Erweiterungen sollen flexibel kombinierbar
sein. - Die ursprüngliche Klasse soll unverändert bleiben. - Ein
Decorator umhüllt ein anderes Objekt derselben Schnittstelle.

**Beispiel:** Ein Kaffee kann nachträglich mit Milch, Sojamilch oder
Sirup erweitert werden. Die Zutaten werden als Decorator hinzugefügt und
können kombiniert werden.

**Weitere Anwendungen:** Java-I/O-Streams, Verschlüsselung und
Komprimierung sowie zusätzliche Funktionen in Textverarbeitungs- oder
Bestellsystemen.

**Merksatz:** Decorator = Objekte erweitern.

### Facade Pattern

**Aufgabe:** Bietet eine einfache Schnittstelle für ein komplexes
System. Die Facade koordiniert mehrere Klassen im Hintergrund.

**Woran erkenne ich es?** - Viele Klassen oder Komponenten müssen
zusammenarbeiten. - Der Benutzer soll nur einen einfachen Methodenaufruf
benötigen. - Die Komplexität soll hinter einer gemeinsamen Schnittstelle
verborgen werden.

**Beispiel:** Bei einer Heimkinoanlage schaltet `filmStarten()`
Fernseher, Soundsystem und Player ein und wählt den richtigen Eingang.

**Weitere Anwendungen:** Smart-Home-Systeme, Buchungssysteme und
komplexe Bibliotheken.

**Merksatz:** Facade = Komplexität vereinfachen.

## 3. Verhaltensmuster (Behavioral Patterns)

Verhaltensmuster beschäftigen sich damit, **wie Objekte kommunizieren
und wie Verhalten organisiert wird**.

### Observer Pattern

**Aufgabe:** Benachrichtigt mehrere registrierte Beobachter automatisch,
wenn sich bei einem beobachteten Objekt etwas ändert.

**Woran erkenne ich es?** - Mehrere Teilnehmer sollen über Änderungen
informiert werden. - Beobachter können sich registrieren und
gegebenenfalls wieder abmelden. - Bei einer Änderung werden die
registrierten Observer benachrichtigt. - Häufig gibt es Methoden wie
`subscribe()`, `publish()` oder `update()`.

**Beispiel:** Bei einem Newsletter registrieren sich Abonnenten. Wird
ein neuer Beitrag veröffentlicht, werden alle registrierten Abonnenten
benachrichtigt.

**Weitere Anwendungen:** Wetter-Apps, Benachrichtigungssysteme und
Ereignisbehandlung in Benutzeroberflächen.

**Merksatz:** Observer = Änderungen mitteilen.

### Strategy Pattern

**Aufgabe:** Kapselt verschiedene Algorithmen oder Verhaltensweisen und
macht sie austauschbar. Die verwendende Klasse muss dafür nicht
umgeschrieben werden.

**Woran erkenne ich es?** - Es gibt mehrere Möglichkeiten, eine Aufgabe
auszuführen. - Das Verhalten soll zur Laufzeit austauschbar sein. - Jede
Variante wird in einer eigenen Strategie umgesetzt.

**Beispiel:** Ein Online-Shop bietet verschiedene Zahlungsstrategien:
PayPal, Kreditkarte oder Sofortüberweisung. Der Shop verwendet die
ausgewählte Strategie.

**Weitere Anwendungen:** Rabattberechnungen, Sortieralgorithmen und
Routenberechnungen.

**Merksatz:** Strategy = Verhalten austauschen.

### Iterator Pattern

**Aufgabe:** Ermöglicht es, eine Sammlung von Elementen nacheinander zu
durchlaufen, ohne ihre interne Struktur kennen zu müssen.

**Woran erkenne ich es?** - Eine Liste oder Sammlung soll durchlaufen
werden. - Elemente werden einzeln und nacheinander ausgelesen. -
Typische Methoden sind `hasNext()` und `next()`.

**Java-Beispiel:**

``` java
Iterator<String> iterator = namen.iterator();

while (iterator.hasNext()) {
    String name = iterator.next();
    System.out.println(name);
}
```

-   `hasNext()` prüft, ob noch ein Element vorhanden ist.
-   `next()` liefert das nächste Element.

**Weitere Anwendungen:** ArrayLists, Einkaufsliste durchlaufen und
Datenbankergebnisse auslesen.

**Merksatz:** Iterator = Elemente nacheinander durchlaufen.

### Command Pattern

**Aufgabe:** Kapselt einen Befehl bzw. eine Aktion als eigenes Objekt.
Dadurch können Befehle beispielsweise gespeichert, weitergegeben oder
rückgängig gemacht werden.

**Woran erkenne ich es?** - Aktionen werden als eigene Objekte
dargestellt. - Häufig gibt es eine gemeinsame Methode wie `execute()`. -
Ein Aufrufer (Invoker) löst den Befehl aus, ohne die konkrete Ausführung
kennen zu müssen. - Befehle können beispielsweise für Undo-Funktionen
gespeichert werden.

**Beispiel:** Bei einer Fernbedienung ist jeder Knopf mit einem eigenen
Command-Objekt verbunden, etwa `LichtEinschaltenCommand` oder
`LauterCommand`.

**Weitere Anwendungen:** Texteditoren mit Rückgängig-Funktion,
Menüaktionen und Aufgabenwarteschlangen.

**Merksatz:** Command = Aktionen als Objekte verpacken.

### Template Method Pattern

**Aufgabe:** Definiert den festen Ablauf eines Algorithmus in einer
Oberklasse. Einzelne Schritte werden von Unterklassen unterschiedlich
umgesetzt.

**Woran erkenne ich es?** - Der grundsätzliche Ablauf bleibt immer
gleich. - Einzelne Schritte unterscheiden sich je nach Variante. - Eine
abstrakte Oberklasse legt die Reihenfolge fest. - Unterklassen
implementieren die variablen Schritte.

**Beispiel:** Ein Exportprozess besteht immer aus Daten vorbereiten,
Daten formatieren und Datei speichern. Die Formatierung unterscheidet
sich für PDF und CSV. Die abstrakte Oberklasse definiert den Ablauf;
Unterklassen implementieren die jeweilige Formatierung.

**Weitere Anwendungen:** Dateiverarbeitung, Import- und Exportprozesse
sowie standardisierte Datenverarbeitung.

**Merksatz:** Template Method = Ablauf bleibt gleich, einzelne Schritte
variieren.

## 4. Kategorien im Überblick

  -----------------------------------------------------------------------
  Kategorie                           Design Patterns
  ----------------------------------- -----------------------------------
  Erzeugungsmuster (Creational)       Factory, Singleton

  Strukturmuster (Structural)         Adapter, Decorator, Facade

  Verhaltensmuster (Behavioral)       Observer, Strategy, Iterator,
                                      Command, Template Method
  -----------------------------------------------------------------------

## 5. Häufige Verwechslungen

### Factory oder Decorator?

-   **Factory:** Erstellt ein passendes Objekt.
-   **Decorator:** Erweitert ein bereits vorhandenes Objekt.

### Facade oder Factory?

-   **Facade:** Vereinfacht den Zugriff auf mehrere Komponenten.
-   **Factory:** Übernimmt die Erstellung konkreter Objekte.

### Adapter oder Facade?

-   **Adapter:** Passt eine inkompatible Schnittstelle an.
-   **Facade:** Bietet eine einfachere Schnittstelle für ein komplexes
    System.

### Command oder Strategy?

-   **Command:** Verpackt eine Aktion als Objekt.
-   **Strategy:** Verpackt eine austauschbare Vorgehensweise bzw. einen
    Algorithmus.

### Iterator oder Observer?

-   **Iterator:** Geht Elemente einer Sammlung nacheinander durch.
-   **Observer:** Informiert registrierte Beobachter über Änderungen.

### Template Method oder Strategy?

-   **Template Method:** Die Oberklasse legt den Ablauf fest;
    Unterklassen variieren einzelne Schritte.
-   **Strategy:** Ein Verhalten bzw. Algorithmus wird durch eine
    austauschbare Strategie bereitgestellt.

## 6. Gründe für die Verwendung von Design Patterns

Design Patterns können unter anderem folgende Vorteile bringen:

-   **Erweiterbarkeit:** Neue Funktionen oder Varianten lassen sich
    leichter hinzufügen.
-   **Wartbarkeit:** Der Code ist klarer strukturiert und leichter zu
    ändern.
-   **Wiederverwendbarkeit:** Bewährte Lösungen können in mehreren
    Projekten eingesetzt werden.
-   **Testbarkeit:** Einzelne Bestandteile lassen sich oft einfacher
    getrennt testen.

## 7. Kurzer Prüfungsleitfaden

Achte bei einer Aufgabenstellung auf diese Hinweise:

  Hinweis in der Aufgabe                                Mögliches Pattern
  ----------------------------------------------------- -------------------
  Nur eine Instanz, zentraler Zugriff                   Singleton
  Objekt abhängig von einer Eingabe erzeugen            Factory
  Unterschiedliche Schnittstellen verbinden             Adapter
  Objekt flexibel um Funktionen erweitern               Decorator
  Komplexes System mit einem Aufruf bedienen            Facade
  Mehrere Teilnehmer automatisch benachrichtigen        Observer
  Zwischen Algorithmen oder Verhaltensweisen wechseln   Strategy
  Sammlung Element für Element durchlaufen              Iterator
  Aktion als Objekt, `execute()`, Undo                  Command
  Fester Ablauf, variable Schritte in Unterklassen      Template Method

**Lerntipp:** Versuche bei jeder Prüfungsaufgabe zuerst herauszufinden,
welches Problem gelöst werden soll: Objekte erstellen, Klassen
verbinden, Komplexität vereinfachen, Änderungen mitteilen, Verhalten
austauschen oder Elemente durchlaufen.
