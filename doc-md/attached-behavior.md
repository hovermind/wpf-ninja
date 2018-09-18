## Attached Behavior
**A behavior is a chunk of code you write that can be used in XAML by attaching it to some element through attached properties**. The behavior can use the exposed API of the element to which it is attached to add functionality to that element or other elements in the visual tree of the view. In this way, they are the XAML equivalent of C# extension methods. Extension methods allow you to define additional methods for some class in C# without modifying the class definition itself, and they work against the exposed API of the class. Behaviors allow you to add functionality to an element by writing that functionality in the behavior class and attaching it to the element as if it was part of the element itself.

See: [Attached Behavior vs Blend Behavior](http://briannoyesblog.azurewebsites.net/2012/12/20/attached-behaviors-vs-attached-properties-vs-blend-behaviors/)

* attaching a behavior to an object simply means making the object do something that it would not do on its own
* when an attached property has a change handler, it become attached behavior
* all behaviors (attached behavior, blend behavior) are in some sense “attached behaviors” because they use Attached Properties in XAML to hook the behavior in to some element within the XAML
* you can hook events and properties from a given control type and feed those down into a view model in a standardized fashion

**Note:** Attached Behavior does not show up in Blend under behaviors, and thus can not be attached if your are using Blend

## Creating Attached Behavior
`DigitsOnlyBehavior.cs`
```
public static class DigitsOnlyBehavior
{
	public static bool GetIsDigitOnly(DependencyObject obj)
	{
		return (bool)obj.GetValue(IsDigitOnlyProperty);
	}

	public static void SetIsDigitOnly(DependencyObject obj, bool value)
	{
		obj.SetValue(IsDigitOnlyProperty, value);
	}

	public static readonly DependencyProperty IsDigitOnlyProperty = DependencyProperty.RegisterAttached("IsDigitOnly", typeof(bool), typeof(DigitsOnlyBehavior), new PropertyMetadata(false, OnIsDigitOnlyChanged));

	private static void OnIsDigitOnlyChanged(object sender, DependencyPropertyChangedEventArgs e)
	{
		// you can hook handler method to sender.Event (if available)
	}
}
```

**Using above attached behavior in a `TextBox`**
```
<TextBox behaviors:DigitsOnlyBehavior.IsDigitOnly="True" />
```

## Usage of Attached Behavior
`TreeViewItemBehavior.cs`
```
// Exposes attached behaviors that can be applied to TreeViewItem objects

public static class TreeViewItemBehavior
{

    public static bool GetIsBroughtIntoViewWhenSelected(TreeViewItem treeViewItem)
    {
        return (bool)treeViewItem.GetValue(IsBroughtIntoViewWhenSelectedProperty);
    }

    public static void SetIsBroughtIntoViewWhenSelected(TreeViewItem treeViewItem, bool value)
    {
        treeViewItem.SetValue(IsBroughtIntoViewWhenSelectedProperty, value);
    }

    public static readonly DependencyProperty IsBroughtIntoViewWhenSelectedProperty = DependencyProperty.RegisterAttached("IsBroughtIntoViewWhenSelected", typeof(bool), typeof(TreeViewItemBehavior), new UIPropertyMetadata(false, OnIsBroughtIntoViewWhenSelectedChanged));

    static void OnIsBroughtIntoViewWhenSelectedChanged(DependencyObject depObj, DependencyPropertyChangedEventArgs e)
    {
        TreeViewItem item = depObj as TreeViewItem;
        if (item == null)
            return;

        if (e.NewValue is bool == false)
            return;

        if ((bool)e.NewValue)
            item.Selected += OnTreeViewItemSelected;
        else
            item.Selected -= OnTreeViewItemSelected;
    }

    static void OnTreeViewItemSelected(object sender, RoutedEventArgs e)
    {
        // Only react to the Selected event raised by the TreeViewItem
        // whose IsSelected property was modified. Ignore all ancestors
        // who are merely reporting that a descendant's Selected fired.
        if (!Object.ReferenceEquals(sender, e.OriginalSource))
            return;

        TreeViewItem item = e.OriginalSource as TreeViewItem;
        if (item != null)
            item.BringIntoView();
    }
}
```

TreeView style
```
<TreeView.ItemContainerStyle>

  <Style TargetType="{x:Type TreeViewItem}">
  
    <!-- This Setter applies an attached behavior to all TreeViewItems -->
    <Setter Property="local:TreeViewItemBehavior.IsBroughtIntoViewWhenSelected" Value="True" />

    <!-- These Setters bind a TreeViewItem to a PersonViewModel -->
    <Setter Property="IsExpanded" Value="{Binding IsExpanded, Mode=TwoWay}" />
    <Setter Property="IsSelected" Value="{Binding IsSelected, Mode=TwoWay}" />
    <Setter Property="FontWeight" Value="Normal" />
	
    <Style.Triggers>
      <Trigger Property="IsSelected" Value="True">
	  
        <Setter Property="FontWeight" Value="Bold" />
		
      </Trigger>
    </Style.Triggers>
	
  </Style>
  
</TreeView.ItemContainerStyle>
```
