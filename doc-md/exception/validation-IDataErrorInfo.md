
## Validation by `IDataErrorInfo`
* `IDataErrorlnfo` interface defines API for querying an object for errors 
  * `Error` property - allows the view model or model class to provide an error message for the entire object. However, this property is not currently called by the WPF data binding engine.
  * Indexer- allows the view model or model class to provide an error message specific to the named property
* `Binding` checks bound object to see if it implements IDataErrorlnfo and queries it whenever binding calls get/set block (performance issue since error is checked for every get/set call)
* need to set `ValidatesOnDataErrors` to true on `Binding`
* **property value `null` or `string.Empty` means no error** & only one string error per property


`MyViewModel.cs`
```
public class MyViewModel : ObservableObject, IDataErrorInfo {

	private string _username;
	public string Username {
		get { return _username; }
		set {
			OnPropertyChanged(ref _username, value);
		}
	}

	public string this[string propertyName] {
		get {
			return GetErrorForProperty(propertyName);
		}
	}

	private string GetErrorForProperty(string propertyName) {

		string result = null;

		switch(propertyName) { // case for each property

			case "Username":
				if(string.IsNullOrWhiteSpace(Username)) {
					result = "Username cannot be empty";
				} else if(Username.Length < 5) {
					result = "Username must be a minimum of 5 characters.";
				}
				break;

			default:
				result = string.Empty;
				break;
		}

		return result;
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
    <TextBox Text="{Binding Username, ValidatesOnDataErrors=True, UpdateSourceTrigger=PropertyChanged}" />
    <Button>Submit</Button>
  </StackPanel>

</Window>
```

## Tooltip (`Dictionary<string, string> ErrorCollection`)
`MyViewModel.cs`
```
public class MyViewModel : ObservableObject, IDataErrorInfo {

	private string _username;
	public string Username {
		get { return _username; }
		set {
			OnPropertyChanged(ref _username, value);
		}
	}

	// For tooltip
	public Dictionary<string, string> ErrorCollection { get; private set; } = new Dictionary<string, string>();

	public string Error { get { return null; } } // error message for the entire object. However, this property is not currently called by the WPF data binding engine.
	public string this[string propertyName] {
		get {
			return GetErrorForProperty(propertyName);
		}
	}

	private string GetErrorForProperty(string propertyName) {

		string result = null;

		switch(propertyName) { // case for each property

			case "Username":
				if(string.IsNullOrWhiteSpace(Username)) {
					result = "Username cannot be empty";
				} else if(Username.Length < 5) {
					result = "Username must be a minimum of 5 characters.";
				}
				break;

			default:
				result = string.Empty;
				break;
		}

		if(ErrorCollection.ContainsKey(propertyName)) {
			ErrorCollection[propertyName] = result;
		} else if(result != null) {
			ErrorCollection.Add(propertyName, result);
		}

		// For tooltip
		OnPropertyChanged("ErrorCollection");

		return result;
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
    <TextBox Text="{Binding Username, ValidatesOnDataErrors=True, UpdateSourceTrigger=PropertyChanged}" ToolTip="{Binding ErrorCollection[Username]}"/>
    <Button>Submit</Button>
  </StackPanel>

</Window>
```
