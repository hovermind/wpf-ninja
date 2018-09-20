## `{Binding Source="{StaticResource MyViewModel}", Path=X"}`
Sets binding context to instance of an object (i.e. `ViewModel`) so that you can bind property of that object using `Path`. 
Instead of establishing a scope in which several properties inherit the same `DataContext`, you can use the `Source` property.

#### Different Source for Different Controls
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.Resources>
      <local:EmployeeViewModel x:Key="EmployeeViewModel" />
      <local:CompanyViewModel x:Key="CompanyViewModel" />
    </Window.Resources>

    <Grid>
      <TextBox Grid.Column="1" Text="{Binding Source="{StaticResource CompanyViewModel}", Path=CompanyId}" />
      <TextBox Grid.Column="1" Text="{Binding Source="{StaticResource EmployeeViewModel}", Path=EmployeeName}" />
    </Grid>
	
</Window>
```

#### Set `DataContext` to Static Resource
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
