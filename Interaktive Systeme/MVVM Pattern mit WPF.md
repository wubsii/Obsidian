## Modulübersicht

In diesem Modul geht es um das MVVM-Architekturmuster und dessen Umsetzung mit WPF.

Die Themenbereiche sind:

1. Grundlagen von MVVM
    
2. Motivation, Vorteile und Nachteile
    
3. Implementierungsbeispiele
    
4. Commands (`ICommand`, `DelegateCommand`)
    
5. Unit Tests
    
6. Dependency Injection
    

---

# 1. Was ist MVVM?

MVVM steht für:

- **Model** – Daten und Geschäftslogik
    
- **View** – Benutzeroberfläche
    
- **ViewModel** – Verbindung zwischen View und Model
    

MVVM ist ein Architektur-Pattern, das von John Gossman entwickelt wurde.

Es ist eine Variation des MVC-Patterns (Model-View-Controller) und ähnelt dem Presentation Model Pattern von Martin Fowler.

MVVM verwendet insbesondere:

- WPF Data Binding
    
- Commanding
    

Ziel ist es, die Benutzeroberfläche, die Daten und die Anwendungslogik voneinander zu trennen.

## Aufbau von MVVM

Die drei Bestandteile:

|Bestandteil|Aufgabe|
|---|---|
|Model|Enthält Daten und Domain-Klassen|
|View|Stellt die Benutzeroberfläche dar|
|ViewModel|Vermittelt zwischen View und Model|

### Abhängigkeiten

- Die View kennt das ViewModel.
    
- Das ViewModel kennt die Models.
    
- Das Model kennt das ViewModel nicht.
    
- Das ViewModel kennt die View nicht.
    

**Merke:** Die Abhängigkeiten gehen von der View über das ViewModel zum Model.

---

# 2. Motivation – Vorteile von MVVM

MVVM verfolgt das Ziel, die Anwendung übersichtlicher und besser testbar zu machen.

## Vorteile

### Testbarkeit

Das ViewModel kann unabhängig von der grafischen Oberfläche getestet werden.

Dadurch können Unit Tests durchgeführt werden, ohne die eigentliche View starten zu müssen.

### Separation of Concerns

Die verschiedenen Aufgaben werden auf unterschiedliche Komponenten aufgeteilt.

- View: Darstellung
    
- ViewModel: Präsentationslogik
    
- Model: Daten und Geschäftslogik
    

### Unabhängigkeit

- Das Model ist unabhängig von der View.
    
- Das ViewModel ist unabhängig von der View.
    

Dadurch können Änderungen an der Oberfläche vorgenommen werden, ohne die gesamte Anwendungslogik verändern zu müssen.

## Nachteile von MVVM

- Die konkrete Implementierung ist teilweise Geschmackssache.
    
- Für kleine und einfache Anwendungen kann MVVM unnötig aufwendig sein (_Overkill_).
    
- Es entsteht zusätzlicher Implementierungsaufwand durch ViewModels, Commands und Datenbindungen.
    

---

# 3. Die drei Bestandteile von MVVM

## 3.1 View

Die View ist die Benutzeroberfläche der Anwendung.

Sie wird in WPF hauptsächlich mit XAML erstellt.

### Aufgaben

- Darstellung der Benutzeroberfläche.
    
- Verwendung von Controls.
    
- Verwendung von Data Templates.
    
- Bindung an das ViewModel.
    
- Command Bindings.
    

### Eigenschaften

- Möglichst wenig oder keine Logik.
    
- So einfach wie möglich halten.
    
- Wenig Code-Behind.
    
- Eine ViewModel-Instanz erstellen, beispielsweise über Dependency Injection.
    
- Command Bindings verwenden.
    
- Möglichst kein `x:Name` verwenden.
    

**Merke:** Die View ist für die Darstellung zuständig, nicht für die eigentliche Anwendungslogik.

## 3.2 ViewModel

Das ViewModel ist eine Abstraktion der View und dient als Verbindung zwischen View und Model.

Es enthält den Zustand der Benutzeroberfläche und die Logik, die für die Darstellung benötigt wird.

### Aufgaben

- Vermittlung zwischen View und Model.
    
- Verwaltung des View States.
    
- Value Conversion.
    
- Bereitstellung von Properties für Data Binding.
    
- Methoden zur Manipulation des ViewModels.
    
- Implementierung von Commands.
    
- Undo-Funktionalität.
    

### Eigenschaften für Data Binding

Ein ViewModel kann folgende Mechanismen verwenden:

