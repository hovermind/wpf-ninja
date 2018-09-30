## Validation by Exception
* simple - using exception for valdation is very convinient but not appropriate way to do it
* `Bindings` normally catch exceptions thrown by get/set blocks of bound properties 
* `ValidatesOnExceptions` property causes validation error on a control (if get/set block throw exception)
* allows the data object to reject invalid values before the property stores the value

`MyViewModel.cs`
```
public class MyViewModel : ObservableObject
{
	private string _username;
	public string Username
	{
		get { return _username; }
		set
		{
			if (string.IsNullOrWhiteSpace(value)){
				throw new ArgumentException("Username cannot be empty.");
			}
			
			OnPropertyChanged(ref _username, value);
		}
	}
}
```

`MainWindow.xaml`
```
<Window x:Class="MyApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:MyApp"
        mc:Ignorable="d"
        Title="Validation By Exception" Height="450" Width="800">
		
    <Window.DataContext>
        <local:MyViewModel/>
    </Window.DataContext>

	<StackPanel>
		<Label>Username</Label>
		<TextBox Text="{Binding Username, ValidatesOnExceptions=True, UpdateSourceTrigger=PropertyChanged}"/>
		<Button>Submit</Button>
	</StackPanel>

</Window>
```
