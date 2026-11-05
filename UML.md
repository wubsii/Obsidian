Ah, stimmt! 😊 Du musst nur diese 10 Design Patterns lernen. Hier sind sie jeweils als eigenes Mermaid-UML-Diagramm für Obsidian.

# 1. Singleton – Erzeugungsmuster

```mermaid
classDiagram
    class Singleton {
        -static Singleton instanz
        -Singleton()
        +static getInstance() Singleton
    }
```

# 2. Factory Method – Erzeugungsmuster

``` mermaid
classDiagram
    class Produkt {
        <<interface>>
        +verwenden()
    }

    class ProduktA {
        +verwenden()
    }

    class ProduktB {
        +verwenden()
    }

    class Factory {
        <<abstract>>
        +createProdukt() Produkt
    }

    class FactoryA {
        +createProdukt() Produkt
    }

    class FactoryB {
        +createProdukt() Produkt
    }

    Produkt <|.. ProduktA
    Produkt <|.. ProduktB
    Factory <|-- FactoryA
    Factory <|-- FactoryB
    FactoryA ..> ProduktA : erzeugt
    FactoryB ..> ProduktB : erzeugt
```

# 3. Adapter – Strukturmuster

```mermaid
classDiagram
    class ZielSchnittstelle {
        <<interface>>
        +anfrage()
    }

    class Adapter {
        -alterDienst AlterDienst
        +anfrage()
    }

    class AlterDienst {
        +spezielleAnfrage()
    }

    ZielSchnittstelle <|.. Adapter
    Adapter --> AlterDienst : verwendet
```

# 4. Decorator – Strukturmuster

```mermaid
classDiagram
    class Komponente {
        <<interface>>
        +ausfuehren()
    }

    class BasisKomponente {
        +ausfuehren()
    }

    class Decorator {
        <<abstract>>
        #komponente Komponente
        +ausfuehren()
    }

    class ZusatzDecorator {
        +ausfuehren()
    }

    Komponente <|.. BasisKomponente
    Komponente <|.. Decorator
    Decorator <|-- ZusatzDecorator
    Decorator o-- Komponente : umhüllt
```
# 5. Facade – Strukturmuster

```mermaid
classDiagram
    class Facade {
        -systemA SystemA
        -systemB SystemB
        +starteSystem()
    }

    class SystemA {
        +start()
    }

    class SystemB {
        +start()
    }

    class Client {
        +ausfuehren()
    }

    Client --> Facade
    Facade --> SystemA
    Facade --> SystemB
```
# 6. Observer – Verhaltensmuster

```mermaid
classDiagram
    class Subject {
        <<interface>>
        +registrieren(Observer)
        +entfernen(Observer)
        +benachrichtigen()
    }

    class KonkretesSubject {
        -beobachter Liste
        +registrieren(Observer)
        +entfernen(Observer)
        +benachrichtigen()
    }

    class Observer {
        <<interface>>
        +update()
    }

    class KonkreterObserver {
        +update()
    }

    Subject <|.. KonkretesSubject
    Observer <|.. KonkreterObserver
    KonkretesSubject o-- Observer : benachrichtigt
```

# 7. Strategy – Verhaltensmuster

```mermaid

classDiagram
    class Strategie {
        <<interface>>
        +berechnen()
    }

    class StrategieA {
        +berechnen()
    }

    class StrategieB {
        +berechnen()
    }

    class Kontext {
        -strategie Strategie
        +strategieSetzen(Strategie)
        +ausfuehren()
    }

    Strategie <|.. StrategieA
    Strategie <|.. StrategieB
    Kontext --> Strategie : verwendet
```

# 8. Command – Verhaltensmuster

```mermaid
classDiagram
    class Kommando {
        <<interface>>
        +execute()
    }

    class LichtEinschalten {
        -licht Licht
        +execute()
    }

    class Licht {
        +einschalten()
        +ausschalten()
    }

    class Fernbedienung {
        -kommando Kommando
        +tasteDruecken()
    }

    Kommando <|.. LichtEinschalten
    LichtEinschalten --> Licht : Receiver
    Fernbedienung --> Kommando : Invoker
```

# 9. Template Method – Verhaltensmuster

```mermaid
classDiagram
    class Vorlage {
        <<abstract>>
        +templateMethod()
        #schrittA()
        #schrittB()
    }

    class KonkreteVorlageA {
        +schrittA()
        +schrittB()
    }

    class KonkreteVorlageB {
        +schrittA()
        +schrittB()
    }

    Vorlage <|-- KonkreteVorlageA
    Vorlage <|-- KonkreteVorlageB
```

# 10. Iterator – Verhaltensmuster

```mermaid
classDiagram
    class Iterator {
        <<interface>>
        +hasNext() boolean
        +next() Element
    }

    class KonkreterIterator {
        -position
        -sammlung Sammlung
        +hasNext() boolean
        +next() Element
    }

    class Sammlung {
        <<interface>>
        +createIterator() Iterator
    }

    class KonkreteSammlung {
        -elemente Liste
        +createIterator() Iterator
    }

    Iterator <|.. KonkreterIterator
    Sammlung <|.. KonkreteSammlung
    KonkreteSammlung --> KonkreterIterator : erstellt
    KonkreterIterator --> KonkreteSammlung : durchläuft
    ``

## Übersicht zum Lernen

|Pattern|Kategorie|Wichtigste UML-Erkennung|
|---|---|---|
|Singleton|Erzeugung|Private Konstruktor, statische Instanz|
|Factory Method|Erzeugung|Factory erzeugt Produkte|
|Adapter|Struktur|Adapter verbindet Schnittstellen|
|Decorator|Struktur|Decorator enthält Komponente|
|Facade|Struktur|Facade greift auf Subsysteme zu|
|Observer|Verhalten|Subject benachrichtigt Observer|
|Strategy|Verhalten|Kontext verwendet Strategie|
|Command|Verhalten|Invoker → Command → Receiver|
|Template Method|Verhalten|Oberklasse und Unterklassen|
|Iterator|Verhalten|`hasNext()` und `next()`|

Tipp für die Prüfung: Achte besonders auf die Pfeile und Beziehungen. Oft erkennt man das richtige Pattern schon daran, welche Klasse ein Interface implementiert oder welche Klasse eine andere enthält.