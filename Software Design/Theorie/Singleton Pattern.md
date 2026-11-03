**Kategorie:** Erzeugungsmuster (Creational Pattern)

## Was ist das Singleton Pattern?

Das Singleton Pattern stellt sicher, dass von einer Klasse nur eine einzige Instanz existiert und ein zentraler Zugriffspunkt auf diese Instanz verfügbar ist.

## Welches Problem löst es?

Manche Objekte sollen nur einmal vorhanden sein, beispielsweise eine zentrale Konfiguration oder ein zentraler Logger.

Ohne Singleton könnten an verschiedenen Stellen mehrere Instanzen derselben Klasse erzeugt werden.

## Aufbau

- **Private statische Instanz:** Speichert die einzige Instanz.
- **Privater Konstruktor:** Verhindert die normale Erzeugung von außen.
- **Öffentliche statische Methode:** Gibt die Instanz zurück.

## Beispiel in Java

```java
class Einstellungen {
    private static Einstellungen instanz;

    private Einstellungen() {
    }

    public static Einstellungen getInstance() {
        if (instanz == null) {
            instanz = new Einstellungen();
        }

        return instanz;
    }
}
```

Verwendung:

```java
Einstellungen e1 = Einstellungen.getInstance();
Einstellungen e2 = Einstellungen.getInstance();

System.out.println(e1 == e2); // true
```

Beide Variablen verweisen auf dieselbe Instanz.

**Hinweis:** Diese einfache Implementierung ist nicht threadsicher. In mehrthreadigen Programmen muss die Instanzerzeugung entsprechend abgesichert werden.

## Vorteile

- Es existiert nur eine Instanz.
- Ein zentraler Zugriffspunkt ist vorhanden.
- Gemeinsame Einstellungen können zentral verwaltet werden.

## Nachteile

- Starke globale Abhängigkeiten können entstehen.
- Unit-Tests können schwieriger werden.
- Gemeinsamer veränderlicher Zustand kann Probleme verursachen.
- Die einfache Implementierung ist nicht automatisch threadsicher.

## Eselsbrücke

**Singleton = Single = einer.**

Es gibt nur einen Schlüssel für einen zentralen Raum: Alle verwenden denselben Zugang.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Singleton Patterns?**

Antwort: Sicherzustellen, dass eine Klasse nur eine Instanz besitzt und diese zentral zugänglich ist.

**Frage 2: Warum ist der Konstruktor privat?**

Antwort: Damit andere Klassen die Instanz nicht direkt mit `new` erzeugen können.

**Frage 3: Warum ist die Instanz statisch?**

Antwort: Damit die Instanz zur Klasse gehört und über eine statische Methode zugänglich ist.

**Frage 4: Warum wird `getInstance()` verwendet?**

Antwort: Die Methode gibt die einzige Instanz zurück und erzeugt sie bei Bedarf.

**Frage 5: Was ist der Unterschied zwischen einer Klasse und einer Instanz?**

Antwort: Die Klasse ist der Bauplan. Die Instanz ist das konkrete Objekt, das anhand dieses Bauplans erzeugt wurde.

**Frage 6: Nenne typische Anwendungsfälle.**

Antwort: Zentrale Einstellungen, Logging, Caches oder bestimmte gemeinsam genutzte Ressourcen.

**Merksatz:** Singleton garantiert eine Instanz und einen zentralen Zugriffspunkt.
