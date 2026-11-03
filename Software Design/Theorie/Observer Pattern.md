**Kategorie:** Verhaltensmuster (Behavioral Pattern)

## Was ist das Observer Pattern?

Das Observer Pattern definiert eine Eins-zu-viele-Abhängigkeit zwischen Objekten.

Wenn sich der Zustand eines Objekts ändert, werden alle registrierten Beobachter automatisch benachrichtigt.

## Welches Problem löst es?

Eine Wetterstation misst die Temperatur. Ein Display und eine Smartphone-App sollen die aktuelle Temperatur anzeigen.

Ohne Observer müsste die Wetterstation jedes Gerät direkt kennen und einzeln aktualisieren.

Mit Observer registrieren sich die Geräte bei der Wetterstation. Bei einer Änderung werden alle registrierten Geräte benachrichtigt.

## Aufbau

- **Subject / Publisher:** Verwaltet die Beobachter und benachrichtigt sie.
- **Observer / Subscriber:** Definiert die gemeinsame Schnittstelle für Beobachter.
- **Concrete Subject:** Das konkrete Objekt, dessen Zustand sich ändert.
- **Concrete Observer:** Reagiert auf Benachrichtigungen.

## Wichtige Methoden

- `registerObserver()` – Beobachter anmelden.
- `removeObserver()` – Beobachter abmelden.
- `notifyObservers()` – Beobachter benachrichtigen.
- `update()` – Benachrichtigung verarbeiten.

## Beispiel aus dem Alltag

Ein Zeitungsverlag veröffentlicht eine neue Ausgabe. Alle Abonnenten, die angemeldet sind, erhalten die neue Ausgabe.

Ein Abonnent kann sich jederzeit abmelden.

## Vorteile

- Mehrere Objekte können automatisch informiert werden.
- Beobachter können zur Laufzeit hinzugefügt oder entfernt werden.
- Subject und Observer sind weniger stark voneinander abhängig.
- Neue Observer können hinzugefügt werden, ohne die zentrale Klasse grundsätzlich zu verändern.

## Nachteile

- Bei vielen Beobachtern kann die Benachrichtigung unübersichtlich werden.
- Die Reihenfolge der Benachrichtigungen ist nicht immer garantiert.
- Nicht abgemeldete Observer können unnötige Benachrichtigungen erhalten.

## Eselsbrücke

**Observer = Beobachter.**

Einer veröffentlicht etwas und alle angemeldeten Beobachter erfahren davon.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Observer Patterns?**

Antwort: Mehrere abhängige Objekte automatisch über Änderungen eines anderen Objekts zu informieren.

**Frage 2: Was bedeutet Eins-zu-viele-Abhängigkeit?**

Antwort: Ein Subject kann mehrere Observer besitzen. Ändert sich das Subject, werden alle registrierten Observer benachrichtigt.

**Frage 3: Welche Aufgabe hat das Subject?**

Antwort: Es verwaltet die Observer und informiert sie über Änderungen.

**Frage 4: Welche Aufgabe hat der Observer?**

Antwort: Er definiert eine gemeinsame Schnittstelle, über die Beobachter Benachrichtigungen empfangen und verarbeiten.

**Frage 5: Wie kann man einen Observer hinzufügen oder entfernen?**

Antwort: Über Methoden wie `registerObserver()` und `removeObserver()`.

**Frage 6: Was bedeutet lose Kopplung beim Observer Pattern?**

Antwort: Das Subject kennt nur die Observer-Schnittstelle und muss nicht wissen, welche konkreten Klassen die Beobachter implementieren.

**Frage 7: Nenne ein Anwendungsbeispiel.**

Antwort: Ein Podcast-Server informiert Notebook, Smartphone und Smartwatch automatisch, wenn ein neuer Podcast verfügbar ist.

**Merksatz:** Ein Objekt ändert sich – alle registrierten Beobachter werden informiert.