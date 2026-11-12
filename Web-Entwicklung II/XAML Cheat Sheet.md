## Basic Structure
```xml
<Window x:Class="MyApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="My App" Height="350" Width="525">
    
    <Grid>
        <!-- UI elements go here -->
    </Grid>
</Window>
```
- `<Window>` – root element for WPF window.
- `<Grid>` – main layout container (rows and columns optional).
- `x:Class` – connects XAML to the code-behind.
- `xmlns` – required namespaces for XAML.
## Layout Panels

|Panel|Description|Example|
|---|---|---|
|`Grid`|Rows & columns|`<Grid><Grid.RowDefinitions>...</Grid.RowDefinitions></Grid>`|
|`StackPanel`|Stack elements vertically/horizontally|`<StackPanel Orientation="Horizontal">...</StackPanel>`|
|`DockPanel`|Dock elements to top/bottom/left/right|`<DockPanel><Button DockPanel.Dock="Top"/>...</DockPanel>`|
|`WrapPanel`|Wraps children if no space|`<WrapPanel Orientation="Horizontal">...</WrapPanel>`|
|`Canvas`|Absolute positioning|`<Canvas><Button Canvas.Left="10" Canvas.Top="20"/></Canvas>`|
## **Common Controls**

|Control|Common Properties|Example|
|---|---|---|
|`Button`|`Content`, `Click`|`<Button Content="Click Me" Click="Btn_Click"/>`|
|`TextBox`|`Text`, `Width`, `Height`|`<TextBox Text="Hello" Width="100"/>`|
|`Label`|`Content`|`<Label Content="Name:"/>`|
|`CheckBox`|`IsChecked`, `Content`|`<CheckBox Content="Accept"/>`|
|`RadioButton`|`IsChecked`, `GroupName`|`<RadioButton Content="Yes" GroupName="G"/>`|
|`ComboBox`|`Items`, `SelectedItem`|`<ComboBox><ComboBoxItem>Item1</ComboBoxItem></ComboBox>`|
|`ListBox`|`ItemsSource`, `SelectedItem`|`<ListBox><ListBoxItem>Item1</ListBoxItem></ListBox>`|
|`Slider`|`Minimum`, `Maximum`, `Value`|`<Slider Minimum="0" Maximum="100" Value="50"/>`|
|`Image`|`Source`, `Width`, `Height`|`<Image Source="img.png" Width="100"/>`|
## Layout Properties

|Property|Description|
|---|---|
|`Margin`|Space outside the element|
|`Padding`|Space inside the element|
|`HorizontalAlignment`|`Left`, `Center`, `Right`, `Stretch`|
|`VerticalAlignment`|`Top`, `Center`, `Bottom`, `Stretch`|
|`Grid.Row` / `Grid.Column`|Assign element to grid cell|
|`RowSpan` / `ColumnSpan`|Span multiple rows/columns|

## Styles and Resources
```xml
<Window.Resources>
    <Style x:Key="RedButton" TargetType="Button">
        <Setter Property="Background" Value="Red"/>
        <Setter Property="Foreground" Value="White"/>
    </Style>
</Window.Resources>

<Button Content="Click Me" Style="{StaticResource RedButton}"/>
```

- `Resources` – reusable styles, brushes, templates.    
- `StaticResource` – reference at compile-time.    
- `DynamicResource` – reference evaluated at runtime.

## Data Binding
```xml
<TextBox Text="{Binding Name, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"/>
<Label Content="{Binding Name}"/>
```

- `Binding` – connects UI to data source.    
- `Mode`: `OneWay`, `TwoWay`, `OneTime`.    
- `UpdateSourceTrigger`: `PropertyChanged`, `LostFocus`, etc.
## Event Handling
```xml
<Button Content="Click Me" Click="Button_Click"/>
```
In Code Behind:
```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Button clicked!");
}
```

## Common Shortcuts

|Shortcut / Tip|Description|
|---|---|
|`x:Name="element"`|Name element for code-behind|
|`Visibility="Collapsed"`|Hide element (no space)|
|`Visibility="Hidden"`|Hide element (keep space)|
|`HorizontalContentAlignment` / `VerticalContentAlignment`|Align content inside controls|
