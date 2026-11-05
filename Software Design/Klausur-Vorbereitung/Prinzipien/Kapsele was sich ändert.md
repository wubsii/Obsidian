---
tags: [prinzip]
aliases: [Das Design Prinzip, Veränderliches kapseln]
---
# Kapsele, was sich ändert

> [!important] (Das) Design Prinzip
> **Identifiziere jene Aspekte einer Applikation, welche sich häufig ändern, und trenne diese von jenen, welche gleich bleiben.**

- „Auslagern, was sich ändert“: im Entenbeispiel das *Flugverhalten* (und Quackverhalten) aus der `Ente` herausnehmen
- Das Veränderliche wird zu einer „Familie“ austauschbarer Klassen
- Umgesetzt in: [[FHC02/2. Semester/Software Design/Strategy Pattern]] (Verhalten), [[FHC02/2. Semester/Software Design/Factory Pattern]] (Objekterzeugung)

Siehe auch: [[Programmiere gegen Interfaces]] · [[Komposition vor Vererbung]] · [[00 Übersicht]]
