# 1. Grundlagen

## Was ist Software Design?

Software Design ist die Planung einer Software auf technischer Ebene. Dabei wird festgelegt, wie Klassen, Objekte und Komponenten aufgebaut sind und zusammenarbeiten.

### Anforderungen an gutes Software Design

- **Erweiterbarkeit:** Neue Funktionen können einfach ergänzt werden.
- **Wartbarkeit:** Fehler können leichter gefunden und behoben werden.
- **Wiederverwendbarkeit:** Code kann in anderen Bereichen erneut verwendet werden.
- **Testbarkeit:** Einzelne Teile der Software können einfach getestet werden.

## Was ist ein Design Pattern?

Ein Design Pattern (Entwurfsmuster) ist eine bewährte Lösung für ein wiederkehrendes Problem in der Softwareentwicklung.

Ein Pattern ist keine fertige Implementierung, sondern ein Konzept, das beschreibt, wie Klassen und Objekte zusammenarbeiten.

## Die drei Kategorien

| Kategorie | Bedeutung | Eselsbrücke |
|---|---|---|
| Creational Patterns | Erzeugungsmuster: Wie werden Objekte erstellt? | Erzeugen |
| Structural Patterns | Strukturmuster: Wie werden Klassen und Objekte verbunden? | Zusammenbauen |
| Behavioral Patterns | Verhaltensmuster: Wie arbeiten Objekte zusammen? | Zusammenarbeiten |

## Wichtige Designprinzipien

### 1. Trenne veränderliche von unveränderlichen Teilen

Verhalten, das sich häufig ändert, soll möglichst unabhängig vom restlichen Code umgesetzt werden.

**Eselsbrücke:** Was sich oft ändert, bekommt einen eigenen Platz.

### 2. Programmiere gegen ein Interface statt gegen eine konkrete Implementierung

Eine Klasse soll wissen, welche Funktionen ein Objekt anbietet, aber nicht unbedingt, wie diese umgesetzt werden.

**Eselsbrücke:** Ich brauche eine Steckdose, nicht einen bestimmten Hersteller.

### 3. Bevorzuge Komposition gegenüber Vererbung

- Vererbung (`is-a`): Ein Hund ist ein Tier.
- Komposition (`has-a`): Ein Auto hat einen Motor.

Komposition ermöglicht es häufig, Verhalten flexibler auszutauschen.

**Eselsbrücke:** Lieber etwas besitzen als davon abstammen.

### 4. Lose Kopplung

Klassen sollen möglichst wenige direkte Abhängigkeiten voneinander haben.

**Eselsbrücke:** Weniger Abhängigkeiten bedeuten leichteres Austauschen.

### 5. Hohe Kohäsion

Eine Klasse soll eine klar umrissene Verantwortung besitzen.

**Eselsbrücke:** Eine Klasse, eine Hauptaufgabe.

### 6. Open-Closed-Prinzip

Software soll für Erweiterungen offen, aber für Änderungen am bestehenden Code möglichst geschlossen sein.

**Eselsbrücke:** Neues anbauen, ohne das Alte aufzubrechen.

### 7. Dependency Inversion Principle (DIP)

Klassen sollen von Abstraktionen wie Interfaces abhängen und nicht direkt von konkreten Implementierungen.

**Eselsbrücke:** Beide Seiten halten sich an einen gemeinsamen Vertrag.


---

# Alle Design Patterns auf einen Blick

| Design Pattern  | Kategorie  | Hauptaufgabe                         | Eselsbrücke          |
| --------------- | ---------- | ------------------------------------ | -------------------- |
| Strategy        | Behavioral | Algorithmen austauschbar machen      | Strategie wählen     |
| Decorator       | Structural | Objekt dynamisch erweitern           | Extras hinzufügen    |
| Observer        | Behavioral | Beobachter benachrichtigen           | Abo                  |
| Singleton       | Creational | Nur eine Instanz ermöglichen         | Nur einer            |
| Factory         | Creational | Objekterzeugung kapseln              | Fabrik               |
| Command         | Behavioral | Befehl als Objekt kapseln            | Auftrag              |
| Adapter         | Structural | Schnittstellen kompatibel machen     | Übersetzer           |
| Facade          | Structural | Komplexes System vereinfachen        | Ein einfacher Zugang |
| Template Method | Behavioral | Ablauf festlegen, Schritte variieren | Kochrezept           |
| Iterator        | Behavioral | Sammlung nacheinander durchlaufen    | Schritt für Schritt  |

---

# Prüfungsfragen

### 01 · Strategy Pattern

**Frage:** Welches Pattern verwendet man, wenn man unterschiedliche Algorithmen zur Laufzeit austauschen möchte?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Strategy Pattern**

Es ermöglicht, verschiedene Algorithmen auszutauschen, ohne den Code der verwendenden Klasse ändern zu müssen.

</details>

### 02 · Decorator Pattern

**Frage:** Welches Pattern erweitert ein Objekt dynamisch um zusätzliche Funktionalität?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Decorator Pattern**

Es erweitert ein Objekt um zusätzliche Funktionen, ohne die ursprüngliche Klasse direkt verändern zu müssen.

</details>

### 03 · Observer Pattern

**Frage:** Welches Pattern informiert mehrere Objekte automatisch über Änderungen?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Observer Pattern**

Registrierte Beobachter werden benachrichtigt, wenn sich der Zustand des beobachteten Objekts ändert.

</details>

### 04 · Singleton Pattern

**Frage:** Welches Pattern garantiert, dass nur eine Instanz einer Klasse existiert?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Singleton Pattern**

