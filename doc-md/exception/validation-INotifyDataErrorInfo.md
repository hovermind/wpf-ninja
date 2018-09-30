## Validation by `INotifyDataErrorInfo`
* same concept as `IDataErrorlnfo` with an event-driven interface but more flexible than the `IDataErrorInfo`
* supports multiple errors for a property
* asynchronous data validation
* need to manage a dictionary of errors per property as part of implementation
* need to set `ValidatesOnNotifyDataErrors` property on `Binding`
```
public interface INotifyDataErrorInfo {    
    bool HasErrors { get; }
    event EventHandler<DataErrorsChangedEventArgs> ErrorsChanged;
    IEnumerable GetErrors(string propertyName);
}
```
* `Binding` calls GetErrors when querying for errors
* `Binding` subscribes to `ErrorsChanged` event & re-queries if event is raised 

`MyViewModel.cs`
```
public class MyViewModel : ObservableObject, INotifyDataErrorInfo {

	public event EventHandler<DataErrorsChangedEventArgs> ErrorsChanged;

	private Dictionary<string, List<string>> _PropertyErrors = new Dictionary<string, List<string>>();

	private string _username;
	public string Username {
		get { return _username; }
		set {

			_username = value;
			OnPropertyChanged(ref _username, value);

			var shouldRaiseErrorsChanged = false;

			// gather all errors
			var nameErrorList = new List<String>();
			if(string.IsNullOrEmpty(value)) {
				nameErrorList.Add("Name can not be empty");
			}
			if(value.Length <= 7) {
				nameErrorList.Add("Name must be 8 characters or more");
			}

			// if no error: remove key from _PropertyErrors
			// if any error: update/add key to _PropertyErrors
			// List.Any() has better performance that List.Count == 0
			if(!nameErrorList.Any()) {

				if(_PropertyErrors.ContainsKey("Username")) {
					_PropertyErrors.Remove("Username");
					shouldRaiseErrorsChanged = true;
				}


			} else { // there is error

				if(_PropertyErrors.ContainsKey("Username")) {
					_PropertyErrors["Username"] = nameErrorList;
				} else {
					_PropertyErrors.Add("Username", nameErrorList);
				}

				shouldRaiseErrorsChanged = true;
			}

			// ErrorsChanged event
			if(shouldRaiseErrorsChanged) {
				ErrorsChanged?.Invoke(this, new DataErrorsChangedEventArgs("Username"));
			}
		}
	}


	public bool HasErrors {
		get {
			return _PropertyErrors.ContainsKey("Username");
		}
	}

	public IEnumerable GetErrors(string propertyName) {

		if(_PropertyErrors.ContainsKey(propertyName)) {
			return _PropertyErrors[propertyName];
		}

		return null; // null or sting.Empty means no error
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
    <TextBox Text="{Binding Username, ValidatesOnNotifyDataErrors=true, UpdateSourceTrigger=PropertyChanged}" />
    <Button>Submit</Button>
  </StackPanel>

</Window>
```
