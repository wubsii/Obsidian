
## Was ist ein Design Pattern?

Ein **Design Pattern (Entwurfsmuster)** ist eine bewährte Lösung für ein häufiges Problem beim Entwurf von Software. Es ist keine fertige Implementierung, sondern eine wiederverwendbare Vorlage.

## 1. Strategy Pattern
Das Strategy Pattern kapselt verschiedene Algorithmen oder Verhaltensweisen in getrennten Klassen.  
Alle Strategien besitzen eine gemeinsame Schnittstelle.  
Dadurch kann das Programm zwischen verschiedenen Strategien wechseln, ohne den aufrufenden Code stark zu verändern.  
Die konkrete Strategie kann häufig zur Laufzeit ausgewählt werden.  
Beispiel: Ein Navigationsprogramm kann zwischen dem schnellsten, kürzesten oder verkehrsärmsten Weg wechseln.

## 2. Decorator Pattern
Das Decorator Pattern erweitert ein Objekt um zusätzliche Funktionen, ohne seine ursprüngliche Klasse zu verändern.  
Ein Decorator umhüllt das ursprüngliche Objekt und besitzt dabei dieselbe gemeinsame Schnittstelle.  
Er ruft das umhüllte Objekt auf und ergänzt dessen Verhalten.  
Mehrere Decorators können miteinander kombiniert werden.  
Beispiel: Ein Kaffee kann mit Milch, Sirup und Schaum erweitert werden, wobei sich die Preise addieren.

## 3. Observer Pattern
Das Observer Pattern ermöglicht es, mehrere Objekte über Änderungen eines anderen Objekts zu informieren.  
Das Objekt, das Änderungen meldet, wird häufig als Subject bezeichnet.  
Die interessierten Objekte heißen Observer und können sich anmelden oder abmelden.  
Bei einer Änderung benachrichtigt das Subject die angemeldeten Observer.  
Beispiel: Mehrere Nutzer erhalten eine Benachrichtigung, wenn ein neuer Beitrag veröffentlicht wird.

## 4. Singleton Pattern
Das Singleton Pattern stellt sicher, dass von einer Klasse nur eine Instanz existiert.  
Es bietet außerdem einen zentralen Zugriff auf diese Instanz.  
Der Konstruktor wird üblicherweise so eingeschränkt, dass nicht beliebig neue Instanzen erzeugt werden können.  
Das Pattern kann sinnvoll sein, wenn eine zentrale gemeinsame Instanz benötigt wird.  
Beispiel: Eine Anwendung verwendet eine zentrale Konfiguration.

## 5. Factory Method Pattern
Das Factory Method Pattern kapselt die Erzeugung von Objekten in einer speziellen Methode.  
Der aufrufende Code muss dadurch nicht immer selbst die konkrete Klasse instanziieren.  
Unterklassen können festlegen, welche konkrete Objektart erzeugt wird.  
So wird die Objekterzeugung vom restlichen Programmcode entkoppelt.  
Beispiel: Eine Anwendung erstellt je nach Bedarf unterschiedliche Dokumenttypen.

## 6. Command Pattern
Das Command Pattern kapselt eine Aktion als eigenes Objekt.  
Ein Command enthält die Informationen, die zum Ausführen einer bestimmten Aktion benötigt werden.  
Ein Aufrufer kann den Befehl ausführen, ohne genau zu wissen, wie die Aktion intern umgesetzt wird.  
Befehle können dadurch beispielsweise gespeichert, in eine Warteschlange gelegt oder rückgängig gemacht werden, wenn dies implementiert ist.  
Beispiel: Eine Fernbedienung verwendet eigene Befehlsobjekte zum Ein- und Ausschalten eines Fernsehers.

## 7. Adapter Pattern
Das Adapter Pattern verbindet Klassen oder Systeme, deren Schnittstellen nicht zueinander passen.  
Der Adapter übersetzt die Aufrufe der erwarteten Schnittstelle in Aufrufe, die das vorhandene System versteht.  
Dadurch muss der bestehende Code nicht unbedingt verändert werden.  
Der Adapter ermöglicht es, zusammenarbeitende Komponenten trotz unterschiedlicher Schnittstellen zu verwenden.  
Beispiel: Ein Adapter verbindet ein Gerät mit einem Anschluss, der sonst nicht passen würde.

