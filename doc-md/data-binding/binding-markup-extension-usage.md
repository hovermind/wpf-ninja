## Markup Extension Usage
Binding is a markup extension class : `Object` -> `MarkupExtension` -> `BindingBase` -> `Binding`    
Binding enables you to synchronize the values of the properties of "two different objects" (WPF Control & ViewModel)
* binding declaration consists of a series of clauses following the `Binding` keyword and separated by commas
* clauses in the binding declaration can be in any order and there are many possible combinations
* each clause is a `Name = Value` pairs where `Name` is the name of the `Binding` class property and `Value` is the value you are setting for that property

**Notes:**
* If you set `DataContext` use: `{Binding ViewModelProperty}` (syntactic sugar of `{Binding Path=MyViewModelProperty}`)
* If you did not set `DataContext` use: `{Binding Source={StaticResource ViewModel}, Path=ViewModelProperty}`   

**Source Object :** `MyViewModel`    
**Source Property :** `MyViewModel.Name`    
**Target Object :** `TextBox`    
**Target Property :** `Text`    
**Binding :** `<TextBox Text={Binding Source={StaticResource myDataSource}, Path=Name}>`   
**With `DataContext` :** `<TextBox Text={Binding Path=Name}>` (Syntactic Sugar : `<TextBox Text={Binding Name}>` )    

#### Markup Extension with Source
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.Resources>
        <local:EmployeeViewModel x:Key="EmployeeViewModel" />
    </Window.Resources>
	
    <TextBlock Text="{Binding Source={StaticResource EmployeeViewModel}, Path=Name}"/>
	
</Window>
```

#### Markup Extension with DataContext (Preferred)
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

        <TextBox Grid.Column="1" Text="{Binding Id}" />
        <TextBox Grid.Column="1" Text="{Binding Name}" />
		
    </Grid>
	
</Window>
```
