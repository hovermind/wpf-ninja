## Attached Property
Attached property (a special kind of DependencyProperties) is the property of a control that needs the data from another control in a specific context.
* an attached property is intended to be used as a type of global property that is settable on any object
* purpose of an attached property is to allow different child elements to specify unique values for a property that is actually defined in a parent element
* attached properties are typically defined as a specialized form of dependency property that does not have the conventional property "wrapper"
* attached properties are a XAML concept, whereas dependency properties are a WPF concept
* attached property is not necessarily part of the CLR, but a XAML processor must be able to set those values when XAML is parsed

Syntax: `AttachedPropertyProvider.PropertyName` ( usage is somewhat similar to a static property)    
Example: `DockPanel.Dock`
```
<DockPanel>
  <CheckBox DockPanel.Dock="Top">Hello</CheckBox>
</DockPanel>
```
`DockPanel.Dock` is attached property of `CheckBox`

See: 
* [Attached Properties Overview](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/attached-properties-overview)
* [How to Create an Attached Property](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/attached-properties-overview#how-to-create-an-attached-property-a-namehowdoicreateattachedpropertiesa)

## [Custom Attached Property](https://docs.microsoft.com/en-us/windows/uwp/xaml-platform/custom-attached-properties#code-example)
```
public class GameService : DependencyObject
{
    public static readonly DependencyProperty IsMovableProperty = DependencyProperty.RegisterAttached("IsMovable", typeof(Boolean), typeof(GameService), new PropertyMetadata(false));
    
    public static void SetIsMovable(UIElement element, Boolean value)
    {
        element.SetValue(IsMovableProperty, value);
    }
    
    public static Boolean GetIsMovable(UIElement element)
    {
        return (Boolean)element.GetValue(IsMovableProperty);
    }
}
```
**Using your custom attached property in XAML**
```
<UserControl
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:uc="using:UserAndCustomControls">
  
  <Image uc:GameService.IsMovable="True" />
  
</UserControl>
```
