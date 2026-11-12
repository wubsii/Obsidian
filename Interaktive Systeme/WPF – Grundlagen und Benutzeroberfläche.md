# 1. Was ist WPF?

WPF steht für **Windows Presentation Foundation**.

WPF ist eine Technologie von Microsoft zur Entwicklung grafischer Benutzeroberflächen für Windows-Anwendungen.

WPF gehört zur .NET-Plattform und wird häufig mit C# verwendet.

## Entwicklungsumgebung

- **C#:** Programmiersprache
    
- **.NET:** Entwicklungsplattform
    
- **Visual Studio:** Entwicklungsumgebung
    
- **WPF:** Technologie zur Erstellung von Benutzeroberflächen
    
- **XAML:** Sprache zur Beschreibung der Benutzeroberfläche
    

## Was ist XAML?

XAML steht für _Extensible Application Markup Language_.

Mit XAML wird die Benutzeroberfläche einer WPF-Anwendung beschrieben.

Damit können beispielsweise folgende Elemente definiert werden:

- Fenster
    
- Buttons
    
- TextBoxen
    
- Labels
    
- Layouts
    
- Farben und Ressourcen
    

Beispiel:

```
<Window x:Class="WpfApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Meine erste WPF-Anwendung"
        Height="300"
        Width="400">

    <Grid>
        <Button Content="Klick mich"/>
    </Grid>

</Window>
```

### Wichtige Eigenschaften eines Window-Elements

|Eigenschaft|Bedeutung|
|---|---|
|`Title`|Titel des Fensters|
|`Height`|Höhe des Fensters|
|`Width`|Breite des Fensters|
|`Background`|Hintergrundfarbe|
|`Content`|Inhalt des Fensters|

---

# 2. Aufbau einer WPF-Anwendung

Eine WPF-Anwendung besteht typischerweise aus XAML und dazugehörigem C#-Code.

## XAML-Datei

Die XAML-Datei beschreibt das Aussehen und den Aufbau der Benutzeroberfläche.

Beispielsweise:

- Welche Buttons gibt es?
    
- Wo befinden sich die Elemente?
    
- Welche Farben werden verwendet?
    
- Welche Texte werden angezeigt?
    

## C#-Datei (Code-Behind)

Die dazugehörige C#-Datei enthält den Code, der mit der Benutzeroberfläche zusammenarbeitet.

Beispielsweise:

- Button-Klicks verarbeiten
    
- Berechnungen durchführen
    
- Werte verändern
    
- Auf Benutzeraktionen reagieren
    

Beispiel:

**MainWindow.xaml**

```
<Window x:Class="WpfApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Beispiel"
        Height="300"
        Width="400">

    <StackPanel>
        <Button Content="Klick mich"
                Click="Button_Click"/>
    </StackPanel>

</Window>
```

**MainWindow.xaml.cs**

```
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Hallo WPF!");
}
```

---

# 3. WPF Layout – Benutzeroberfläche anordnen

WPF verwendet sogenannte Panels, um Steuerelemente innerhalb eines Fensters anzuordnen.

Die Basisklasse dieser Layout-Container ist `Panel`.

## Die wichtigsten Layout-Klassen

|Klasse|Aufgabe|
|---|---|
|`Canvas`|Elemente frei über Koordinaten positionieren|
|`DockPanel`|Elemente an einer Seite anordnen|
|`Grid`|Elemente in Zeilen und Spalten anordnen|
|`StackPanel`|Elemente untereinander oder nebeneinander anordnen|
|`VirtualizingStackPanel`|Elemente wie ein StackPanel anordnen und Virtualisierung ermöglichen|
|`WrapPanel`|Elemente automatisch umbrechen|

## Canvas

Mit `Canvas` können Elemente frei positioniert werden.

Die Position wird über Koordinaten festgelegt.

```
<Canvas>
    <Button Content="Button 1"
            Canvas.Left="50"
            Canvas.Top="30"/>

    <Button Content="Button 2"
            Canvas.Left="150"
            Canvas.Top="100"/>
</Canvas>
```

## DockPanel

Mit `DockPanel` werden Elemente an den Seiten eines Containers angeordnet.

Mögliche Positionen:

- Top
    
- Bottom
    
- Left
    
- Right
    

```
<DockPanel>
    <Button Content="Oben"
            DockPanel.Dock="Top"/>

    <Button Content="Links"
            DockPanel.Dock="Left"/>

    <Button Content="Inhalt"/>
</DockPanel>
```

## Grid

Mit `Grid` wird die Oberfläche in Zeilen und Spalten unterteilt.

```
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>

    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>

    <Button Content="Button 1"
            Grid.Row="0"
            Grid.Column="0"/>

    <Button Content="Button 2"
            Grid.Row="1"
            Grid.Column="1"/>
</Grid>
```

## StackPanel

