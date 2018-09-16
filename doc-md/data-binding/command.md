## Commands
Commands are an implementation of the ICommand interface that is part of the .NET Framework
ICommand interface specifies three members:
* the method `Execute` is called when the command is actuated. It has one parameter, which can be used to pass additional information from the caller to the command
* the method `CanExecute` returns a Boolean. If the return value is true, it means that the command can be executed. The parameter is the same one as for the `Execute` method. 
When used in XAML controls that support the Command property, the control will be automatically disabled if CanExecute returns false
* the `CanExecuteChanged` event handler must be raised by the command implementation when the `CanExecute` method needs to be reevaluated
In XAML, when an instance of ICommand is bound to a control’s Command property through a data-binding, raising the `CanExecuteChanged` event will automatically call the `CanExecute` method, and the control will be enabled or disabled accordingly

In WPF, the `CanExecuteChanged` event does not need to be raised manually. `CommandManager` class is observing the user interface and calls the `CanExecute` method when it deems it necessary. 

See: [Commanding Overview](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/commanding-overview)

#### Command Sources
A command source is the object which invokes the command i.e.`MenuItem`, `Button` etc.
Command sources in WPF generally implement the `ICommandSource` interface. `ICommandSource` exposes three properties:
* `Command`: the command to execute when the command source is invoked (i.e. delete `Button` is clicked)
* `CommandTarget`: is the object on which to execute the command (i.e. row in a grid)
* `CommandParameter`: is a user-defined data type used to pass information to the handlers implementing the command

Typically, a command source will listen to the `CanExecuteChanged` event. 
This event informs the command source that the ability of the command to execute on the current command target may have changed (enable/disable depending on state)
