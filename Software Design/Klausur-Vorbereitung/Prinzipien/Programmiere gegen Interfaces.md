---
tags: [prinzip]
aliases: [Programmiere gegen ein Interface]
---
# Programmiere gegen ein Interface (Supertyp)

> [!important] Zweites Design Prinzip
> **Programmiere gegen ein Interface (Supertyp) anstatt gegen eine konkrete Implementierung.**

## Problem vorher
- Abhängigkeit von der Implementation in `Ente` oder einer abgeleiteten Klasse
- Flugverhalten nur durch Schreiben von neuem Code änderbar

## Lösung
- Flugverhalten in ein **eigenes Interface** auslagern; `Ente` muss die Implementierung nicht kennen
- **Konkrete Klassen** für jede Art des Flugverhaltens
- Deklarierter Typ ist eine abstrakte Klasse/Interface, die Implementierung wird zugewiesen
- Die Klasse muss nichts über das implementierende Objekt wissen

```java
// Deklarierter Typ = Interface, Implementierung wird zugewiesen
Flugverhalten flugVerhalten = new FlatterFlugverhalten();
```

→ Angewandt im [[FHC02/2. Semester/Software Design/Strategy Pattern]] · Folge: [[Lose Kopplung]] · Vertiefung: [[Dependency Inversion Prinzip]]
