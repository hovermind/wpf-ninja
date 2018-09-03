## UserControl
A `UserControl` is a reusable user-created control that you can add to your UI the same way you would add any other control.

When to use `UserControl`:
* there is a large amount of related XAML code i.e. a **View when using the MVVM design pattern**
* to create some reusable component (but not standalone one) to use it in multiple different Windows
* to build in some custom functionality (for example, a `CalendarControl`)

## Creating UserControl

`FieldUserControl.xaml`
```
<UserControl x:Class="Demo.FieldUserControl" Name="ThisControl">

  <StackPanel DataContext={Binding ElementName=ThisControl} Orientation="Horizontal">
  
    <TextBlock Text="{Binding Label}" Width="100"/>
	
    <TextBox Text="{Binding TxtInput}" Width="100"/>
	
  </StackPanel>
  
</UserControl>
```

* **a `UserControl` should never specify its own data context in its definition (Set `DataContext` in it's root layout)**
* if `DataContext` is set in definition (hard-coded), then `DataContext` inheritance (from parent) would not work
* in a page/window/other control i.e. `<local:FieldUserControl Label="Name:" TxtInput="{Binding Name}"/>` would expect `Name` property in `UserControl` class itself instaed of `DataContext` of page/window/other control (containing `UserControl`)

#### Code Behind
`FieldUserControl.cs`
```
public partial class FieldUserControl : UserControl
{

  public String Label
  {
    get { return (String)GetValue(LabelProperty); }
    set { SetValue(LabelProperty, value); }
  }
  
  public static readonly DependencyProperty LabelProperty = DependencyProperty.Register("Label", typeof(string), typeof(FieldUserControl), new PropertyMetadata(""));
  
  public object TxtInput
  {
    get { return (object)GetValue(TxtInputProperty); }
    set { SetValue(TxtInputProperty, value); }
  }

  public static readonly DependencyProperty TxtInputProperty = DependencyProperty.Register("TxtInput", typeof(object),typeof(FieldUserControl), new PropertyMetadata(null));

  public FieldUserControl()
  {
    InitializeComponent();
	
	Label = "default label";
	TxtInput = "default txt input";
  }
}
```
**Note:** Label & TxtInput are dependecny property to allow data binding while using `UserControl` in page/window/other control

## Using `UserControl` in MainWindow
```
<Window
    x:Class="Demo.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:Demo"
    Width="200" Height="200">
	
	<Window.DataContext>
	    <local:Person/>
	</Window.DataContext>
	
<Grid>

  <StackPanel Orientation="Vertical" HorizontalAlignment="Left" Margin="10">

    <local:FieldUserControl Label="Name:" TxtInput="{Binding Name}"/>

    <local:FieldUserControl Label="Id:" TxtInput="{Binding Id}"/>

  </StackPanel>

</Grid>
  
</Window>
```