|Mechanismus|Aufgabe|
|---|---|
|Dependency Properties (DP)|Eigenschaften, die das WPF-Dependency-Property-System verwenden|
|`INotifyPropertyChanged`|Meldet Änderungen an Eigenschaften|
|`ObservableCollection`|Meldet Änderungen an einer Sammlung|

### Wichtige Regeln

- Das ViewModel darf keine starke oder schwache Referenz auf die View besitzen.
    
- Es sollte unabhängig von der View sein.
    
- Es sollte testbar sein.
    

**Merke:** Das ViewModel enthält die Präsentationslogik und stellt der View die benötigten Daten und Commands zur Verfügung.

## 3.3 Model

Das Model enthält die Daten und Domain-Klassen der Anwendung.

### Beispiele

- Data Models
    
- DTOs (Data Transfer Objects)
    
- POCOs (Plain Old CLR Objects)
    
- Automatisch generierte Klassen
    
- Domain-Klassen
    

### Eigenschaften

- Keine Referenz auf das ViewModel.
    
- Enthält die Daten und die fachlichen Informationen.
    
- Die Abhängigkeit zwischen Domain Service und Presentation Layer kann die konkrete Gestaltung beeinflussen.
    

**Merke:** Das Model ist unabhängig von der Benutzeroberfläche und dem ViewModel.

---

# 4. Implementierungsbeispiele

## Beispiel: MVVM ohne direkte View-Logik

Bei einer Umsetzung mit MVVM werden Aufgaben, die normalerweise in der View stehen könnten, in das ViewModel ausgelagert.

Laut Präsentation gehören dazu:

- `ObservableCollection` ins ViewModel auslagern.
    
- Event-Subscription ins ViewModel auslagern.
    
- Event-Handling ins ViewModel auslagern.
    
- Kein `x:Name` verwenden.
    
- Unit Tests für das ViewModel erstellen.
    

### Ziel

Die View soll möglichst wenig Code enthalten.

Das ViewModel übernimmt die Verarbeitung und stellt die benötigten Daten für die Oberfläche bereit.

---

# 5. Commands in MVVM

## Was sind Commands?

Commands ermöglichen es, Aktionen der Benutzeroberfläche mit Methoden im ViewModel zu verbinden.

Dadurch muss die Logik nicht direkt im Code-Behind der View stehen.

Beispiel:

Ein Benutzer klickt auf einen Button.

Anstatt die Aktion direkt im Button-Click-Event zu implementieren, wird ein Command im ViewModel aufgerufen.

## Command Binding

Ein Command kann über XAML an ein UI-Control gebunden werden.

Beispiel:

```
<Button Content="Speichern"
        Command="{Binding SaveCommand}"/>
```

Der Button ruft dadurch den Command `SaveCommand` aus dem ViewModel auf.

## ICommand

`ICommand` ist ein Interface, das die Grundlage für Commands in WPF bildet.

Wichtige Bestandteile:

|Bestandteil|Aufgabe|
|---|---|
|`Execute`|Führt die Aktion aus|
|`CanExecute`|Prüft, ob die Aktion ausgeführt werden darf|
|`CanExecuteChanged`|Informiert darüber, dass sich die Ausführbarkeit geändert hat|

### Execute

Enthält beziehungsweise startet die auszuführende Aktion.

### CanExecute

Prüft, ob der Command aktuell ausgeführt werden kann.

Beispiel:

Ein Speichern-Button ist nur aktiv, wenn gültige Daten vorhanden sind.

## DelegateCommand

Ein DelegateCommand ist eine eigene Command-Implementierung, die Aktionen an übergebene Methoden beziehungsweise Delegates weiterleitet.

Dadurch muss nicht für jede Aktion eine komplett eigene Command-Klasse geschrieben werden.

### Vorteile

- Command-Logik wird ausgelagert.
    
- Das ViewModel kann Commands bereitstellen.
    
- Die View kann Commands über Data Binding aufrufen.
    

## Weitere Begriffe aus den Folien

- Command Binding
    
- Executed
    
- CanExecute
    
- Routed Events
    
- Delegieren der Logik an das ViewModel
    

**Merke:** Commands verbinden Benutzeraktionen mit Methoden im ViewModel und reduzieren die Logik im Code-Behind.

---

# 6. Unit Tests

Unit Tests werden verwendet, um einzelne Teile einer Anwendung unabhängig voneinander zu testen.

Bei MVVM ist besonders das ViewModel gut testbar.

### Warum?

- Das ViewModel besitzt keine Referenz auf die View.
    