Mit `StackPanel` werden Elemente hintereinander angeordnet.

```
<StackPanel Orientation="Vertical">
    <Button Content="Button 1"/>
    <Button Content="Button 2"/>
    <Button Content="Button 3"/>
</StackPanel>
```

- `Vertical`: Elemente untereinander.
    
- `Horizontal`: Elemente nebeneinander.
    

## WrapPanel

Mit `WrapPanel` werden Elemente automatisch in die nächste Zeile oder Spalte verschoben, wenn nicht mehr genügend Platz vorhanden ist.

```
<WrapPanel>
    <Button Content="1"/>
    <Button Content="2"/>
    <Button Content="3"/>
    <Button Content="4"/>
</WrapPanel>
```

## VirtualizingStackPanel

Funktioniert ähnlich wie ein StackPanel.

Bei großen Datenmengen müssen nicht alle Elemente gleichzeitig visuell erzeugt werden. Dadurch kann die Darstellung großer Listen effizienter werden.

---

# 4. Panel – Wichtige Eigenschaften

`Panel` ist die Basisklasse für verschiedene Layout-Container.

Wichtige Eigenschaften:

|Eigenschaft|Bedeutung|
|---|---|
|`Background`|Hintergrundfarbe|
|`Children`|Enthält die untergeordneten Elemente|
|`ZIndex`|Bestimmt die Reihenfolge bei überlappenden Elementen|

---

# 5. Controls – Steuerelemente

Controls sind Elemente, mit denen Benutzer interagieren können.

WPF bietet unterschiedliche Arten von Controls.

## Content Controls

Ein Content Control enthält grundsätzlich ein einzelnes Inhaltselement.

Es besitzt die Eigenschaft `Content`.

Beispiele:

|Control|Aufgabe|
|---|---|
|`Button`|Schaltfläche|
|`CheckBox`|Kontrollkästchen|
|`GroupItem`|Gruppiert ein Element|
|`Label`|Beschriftung|
|`RadioButton`|Auswahl einer Option|
|`RepeatButton`|Wiederholt eine Aktion beim Gedrückthalten|
|`ToggleButton`|Schaltfläche mit zwei Zuständen|
|`ToolTip`|Zeigt zusätzliche Informationen an|

### Beispiel

```
<Button Content="Speichern"/>
```

Die Eigenschaft `Content` bestimmt, was innerhalb des Buttons angezeigt wird.

## Headered Content Controls

Headered Content Controls sind eine spezielle Form von Content Controls.

Sie besitzen zwei wichtige Eigenschaften:

- `Content`: Der eigentliche Inhalt.
    
- `Header`: Die Überschrift.
    

Beispiele:

|Control|Aufgabe|
|---|---|
|`Expander`|Ein- und ausklappbarer Bereich|
|`GroupBox`|Gruppiert Elemente mit einer Überschrift|
|`TabItem`|Einzelner Reiter eines TabControls|

### Beispiel

```
<GroupBox Header="Persönliche Daten">
    <StackPanel>
        <Label Content="Vorname"/>
        <TextBox/>
    </StackPanel>
</GroupBox>
```

---

# 6. Items Controls

Items Controls können mehrere Objekte enthalten.

Sie besitzen zwei wichtige Eigenschaften:

- `Items`: Enthält die Elemente direkt.
    
- `ItemsSource`: Gibt eine Datenquelle an, aus der die Elemente geladen werden.
    

Beispiele:

|Control|Aufgabe|
|---|---|
|`ComboBox`|Dropdown-Liste|
|`ListBox`|Liste mit auswählbaren Elementen|
|`Menu`|Menü|
|`StatusBar`|Statusleiste|
|`TabControl`|Benutzeroberfläche mit mehreren Tabs|
|`ToolBar`|Werkzeugleiste|
|`TreeView`|Hierarchische Baumansicht|

### Beispiel

```
<ListBox>
    <ListBoxItem Content="Apfel"/>
    <ListBoxItem Content="Banane"/>
    <ListBoxItem Content="Orange"/>
</ListBox>
```

## Auswahl von Elementen

Mit dem Event `SelectionChanged` kann auf eine veränderte Auswahl reagiert werden.

```
<ListBox SelectionChanged="ListBox_SelectionChanged">
    <ListBoxItem Content="Apfel"/>
    <ListBoxItem Content="Banane"/>
</ListBox>
```

C#:

```
private void ListBox_SelectionChanged(
    object sender,
    SelectionChangedEventArgs e)
{
    // Wird ausgeführt, wenn sich die Auswahl ändert
}
```

---

# 7. Resources – Ressourcen

Resources ermöglichen es, häufig verwendete Objekte und Werte wiederzuverwenden.

Beispiele:

- Brushes
    
- Farben
    
- Styles
    
- Control Templates
    

