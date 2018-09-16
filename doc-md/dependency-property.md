## What is DependencyProperty?
WPF provides a set of services that can be used to extend the functionality of a type's property. Collectively, these services are typically referred to as the WPF property system. 
**A property that is backed by the WPF property system is known as a dependency property.**

Dependency properties are properties of classes that derive from DependencyObject. The main difference is, that the value of a normal .NET property is read directly from a private member in your class, whereas the value of a DependencyProperty is resolved dynamically when calling the GetValue() method that is inherited from DependencyObject.

**The nicest thing about them is that they have all the plumbing for data binding built in**. If you bind something to them, they'll notify it when they change.

**When you set a value of a dependency property it is not stored in a field of your object, but in a dictionary provided by the base class DependencyObject**. The key of an entry is the name of the property and the value is the value you want to set.

The purpose of dependency properties is to provide a way to compute the value of a property based on the value of other inputs. These other inputs might include system properties such as themes and user preference, just-in-time property determination mechanisms such as data binding and animations/storyboards, multiple-use templates such as resources and styles, or values known through parent-child relationships with other elements in the element tree.

Example:
```
public partial class FieldUserControl : UserControl
{

  public String Label
  {
    get { return (String)GetValue(LabelProperty); }
    set { SetValue(LabelProperty, value); }
  }
  
  public static readonly DependencyProperty LabelProperty = DependencyProperty.Register("Label", typeof(string), typeof(FieldUserControl), new PropertyMetadata(""));

  public FieldUserControl()
  {
    InitializeComponent();
	
	  Label = "default label";
  }
}
```

**See:** 
* [Property functionality provided by a dependency property](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/dependency-properties-overview#property-functionality-provided-by-a-dependency-property)
* [Custom Dependency Properties](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/custom-dependency-properties)

**Notes:**
* **WPF Property System (`DependencyObject` class + `DependencyProperty` class)**: primary function is to compute the values of properties and to provide system notification about values that have changed
* **Dependency Property**: a property that is backed by the WPF property system is known as a dependency property
* **`DependencyObject` class**: `DependencyObject` as a base class enables objects to use the dependency properties. In other words, in order for a class to to have a property of type `DependencyProperty`, the class must inherit from `DependencyObject`
* **`DependencyProperty` class**: `DependencyProperty` backs CLR property to extend property functionality i.e. data binding support (CLR properties are backed by private fields & can not be bind to controls, while a property of type `DependencyProperty` can be bind to controls)
* **Data Binding**: the nicest thing about `DependencyProperty` is that it has all the plumbing for data binding built-in. If you bind something to it, it will notify when value changes (although the ViewModel must implement `INotifyPropertyChanged` interface to get notified)
* **WPF Controls**: WPF controls inherit from `DependencyObject` and properties i.e. `Background`, `Width` etc. are of type `DependencyProperty` (therefore `Background`, `Width` etc. support data binding)

## DependencyProperty for Custom Controls
To bind data to the property of a control (i.e. `Background` property of `Button` control), that property must be of type `DependencyProperty`.
WPF controls inherit from `DependencyObject` and properties (i.e. `Background`, `Width` etc.) are of type `DependencyProperty` and therefore they support data binding.   

If you create a custom control and want to have data binding support then properties of that custom control must be of type `DependencyProperty`. Typically custom controls inherits from `UserControl` class (`UserControl` << `Control` << `DependencyObject`)

#### See: [Creating Custom Control with DependencyProperty](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/user-control.md#creating-usercontrol)
