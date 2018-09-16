## Change Notification by Inheriting `DependencyObject`
To update view when underlaying data is changed can be achieved by [INotifyPropertyChanged](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/data-binding/INotifyPropertyChanged.md). 

Another way to notify property value change is inheriting from `DependencyObject` and make all `ViewModel` properties dependencyproperties. They notify without implementing `INotifyPropertyChanged`. 
All the WPF GUI side Properties are dependency Properties and part of thiere ability is change notification.
```
public class MyViewModel : DependencyObject {

	public static readonly DependencyProperty NameProperty = DependencyProperty.Register("Name", typeof(string), typeof(MyViewModel), new PropertyMetadata(""));

	public string Name
	{
		get { return (string) GetValue(HelloWorldProperty); }
		set { SetValue(NameProperty, value); }
	}
}
```

## Using Fody Assembly Weaver
* Fody: https://www.nuget.org/packages/Fody/
* AutoDependencyProperty.Fody: https://www.nuget.org/packages/AutoDependencyProperty.Fody/

**Step 1: Install Fody (Nuget Package)**    
**Step 2: Install AutoDependencyProperty.Fody**   


**Step 3: Buiuld & add `[AutoDependencyProperty]` annotation**
```
public class MyViewModel
{

	[AutoDependencyProperty(Options = FrameworkPropertyMetadataOptions.BindsTwoWayByDefault)]
	public bool Name { get; set; }
}
```
**Step 4: Build & It should work**