Dadurch müssen bestimmte Werte nicht immer wieder neu definiert werden.

## Wo können Resources definiert werden?

Es gibt drei Ebenen:

1. **Application Scope:** Für die gesamte Anwendung.
    
2. **Window oder Page Scope:** Für ein bestimmtes Fenster oder eine Seite.
    
3. **Element-Level Scope:** Für ein bestimmtes Element und dessen untergeordnete Elemente.
    

## Resources in XAML definieren

```
<Window.Resources>

    <SolidColorBrush x:Key="blueBrush"
                     Color="Blue"/>

    <SolidColorBrush x:Key="whiteBrush"
                     Color="White"/>

</Window.Resources>
```

`x:Key` ist der eindeutige Schlüssel, über den eine Resource angesprochen wird.

## StaticResource

Mit `StaticResource` wird eine Resource statisch referenziert.

```
<Button Background="{StaticResource blueBrush}"
        Foreground="{StaticResource whiteBrush}"
        Content="Klick mich"/>
```

Die Resource wird beim Laden der Oberfläche aufgelöst.

## DynamicResource

Mit `DynamicResource` wird eine Resource dynamisch referenziert.

```
<Button Background="{DynamicResource blueBrush}"
        Content="Klick mich"/>
```

Änderungen an der Resource können zur Laufzeit übernommen werden.

## Unterschied

|StaticResource|DynamicResource|
|---|---|
|Statische Referenz|Dynamische Referenz|
|Wird beim Laden aufgelöst|Kann zur Laufzeit neu aufgelöst werden|
|Für unveränderliche Ressourcen geeignet|Für veränderliche Ressourcen geeignet|

## Resources in C# verwenden

Es gibt verschiedene Möglichkeiten, auf Ressourcen zuzugreifen.

### FindResource()

```
SolidColorBrush brush = (SolidColorBrush)
    this.FindResource("whiteBrush");
```

Sucht eine Resource anhand ihres Schlüssels. Wird sie nicht gefunden, entsteht eine Ausnahme.

### TryFindResource()

Sucht ebenfalls nach einer Resource, gibt aber `null` zurück, wenn sie nicht gefunden wird.

### SetResourceReference()

Verknüpft eine Eigenschaft eines Controls mit einer Resource.

```
this.myButton.SetResourceReference(
    Button.BackgroundProperty,
    "whiteBrush");
```

### Resources-Eigenschaft

```
SolidColorBrush brush = (SolidColorBrush)
    this.Resources["whiteBrush"];
```

Greift direkt auf eine Resource des aktuellen Elements zu.

---

# 8. Prüfungswissen

## WPF-Grundlagen

- Wofür steht WPF?
    
- Wofür wird XAML verwendet?
    
- Welche Aufgaben haben XAML und Code-Behind?
    
- Was ist der Zusammenhang zwischen C#, .NET, Visual Studio und WPF?
    

## Layouts

- Unterschied zwischen Canvas, DockPanel und Grid erklären.
    
- StackPanel und WrapPanel unterscheiden.
    
- Wissen, wofür VirtualizingStackPanel verwendet wird.
    
- Die wichtigsten Eigenschaften von Panel kennen.
    

## Controls

- Content Controls erklären können.
    
- `Content` und `Header` unterscheiden.
    
- Beispiele für Content Controls nennen.
    
- Items Controls erklären können.
    
- `Items` und `ItemsSource` unterscheiden.
    
- Wissen, wofür `SelectionChanged` verwendet wird.
    

## Resources

- Erklären können, warum Resources verwendet werden.
    
- Die drei Ebenen der Ressourcendefinition kennen.
    
- `StaticResource` und `DynamicResource` unterscheiden.
    
- `FindResource()` und `TryFindResource()` kennen.
    

---

# 9. Merksätze

- **WPF:** Technologie zur Entwicklung grafischer Windows-Anwendungen.
    
- **XAML:** Beschreibt die Benutzeroberfläche.
    
- **Code-Behind:** Enthält C#-Code zur Interaktion mit der Oberfläche.
    
- **Panel:** Basisklasse für Layout-Container.
    
- **Canvas:** Freie Positionierung.
    
- **DockPanel:** Anordnung an Seiten.
    
- **Grid:** Zeilen und Spalten.
    
- **StackPanel:** Elemente hintereinander.
    
- **WrapPanel:** Automatischer Umbruch.
    
- **ContentControl:** Grundsätzlich ein Inhaltselement.
    
- **HeaderedContentControl:** Inhalt plus Überschrift.
    
- **ItemsControl:** Mehrere Elemente.
    
- **ItemsSource:** Datenquelle für Elemente.
    
- **Resources:** Wiederverwendbare Objekte und Werte.
    
- **StaticResource:** Statische Ressourcenreferenz.
    
- **DynamicResource:** Dynamische Ressourcenreferenz.