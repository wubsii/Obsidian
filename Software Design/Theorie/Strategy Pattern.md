**Kategorie:** Verhaltensmuster (Behavioral Pattern)

## Was ist das Strategy Pattern?

Das Strategy Pattern kapselt eine Familie von Algorithmen und macht sie austauschbar. Die Klasse, welche die Strategie verwendet, muss nicht wissen, wie der Algorithmus intern funktioniert.

## Welches Problem löst es?

Wenn sich ein Verhalten auf verschiedene Arten ausführen lässt, könnte man viele `if`- oder `switch`-Abfragen verwenden.

Dadurch wird der Code oft unübersichtlich.

Beim Strategy Pattern wird jede Variante in eine eigene Klasse ausgelagert.

## Aufbau

- **Strategy:** Gemeinsames Interface für alle Strategien.
- **Concrete Strategy:** Implementiert eine bestimmte Variante.
- **Context:** Verwendet eine Strategie und kann sie austauschen.
- **Client:** Wählt die gewünschte Strategie aus.

## Beispiel

Ein Unternehmen berechnet Provisionen auf zwei Arten:

- 10 % des Gewinns
- 5 % des Umsatzes

```java
interface ProvisionsStrategie {
    double berechne(double umsatz, double gewinn);
}

class GewinnStrategie implements ProvisionsStrategie {
    public double berechne(double umsatz, double gewinn) {
        return gewinn * 0.10;
    }
}

class UmsatzStrategie implements ProvisionsStrategie {
    public double berechne(double umsatz, double gewinn) {
        return umsatz * 0.05;
    }
}
```

Der Manager kann die Strategie austauschen:

```java
class MitarbeiterManager {
    private ProvisionsStrategie strategie;

    public void setStrategie(ProvisionsStrategie strategie) {
        this.strategie = strategie;
    }

    public double berechneProvision(double umsatz, double gewinn) {
        return strategie.berechne(umsatz, gewinn);
    }
}
```

Verwendung:

```java
MitarbeiterManager manager = new MitarbeiterManager();

manager.setStrategie(new GewinnStrategie());
System.out.println(manager.berechneProvision(10000, 2000));
// 200.0

manager.setStrategie(new UmsatzStrategie());
System.out.println(manager.berechneProvision(10000, 2000));
// 500.0
```

## Vorteile

- Strategien können während der Laufzeit ausgetauscht werden.
- Neue Varianten können ergänzt werden.
- Weniger `if`- und `switch`-Abfragen.
- Die Implementierungen sind voneinander getrennt.

## Nachteile

- Es entstehen zusätzliche Klassen und Interfaces.
- Für sehr einfache Verhaltensweisen kann das Pattern unnötig kompliziert sein.

## Eselsbrücke

**Strategy = Strategie auswählen.**

Wie bei einem Navigationsgerät: schnellste, kürzeste oder mautfreie Route. Das Ziel bleibt gleich, aber die Strategie ändert sich.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Strategy Patterns?**

Antwort: Es kapselt verschiedene Algorithmen und ermöglicht, diese unabhängig von der verwendenden Klasse auszutauschen.

**Frage 2: Warum verwendet man ein Interface?**

Antwort: Alle Strategien bieten dieselbe Schnittstelle an. Dadurch kann der Context verschiedene Strategien verwenden, ohne deren konkrete Implementierung kennen zu müssen.

**Frage 3: Was ist der Unterschied zwischen Strategy und Vererbung?**

Antwort: Beim Strategy Pattern wird das Verhalten in separate Objekte ausgelagert. Es kann dadurch flexibler ausgetauscht werden, anstatt fest in einer Vererbungshierarchie verankert zu sein.

**Frage 4: Was bedeutet Komposition beim Strategy Pattern?**

Antwort: Der Context besitzt eine Strategie (`has-a`) und verwendet diese. Die Strategie kann durch eine andere Implementierung ersetzt werden.

**Frage 5: Welches Problem entsteht bei vielen `if`-Abfragen für unterschiedliche Algorithmen?**

Antwort: Der Code wird unübersichtlich und Änderungen können mehrere Stellen betreffen. Strategy trennt die Varianten in eigene Klassen.

**Frage 6: Nenne ein Anwendungsbeispiel.**

Antwort: Unterschiedliche Zahlungsarten wie Kreditkarte, PayPal und Überweisung können als austauschbare Strategien umgesetzt werden.

**Merksatz:** Strategy kapselt Algorithmen und macht sie austauschbar.