- Die Präsentationslogik ist von der grafischen Oberfläche getrennt.
    
- Methoden und Eigenschaften können unabhängig getestet werden.
    

### Beispiel

Man könnte testen:

- Ob ein Command die richtige Aktion ausführt.
    
- Ob sich eine Property nach einer Aktion verändert.
    
- Ob eine ObservableCollection korrekt verändert wird.
    

**Merke:** Ein wichtiger Vorteil von MVVM ist die Möglichkeit, das ViewModel ohne die grafische Benutzeroberfläche zu testen.

---

# 7. Dependency Injection

Dependency Injection (DI) ist ein Konzept, bei dem benötigte Abhängigkeiten einer Klasse von außen bereitgestellt werden.

Dadurch muss eine Klasse ihre benötigten Objekte nicht selbst erstellen.

In der Präsentation wird **Unity** als Dependency-Injection-Framework genannt.

### Beispielhafter Zusammenhang mit MVVM

- Eine View benötigt ein ViewModel.
    
- Das ViewModel benötigt möglicherweise einen Service.
    
- Die benötigten Objekte können über Dependency Injection bereitgestellt werden.
    

### Vorteile

- Abhängigkeiten werden von außen bereitgestellt.
    
- Klassen sind weniger stark miteinander gekoppelt.
    
- Komponenten können leichter ausgetauscht und getestet werden.
    

**Merke:** Dependency Injection hilft dabei, Abhängigkeiten zwischen Klassen zu verwalten und die Anwendung flexibel zu gestalten.

---

# 8. Beispiel Aktienservice

Die Präsentation nennt einen Aktienservice als Beispiel für die Umsetzung von MVVM.

Die konkreten Implementierungsschritte und der vollständige Beispielcode sind in den übermittelten Folieninhalten nicht enthalten.

Das Beispiel lässt sich anhand der MVVM-Aufteilung folgendermaßen einordnen:

|Bestandteil|Mögliche Aufgabe|
|---|---|
|View|Aktieninformationen anzeigen|
|ViewModel|Daten für die Oberfläche bereitstellen und Aktionen verwalten|
|Model|Aktieninformationen und zugehörige Daten darstellen|
|Service|Aktieninformationen bereitstellen|

---

# Prüfungswissen – Das solltest du können

## MVVM-Grundlagen

- Wofür steht MVVM?
    
- Welche drei Bestandteile gibt es?
    
- Was ist die Aufgabe von Model, View und ViewModel?
    
- Welche Abhängigkeiten bestehen zwischen den drei Bestandteilen?
    
- Warum wird MVVM verwendet?
    

## View, ViewModel und Model

- Warum sollte die View möglichst wenig Logik enthalten?
    
- Warum darf das ViewModel keine Referenz auf die View besitzen?
    
- Welche Eigenschaften stellt das ViewModel für Data Binding bereit?
    
- Was gehört in das Model?
    
- Was bedeutet Separation of Concerns?
    

## Commands

- Was ist ein Command?
    
- Wofür wird `ICommand` verwendet?
    
- Was ist der Unterschied zwischen `Execute` und `CanExecute`?
    
- Was ist ein DelegateCommand?
    
- Warum werden Commands statt Click-Events im Code-Behind verwendet?
    

## Unit Tests und Dependency Injection

- Warum ist das ViewModel gut testbar?
    
- Was ist Dependency Injection?
    
- Welche Vorteile bietet DI?
    
- Welches DI-Framework wird in der Präsentation genannt?
    

---

# Merksätze

- **MVVM:** Model – View – ViewModel.
    
- **View:** Benutzeroberfläche, möglichst keine Logik.
    
- **ViewModel:** Verbindung zwischen View und Model.
    
- **Model:** Daten und Domain-Klassen.
    
- **Separation of Concerns:** Aufgaben voneinander trennen.
    
- **INotifyPropertyChanged:** Meldet Änderungen an Properties.
    
- **ObservableCollection:** Meldet Änderungen an Sammlungen.
    
- **ICommand:** Grundlage für Commands in WPF.
    
- **Execute:** Führt eine Aktion aus.
    
- **CanExecute:** Prüft, ob eine Aktion ausgeführt werden darf.
    
- **DelegateCommand:** Leitet eine Aktion an einen Delegate weiter.
    
- **Unit Tests:** Testen einzelne Komponenten unabhängig.
    
- **Dependency Injection:** Stellt Abhängigkeiten von außen bereit.
    
- **Unity:** In der Präsentation genanntes DI-Framework.