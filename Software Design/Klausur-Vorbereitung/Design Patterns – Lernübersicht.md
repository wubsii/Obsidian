
## 1. Factory Pattern (Erzeugungsmuster)

- Muster: Erzeugungsmuster (Creational)
    
- Aufgabe: Erzeugt Objekte, ohne dass der aufrufende Code die konkreten Klassen kennen muss.
    
- Typische Methoden: `create()`, `createProduct()`, `getProduct()`
    
- Konkrete Beispiele:
    
    - Autohersteller erzeugt unterschiedliche Automodelle.
        
    - Nokia Factory erzeugt Boots oder Basisstationen.
        
    - Eine Factory erstellt je nach Auswahl unterschiedliche Benutzer oder Fahrzeuge.
        
    

## 2. Singleton Pattern (Erzeugungsmuster)

- Muster: Erzeugungsmuster (Creational)
    
- Aufgabe: Stellt sicher, dass von einer Klasse nur eine einzige Instanz existiert.
    
- Typische Methoden: `getInstance()`
    
- Typische Besonderheit: `private` Konstruktor.
    
- Konkrete Beispiele:
    
    - Logging / Logger
        
    - Zentrale Konfiguration
        
    - Gemeinsamer Zugriff auf eine zentrale Ressource.
        
    

## 3. Observer Pattern (Verhaltensmuster)

- Muster: Verhaltensmuster (Behavioral)
    
- Aufgabe: Informiert mehrere registrierte Observer automatisch, wenn sich etwas ändert oder ein Ereignis veröffentlicht wird.
    
- Typische Methoden: `register()`, `unregister()`, `notifyObservers()`, `update()`
    
- Konkrete Beispiele:
    
    - Newsletter-Abonnenten erhalten neue Nachrichten.
        
    - Roleplay-Server informiert angemeldete Clients über neue Events.
        
    - YouTube-Abonnenten erhalten Informationen über neue Videos.
        
    

## 4. Strategy Pattern (Verhaltensmuster)

- Muster: Verhaltensmuster (Behavioral)
    
- Aufgabe: Ermöglicht es, verschiedene Algorithmen oder Verhaltensweisen auszutauschen, ohne die verwendende Klasse zu verändern.
    
- Typische Methoden: `execute()`, `calculate()`, `doOperation()`
    
- Konkrete Beispiele:
    
    - Verschiedene Zahlungsarten (PayPal, Kreditkarte, Überweisung).
        
    - Unterschiedliche Berechnungsstrategien.
        
    - Verschiedene Routenberechnungen (Auto, Fahrrad, Fußweg).
        

## 8. Iterator Pattern (Verhaltensmuster)

- Muster: Verhaltensmuster (Behavioral)
    
- Aufgabe: Durchläuft Elemente einer Sammlung, ohne die interne Struktur der Sammlung kennen zu müssen.
    
- Typische Methoden: `hasNext()`, `next()`
    
- Konkrete Beispiele:
    
    - Einkaufstasche mit mehreren Artikeln durchlaufen.
        
    - Liste mit Studenten durchlaufen.
        
    - Alle Produkte eines Warenkorbs anzeigen.
        
    

## 9. Command Pattern (Verhaltensmuster)

- Muster: Verhaltensmuster (Behavioral)
    
- Aufgabe: Kapselt einen Befehl bzw. eine Aktion als eigenes Objekt.
    
- Typische Methoden: `execute()`, optional `undo()`
    
- Konkrete Beispiele:
    
    - Fernbedienung mit ChannelUp- und ChannelDown-Befehlen.
        
    - Rückgängig-Funktion in einem Texteditor.
        
    - Buttons lösen unterschiedliche Aktionen aus.
        
    

## 5. Decorator Pattern (Strukturmuster)

- Muster: Strukturmuster (Structural)
    
- Aufgabe: Erweitert ein bestehendes Objekt flexibel um zusätzliche Funktionen oder Eigenschaften, ohne die ursprüngliche Klasse zu verändern.
    
- Typische Methoden: Methoden der ursprünglichen Klasse, z. B. `getPreis()`, `getBeschreibung()`
    
- Konkrete Beispiele:
    
    - Kaffee mit Milch, Sojamilch oder Sirup.
        
    - Pizza mit zusätzlichen Zutaten.
        
    - Getränke mit unterschiedlichen Erweiterungen.
        
    

## 6. Adapter Pattern (Strukturmuster)

- Muster: Strukturmuster (Structural)
    
- Aufgabe: Passt unterschiedliche bzw. inkompatible Schnittstellen aneinander an, damit Klassen zusammenarbeiten können.
    
- Typische Methoden: z. B. `request()`, `adapt()`
    
- Konkrete Beispiele:
    
    - Steckdosenadapter für unterschiedliche Steckertypen.
        
    - Ein Adapter verbindet ein altes System mit einer neuen Schnittstelle.
        
    - Ein Adapter wandelt Datenformate um.
        
    

## 7. Facade Pattern (Strukturmuster)

- Muster: Strukturmuster (Structural)
    
- Aufgabe: Stellt eine vereinfachte Schnittstelle für ein komplexes System mit mehreren Klassen bereit.
    
- Typische Methoden: z. B. `start()`, `execute()`, `shutdown()`
    
- Konkrete Beispiele:
    
    - Eine Methode startet ein komplettes Heimkinosystem.
        
    - Eine Methode startet mehrere Schritte eines Bestellprozesses.
        
    - Eine zentrale Klasse steuert mehrere Subsysteme.
        
    



## Kategorien auf einen Blick

|Kategorie|Design Patterns|
|---|---|
|Erzeugungsmuster|Factory, Singleton|
|Strukturmuster|Adapter, Decorator, Facade|
|Verhaltensmuster|Observer, Strategy, Iterator, Command|

## Merkhilfe für die Prüfung

|Wenn in der Aufgabenstellung steht ...|Dann denke an ...|
|---|---|
|Objekte erzeugen|Factory|
|Nur eine Instanz|Singleton|
|Mehrere werden benachrichtigt|Observer|
|Algorithmen austauschen|Strategy|
|Zutaten/Funktionen hinzufügen|Decorator|
|Schnittstellen verbinden|Adapter|
|Komplexes System vereinfachen|Facade|
|Sammlung durchlaufen|Iterator|
|Befehl als Objekt|Command|

Besonders wichtig für deine Prüfung: Lerne nicht nur die Namen, sondern vor allem die jeweilige Aufgabe. Dein Lektor fragt gerne nach konkreten Anwendungsszenarien, bei denen du selbst das passende Pattern erkennen musst.