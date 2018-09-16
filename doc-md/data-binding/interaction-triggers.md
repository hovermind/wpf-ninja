## Interaction Triggers
Unfortunately, only a rather small subset of controls (those derived from `System.Windows.Controls.Primitives.ButtonBase` or `System.Windows.Controls.MenuItem`) 
support commands out of the box with `Command` and `CommandParameter` properties. 

If you want to attach a command to some other control or when you want to invoke a command on an event other than the click event 
for a button, you can use Expression Blend interaction triggers (xmlns:i="clr-namespace:System.Windows.Interactivity;assembly=System.Windows.Interactivity") 
and the `System.Windows.Interactivity.InvokeCommandAction` class. 

```
<Window x:Class="MyNamespace.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation Jump "
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml Jump "
        xmlns:i="clr-namespace:System.Windows.Interactivity;assembly=System.Windows.Interactivity"
        Title="MainWindow" Height="350" Width="525">
        
    <Window.Resources>
	
        <local:MyViewModel x:Key="MyViewModel" />
		
    </Window.Resources>

	
    <StackPanel DataContext="{StaticResource MyViewModel}">

	      <TextBox Text="{Binding Input, UpdateSourceTrigger=PropertyChanged}" />

	      <Button Content="Click here!">
        
            <i:Interaction.Triggers>
            
                <i:EventTrigger EventName="MouseClick" >
                
                    <i:InvokeCommandAction Command="{Binding ButtonClickCommand}" />
                    
                </i:EventTrigger>
                
            </i:Interaction.Triggers>
            
        </Button>

    </StackPanel>
    
</Window>
```

**Notes:**
* remember to add a reference to `System.Windows.Interactivity.dll` for this to compile
* `InvokeCommandAction` doesn't automatically enable or disable the control based on the command's `CanExecute` method (unlike controls that have a Command property and can be bound directly to a command)

## Command Parameters
```
<i:InvokeCommandAction Command="{Binding MouseEnterCommand}" CommandParameter="some string to be passed..."/>
```

## CallMethodAction
Besides the `InvokeCommandAction` class, there is also another class named `CallMethodAction` that can be used to invoke a method in the view model from the view without using commands. 
It has a `MethodName` property for specifying the name of the method to call and a `TargetObject` property that needs to be bound to an instance of the class containing the method, i.e. the ViewModel:

```
<Window x:Class="MyNamespace.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation Jump "
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml Jump "
        xmlns:i="clr-namespace:System.Windows.Interactivity;assembly=System.Windows.Interactivity"
        Title="MainWindow" Height="350" Width="525">
        
    <Window.Resources>
	
        <local:MyViewModel x:Key="MyViewModel" />
		
    </Window.Resources>

	
    <StackPanel DataContext="{StaticResource MyViewModel}">

	      <TextBox Text="{Binding Input, UpdateSourceTrigger=PropertyChanged}" />

	      <Button Content="Click here!">
        
            <i:Interaction.Triggers>
            
                <i:EventTrigger EventName="MouseClick" >
                
                    <i:CallMethodAction TargetObject="{Binding}" MethodName="OnMyButtonClicked" />
                    
                </i:EventTrigger>
                
            </i:Interaction.Triggers>
            
        </Button>

    </StackPanel>
    
</Window>
```

`TargetObject="{Binding}"` referring to `DataContext` (MyViewModel)

`MyViewModel.cs`
```
public class MyViewModel{

	public void OnMyButtonClicked()
	{
		/* do something ... */
	}

}
```

**Notes:**
* `CallMethodAction` doesn't support parameters
* `CallMethodAction` class is defined in another assembly and namespace and you will need to add a reference to `Microsoft.Expressions.Interactions.dll` to be able to use it
