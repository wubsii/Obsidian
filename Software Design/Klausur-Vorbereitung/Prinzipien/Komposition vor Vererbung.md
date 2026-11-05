---
tags: [prinzip]
aliases: [Has-A vor Is-A, Komposition über Vererbung]
---
# Bevorzuge Has-A (Komposition) gegenüber Is-A (Vererbung)

> [!important] Prinzip
> Bevorzuge **Has-A (Komposition)** gegenüber **Is-A (Vererbung)**.

**Warum?** → **Flexibilität**: Eine *Familie von Algorithmen* kann **während der Laufzeit** ausgetauscht werden.

Komposition wird oft in Patterns verwendet, z. B. [[FHC02/2. Semester/Software Design/Strategy Pattern]] und [[FHC02/2. Semester/Software Design/Decorator Pattern]].

## Probleme der Vererbungs-Lösungen (Entenbeispiel)
- `fliegen()` in `Ente` ergänzen → auch Gummienten fliegen (nicht lokale Seiteneffekte)
- `fliegen()` für Gummiente überschreiben → duplizierter Code, Laufzeitverhalten nicht änderbar, keine zentrale Übersicht aller Verhalten
- `switch` in `fliegen()` → ebenfalls unelegant

Siehe [[UML Wiederholung]] (Komposition vs. Vererbung) · [[Kapsele was sich ändert]]
