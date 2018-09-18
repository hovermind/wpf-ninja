## Attached Behavior
Attaching a behavior to an object simply means making the object do something that it would not do on its own.
The idea is that you set an attached property on an element so that you can gain access to the element from the class that exposes the attached property. 
Once that class has access to the element, it can hook events on it and, in response to those events firing, make the element do things that it normally would not do. 
It is a very convenient alternative to creating and using subclasses, and is very XAML-friendly.

When an attached property has a change handler, it become attached behavior.
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

**Note:** Attached Behavior does not show up in Blend under behaviors, and thus can not be attached if your are using Blend


## Usage of Attached Behavior
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
