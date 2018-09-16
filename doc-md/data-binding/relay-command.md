## `Command` DependencyProperty
[Command Sources](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/commanding-overview#command-sources) in WPF generally implement the `ICommandSource` interface & `ICommandSource` exposes three properties: 
* `Command`
* `CommandTarget`
* `CommandParameter`

Some controls expose `Command` `DependencyProperty` like Button, MenuItem etc. which have some default event registered to it. For Button it's Click event. 
So, if you bind `ICommand` declared in ViewModel with a Button's `Command` DependencyProperty, it will be invoked whenever button is clicked on.

## Why RelayCommand?
Having to implement the `ICommand` interface every time a command must be added to the project is impractical. 
This is why we need a generic implementation of `ICommand` => `RelayCommand`

## Creating RelayCommand
Using a command (ViewModel property of type `ICommand`) to expose the “event handler” and bind the UI element to that command by using a XAML data-binding. 
Because data-bindings are evaluated only at run time, they won’t cause a compilation error. And because they are loosely coupled, they won’t risk causing memory leaks.


`RelayCommand.cs`
```
public class RelayCommand<T> : ICommand where T : class
{
    private readonly Predicate<T> _canExecute; // private readonly Func<T, bool> _canExecute;
    private readonly Action<T> _execute;
	
	public event EventHandler CanExecuteChanged;
 
    public RelayCommand(Action<T> execute): this(execute, null)
	{
    }
 
    public RelayCommand(Action<T> execute, Predicate<T> canExecute)
    {
        _execute = execute;
        _canExecute = canExecute;
    }
 
    public bool CanExecute(object parameter)
    {
        if (_canExecute == null)
		{
            return true;
		}
 
        return _canExecute((T)parameter);
    }
 
    public void Execute(object parameter)
    {
        _execute((T)parameter);
    }
 

    public void RaiseCanExecuteChanged()
    {
        if (CanExecuteChanged != null)
		{
            CanExecuteChanged(this, EventArgs.Empty);
		}
    }
}
```

The ViewModel will then expose property of this type for the view to bind to: `MyViewModel.cs`
```
public class MyViewModel
{

	public RelayCommand<string> ButtonClickCommand { get; private set; }
	
	private string _input;
    public string Input
    {
        get { return _input; }
        set
        {
            _input = value;
            ButtonClickCommand.RaiseCanExecuteChanged();
        }
    }
	
    public MyViewModel()
    {
        ButtonClickCommand = new RelayCommand<string>(
            (s) => { /* perform some action */ }, //Execute
            (s) => { return !string.IsNullOrEmpty(_input); } //CanExecute
        );
    }
 


}
```

`MainWindow.xaml.cs`
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.Resources>
	
        <local:MyViewModel x:Key="MyViewModel" />
		
    </Window.Resources>

	
	<StackPanel DataContext="{StaticResource MyViewModel}">

		<TextBox Text="{Binding Input, UpdateSourceTrigger=PropertyChanged}" />
		
		<Button Content="Click here!" Command="{Binding ButtonClickCommand}" />
		
	</StackPanel>
	
</Window>
```

With this approach you have now moved the presentation logic from the view to the view model. Instead of hooking up the button's click handler, 
its Command property is now bound to the command defined in the view model and when the user clicks on the button the command's Execute method will be invoked.

## Command Parameters
If you wish to pass a parameter to a command from the view you do so by using the `CommandParameter` property. The type argument of the generic `RelayCommand<T>` class specifies the type of the command parameter that gets passed to the `Execute` and `CanExecute` methods. The `CommandParameter` property exists in both the `ButtonBase` and `MenuItem` derived controls as well as in the `InvokeCommandAction` class:
```
<Button Content="Click here!" Command="{Binding ButtonClickCommand}"
                CommandParameter="some string to be passed..." />
```