Es stellt sicher, dass eine Klasse nur eine einzige Instanz besitzt und diese zentral zugänglich ist.

</details>

### 05 · Factory Pattern

**Frage:** Welches Pattern kapselt die Erzeugung von Objekten?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Factory Pattern**

Es kapselt die Objekterzeugung, sodass der aufrufende Code nicht alle Details der Erstellung kennen muss.

</details>

### 06 · Command Pattern

**Frage:** Welches Pattern macht einen Befehl zu einem Objekt?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Command Pattern**

Ein Befehl wird als eigenes Objekt gekapselt. Dadurch können Befehle beispielsweise übergeben, gespeichert oder rückgängig gemacht werden.

</details>

### 07 · Adapter Pattern

**Frage:** Welches Pattern verbindet zwei inkompatible Schnittstellen?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Adapter Pattern**

Es passt eine Schnittstelle an eine andere an, damit zwei ansonsten inkompatible Klassen zusammenarbeiten können.

</details>

### 08 · Facade Pattern

**Frage:** Welches Pattern bietet eine vereinfachte Schnittstelle für ein komplexes Subsystem?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Facade Pattern**

Es stellt eine vereinfachte Schnittstelle bereit, über die ein komplexes Subsystem leichter verwendet werden kann.

</details>

### 09 · Template Method Pattern

**Frage:** Welches Pattern legt einen Algorithmus fest, lässt aber einzelne Schritte durch Unterklassen umsetzen?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Template Method Pattern**

Es definiert den grundsätzlichen Ablauf eines Algorithmus. Einzelne Schritte können von Unterklassen konkret implementiert werden.

</details>

### 10 · Iterator Pattern

**Frage:** Welches Pattern ermöglicht es, eine Sammlung zu durchlaufen, ohne ihre interne Struktur zu kennen?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Iterator Pattern**

Es ermöglicht, Elemente einer Sammlung nacheinander zu durchlaufen, ohne die interne Implementierung der Sammlung kennen zu müssen.

</details>

---

# Patterns unterscheiden

### 11 · Adapter vs. Decorator

**Frage:** Welche beiden Patterns werden oft verwechselt, weil beide ein bestehendes Objekt umhüllen können?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Adapter und Decorator**

- **Adapter:** Passt die Schnittstelle an, damit etwas kompatibel wird.
    
- **Decorator:** Erweitert die Funktionalität eines Objekts.
    

**Merksatz:** Adapter = anpassen. Decorator = erweitern.

</details>

### 12 · Strategy vs. Template Method

**Frage:** Welche beiden Patterns werden oft verwechselt, weil beide das Verhalten beeinflussen?

<details>  
<summary>💡 Antwort anzeigen</summary>

**Strategy und Template Method**

- **Strategy:** Verwendet austauschbare Strategieobjekte.
    
- **Template Method:** Definiert einen festen Ablauf mit variablen Schritten.
    

**Merksatz:** Strategy = austauschbar. Template Method = Ablauf vorgegeben.

</details>

### 13 · Factory vs. Singleton

**Frage:** Was ist der Unterschied zwischen Factory und Singleton?

<details>  
<summary>💡 Antwort anzeigen</summary>

- **Factory:** Kapselt die Erzeugung von Objekten.
    
- **Singleton:** Stellt sicher, dass nur eine Instanz einer Klasse existiert.
    

**Merksatz:** Factory = erstellen. Singleton = einmalig.

</details>

### 14 · Facade vs. Adapter

**Frage:** Was ist der Unterschied zwischen Facade und Adapter?

<details>  
<summary>💡 Antwort anzeigen</summary>

- **Facade:** Vereinfacht die Verwendung eines Subsystems.
    
- **Adapter:** Macht eine inkompatible Schnittstelle passend.
    

**Merksatz:** Facade = vereinfachen. Adapter = kompatibel machen.

</details>

---

# Patterns nach Kategorien

### 15 · Erzeugungsmuster

**Frage:** Welche Patterns gehören in diesem Lernzettel zu den Erzeugungsmustern?

<details>  
<summary>💡 Antwort anzeigen</summary>

- Singleton
    
- Factory
    

</details>

### 16 · Strukturmuster

**Frage:** Welche Patterns gehören zu den Strukturmustern?

<details>  
<summary>💡 Antwort anzeigen</summary>

- Decorator
    
- Adapter
    
- Facade
    

</details>

### 17 · Verhaltensmuster

**Frage:** Welche Patterns gehören zu den Verhaltensmustern?

<details>  
<summary>💡 Antwort anzeigen</summary>

- Strategy
    
- Observer
    
- Command
    
- Template Method
    
- Iterator
    

</details>

---

## ⚡ Schnellwiederholung

|Schlüsselwort in der Frage|Gesuchtes Pattern|
|---|---|
|Algorithmen austauschen|Strategy|
|Funktionalität erweitern|Decorator|
|Objekte benachrichtigen|Observer|
|Nur eine Instanz|Singleton|
|Objekte erzeugen|Factory|
|Befehl als Objekt|Command|
|Schnittstellen anpassen|Adapter|
|Komplexes System vereinfachen|Facade|
|Fester Ablauf, variable Schritte|Template Method|
|Sammlung durchlaufen|Iterator|

> [!success] Prüfungs-Merksatz  
> **Strategy tauscht aus, Decorator erweitert, Observer benachrichtigt, Singleton begrenzt, Factory erzeugt, Command kapselt, Adapter passt an, Facade vereinfacht, Template Method gibt den Ablauf vor und Iterator durchläuft.**