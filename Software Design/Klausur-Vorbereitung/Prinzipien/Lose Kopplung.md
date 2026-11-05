---
tags: [prinzip]
aliases: [Loose Coupling]
---
# Lose Kopplung

Teilsysteme sind **lose gekoppelt**, wenn ihre **Abhängigkeiten zueinander minimal** sind.

> [!example] Beispiel Ente
> `Ente` kennt nur das Interface `Flugverhalten` (und `Quackverhalten`), nicht deren konkrete Implementierungen. Letztere können ausgetauscht werden, ohne dass `Ente` geändert werden muss.

## Lose Kopplung im [[FHC02/2. Semester/Software Design 1/Patterns/Observer Pattern]]
- Subject weiß über Observer nur, dass ein Interface implementiert wird
- Neue Observer können zur Laufzeit hinzugefügt werden
- Subject muss dafür nicht angefasst werden
- Subjects und Observer unabhängig wiederverwendbar
- Änderung an einem hat keinen Einfluss auf den anderen

Siehe auch: [[Programmiere gegen Interfaces]] · [[Kohärenz]]