## 8. Facade Pattern
Das Facade Pattern bietet eine einfache Schnittstelle zu einem komplexen Subsystem.  
Die Facade bündelt mehrere interne Schritte hinter wenigen leicht verständlichen Methoden.  
Der aufrufende Code muss die einzelnen Komponenten und ihre Abläufe nicht kennen.  
Das reduziert die Komplexität an der Stelle, an der das Subsystem verwendet wird.  
Beispiel: Eine Methode „FilmStarten“ schaltet Fernseher, Soundanlage und Streaminggerät ein.

## 9. Template Method Pattern
Das Template Method Pattern legt den Grundablauf eines Algorithmus in einer Basisklasse fest.  
Einzelne Schritte des Ablaufs können von Unterklassen unterschiedlich umgesetzt werden.  
Die Reihenfolge der grundlegenden Schritte bleibt dabei vorgegeben.  
So können gemeinsame Abläufe wiederverwendet werden, während bestimmte Details variieren.  
Beispiel: Verschiedene Getränke werden nach demselben Grundablauf zubereitet, aber einzelne Schritte unterscheiden sich.

## 10. Iterator Pattern
Das Iterator Pattern ermöglicht es, Elemente einer Sammlung nacheinander zu durchlaufen.  
Der Code, der die Elemente verarbeitet, muss die interne Struktur der Sammlung nicht kennen.  
Der Iterator stellt typischerweise Funktionen bereit, um das nächste Element abzurufen und festzustellen, ob weitere Elemente vorhanden sind.  
Dadurch kann eine Sammlung einheitlich durchlaufen werden.  
Beispiel: Eine Liste von Studierenden wird der Reihe nach ausgegeben.

## Besonders wichtige Unterschiede


- **Strategy vs. Decorator:** Strategy tauscht ein Verhalten bzw. einen Algorithmus aus. Decorator ergänzt ein Objekt um zusätzliche Funktionen.

- **Decorator vs. Vererbung:** Decorator erlaubt flexible Kombinationen zur Laufzeit und vermeidet viele Unterklassen für jede Kombination.

- **Factory Method vs. Decorator:** Factory Method kümmert sich um die Erzeugung von Objekten; Decorator erweitert ein bestehendes Objekt.

- **Adapter vs. Facade:** Adapter macht inkompatible Schnittstellen kompatibel; Facade vereinfacht den Zugriff auf ein komplexes System.

- **Command vs. Strategy:** Command kapselt eine Aktion als Objekt; Strategy kapselt eine austauschbare Vorgehensweise bzw. einen Algorithmus.

- **Observer vs. Strategy:** Observer verteilt Benachrichtigungen bei Änderungen; Strategy wählt aus verschiedenen Verhaltensweisen.

  

## Typische Hinweise in Prüfungsfragen

  

- „Verhalten/Algorithmus austauschen“ → **Strategy**

- „Zusätze kombinieren, Kosten addieren, dynamisch erweitern“ → **Decorator**

- „Bei Änderung mehrere Objekte benachrichtigen“ → **Observer**

- „Nur eine Instanz“ → **Singleton**

- „Objekte abhängig von Typ/Bedarf erzeugen“ → **Factory Method**

- „Aktion rückgängig machen (Undo/Redo)“ → **Command**

- „Zwei inkompatible Schnittstellen verbinden“ → **Adapter**

- „Komplexes System über einfache Schnittstelle bedienen“ → **Facade**

- „Fester Ablauf mit anpassbaren Einzelschritten“ → **Template Method**

- „Elemente nacheinander durchlaufen“ → **Iterator**

  

## Beispiel: Getränkeautomat

  

Ein Kaffee kann mit Milch, Sirup und Schaum erweitert werden. Die Kosten jedes Zusatzes werden zum Preis addiert. Da Zusätze flexibel und beliebig kombinierbar sein sollen, eignet sich das **Decorator Pattern**.

  

**Wichtig für Multiple-Choice-Fragen:** Wenn Decorator die fachlich richtige Antwort ist, aber nicht als Auswahl angeboten wird, ist die Frage wahrscheinlich unvollständig. Strategy, Template Method und Factory Method sind dafür kein gleichwertiger Ersatz.

  

## Mini-Merkliste

- Strategy = **austauschen**

- Decorator = **ergänzen**

- Observer = **benachrichtigen**

- Singleton = **einmalig**

- Factory Method = **erzeugen**

- Command = **Aktion kapseln**

- Adapter = **kompatibel machen**

- Facade = **vereinfachen**

- Template Method = **Ablauf festlegen**

- Iterator = **durchlaufen**