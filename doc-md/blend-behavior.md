## Blend Behavior
The problem with [Attached Behaviors](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/attached-behavior.md) is that they are defined entirely through a set of public static variables and methods within a static class. 
As a result, there is not good encapsulating, and you have to be very careful with unsubscribing from events that you subscribe to at the appropriate time so you do not cause memory leaks. Additionally, they are not easy to use in a visual designer. 

As a result, the Microsoft Expression Blend team standardized a new coding structure for defining behaviors that is both design tool friendly, and is better encapsulated (can use non-static class)

## Creating Blend Behavior
With a Blend Behavior, you define a non-static class as your behavior , derived from a Behavior or Behavior base class. 
In your behavior you override a base class method called OnAttached, and you have a base class property called AssociatedObject that gives you a reference to the element to which the behavior is attached.

`ItemClickNavBehavior.cs`
```
publicclass ItemClickNavBehavior : Behavior
{

	public string Destination

	{
		get { return (string)GetValue(DestinationProperty); }
		set { SetValue(DestinationProperty, value); }
	}

	publicstaticreadonly DependencyProperty DestinationProperty = DependencyProperty.Register("Destination", typeof(string), typeof(ItemClickNavBehavior2), new PropertyMetadata(null));

	protectedoverridevoid OnAttached()

	{
		base.OnAttached();

		AssociatedObject.ItemClick += DoNavigation;
	}

	privatevoid DoNavigation(object sender, ItemClickEventArgs e) {
		// ...
	}
}
```

#### Using Blend Behavior
```
<GridView>

	<i:Interaction.Behaviors>

		<local:ItemClickNavBehavior2Destination="Home"/>

	i:Interaction.Behaviors>

GridView>
```

The base classes and the attached property class for Blend behaviors come out of the Blend SDK. The Blend SDK also ships with a number of pre-built, general purpose behaviors such as `InvokeCommandAction`, 
`CallMethodAction`, and `ChangePropertyAction` that can be used in MVVM scenarios. These behaviors actually get attached through a Triggers attached property collection (`EventTrigger`, `DataTrigger`, `TimerTrigger`) instead of Behaviors.

See: [Attached Behavior vs Blend Behavior](http://briannoyesblog.azurewebsites.net/2012/12/20/attached-behaviors-vs-attached-properties-vs-blend-behaviors/)
