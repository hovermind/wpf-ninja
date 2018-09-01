## View First Approach
Model: `Employee.cs`
```
public class EmployeeViewModel
{
    public int Id {get; set;}
    public string Name {get; set;}
    
    public EmployeeViewModel()
    {
        Id = 123;
        Name = "ABC";
    }
}
```

View: `MainWindow.xaml`
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.Resources>
        <local:EmployeeViewModel x:Key="EmployeeViewModel" />
    </Window.Resources>
	
    <Grid DataContext="{StaticResource EmployeeViewModel}">
	
		// ... ...
		
        <TextBox Grid.Column="1" Text="{Binding Id}" />
        <TextBox Grid.Column="1" Text="{Binding Name}" />
		
    </Grid>
	
</Window>
```
