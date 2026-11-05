---
tags: [prinzip, solid]
aliases: [DIP, Dependency Inversion]
---
# Dependency Inversion Principle

> [!important] Kurzfassung
> **Hänge von Abstraktionen und nicht von konkreten Klassen ab.**

**Abhängigkeit:** Klasse A ist abhängig von Klasse B, wenn eine Änderung in B zur Folge hat, dass auch A sich ändern muss.

## Im Pizzarestaurant ([[FHC02/2. Semester/Software Design/Factory Pattern]])
- `PizzaStore` ist abhängig von `Pizza`
- `Pizza` ist abhängig von konkreten Pizzen
- → Die Factory entkoppelt: Der Store arbeitet nur mit dem Interface `Pizza`

Siehe auch: [[Programmiere gegen Interfaces]] · [[Lose Kopplung]]
