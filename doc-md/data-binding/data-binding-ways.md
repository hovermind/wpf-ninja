## [Using ViewModelLocator](https://github.com/hovermind/wpf-ninja/blob/mvvm/doc-md/mvvm/viewmodel-locator.md)

## In Code Behind Class Constructor
```
public MainWindow()
{
    InitializeComponent();
    this.DataContext = new EmployeeViewModel();
}
```
Using DI
```
public CalculatorView(CalculatorViewModel viewModel)
{
    InitializeComponent();
    this.DataContext = viewModel;
}
```
**You'd probably want to use an IOC container to instantiate `ViewModel` instead of**:
```
var viewModel = new CalculatorViewModel();
var view = new CalculatorView(viewModel);
```

## External Creation and Assignment
In this approach, the View doesn't even know how its DataContext will be set - our navigation code "peers in" to the view:
```
var view = new CalculatorView();
var viewModel = new CalculatorViewModel();
view.DataContext = viewModel;
```

## In XAML - Static Resource
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
If you want to change data context at runtime:
```
<UserControl ...>

    <UserControl.Resources>
        <local:CalculatorViewModel x:Key="Model" />
    </UserControl.Resources>
    
    <TextBox Text="{Binding Source={DynamicResource Model}, Path=""}" />
    
</UserControl>
```
Then in `ViewModel` constructor:
```
public CalculatorView(CalculatorViewModel viewModel)
{
    InitializeComponent();
    Resources["Model"] = viewModel;
}
```


## In XAML - Element Tag
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.DataContext>
        <local:EmployeeViewModel />
    </Window.DataContext>
	
    <Grid>

        <TextBox Grid.Column="1" Text="{Binding Id}" />
        <TextBox Grid.Column="1" Text="{Binding Name}" />
		
    </Grid>
	
</Window>
```

## In XAML - 'Element Tag' & 'Source Property' of Binding
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.Resources>
        <local:EmployeeViewModel x:Key="EmployeeViewModel" />
    </Window.Resources>
	
    <Grid>
	<Grid.DataContext>
	    <Binding Source="{StaticResource EmployeeViewModel}"/>
	</Grid.DataContext>
  
        <TextBox Grid.Column="1" Text="{Binding Id}" />
        <TextBox Grid.Column="1" Text="{Binding Name}" />
		
    </Grid>
	
</Window>
```
**See:** [Source property instead of the DataContext property](https://docs.microsoft.com/en-us/dotnet/api/system.windows.data.binding.source?view=netframework-4.7.2#remarks)
