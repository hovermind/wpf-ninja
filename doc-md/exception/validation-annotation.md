## Validation by Annotations
* `System.ComponentModeI.DataAnnotations` (same as ASP.NET model binding, Entity Framework) 
* set of built-in attributes - `Required`, `RegularExpression`, `StringLength`, `Range`, `Phone`, `Email`, `Url`, `CreditCard` 
* need to write code to evaluate (`ValidationContext` and `Validator` classes)
* `ValidatesOnExceptions=True` (since Exception will be thrown for invalid data)

`MyViewModel.cs`
```
public class MyViewModel : ObservableObject
{
	private string _username;

	[Required(ErrorMessage = "Must not be empty.")]
	[StringLength(maximumLength: 50, MinimumLength = 5, ErrorMessage = "Must be at least 5 characters.")]
	public string Username
	{
		get { return _username; }
		set
		{
			ValidateProperty(value, "Username");
			OnPropertyChanged(ref _username, value);
		}
	}
  
  // should be in BaseViewModel
	private void ValidateProperty<T>(T value, string name)
	{
		Validator.ValidateProperty(value, new ValidationContext(this, null, null)
		{
			MemberName = name
		});
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
        Title="Validation By IDataErrorInfo" Height="450" Width="800">
		
    <Window.DataContext>
        <local:MyViewModel/>
    </Window.DataContext>

  <StackPanel>
    <Label>Username</Label>
    <TextBox Text="{Binding Username, ValidatesOnExceptions=True, UpdateSourceTrigger=PropertyChanged}" />
    <Button>Submit</Button>
  </StackPanel>

</Window>
```
