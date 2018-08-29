## ResourceDictionary
Every framework-level element has a Resources property, which is the property that contains the resources as a ResourceDictionary. 

**Each resource in a resource dictionary must have a unique key** (typically the key is a string). When you define resources in markup, you assign the unique key through the `x:Key` Directive
```
<Page.Resources>
    <SolidColorBrush x:Key="MyBrush" Color="Green"/>
</Page.Resources>
```
**key can be**
* implicit: `x:Key="MyKey"`
* explicit: `TargetType="Control"`

After defining a resource, you can reference it to be used for a property value by using resource markup extension syntax
```
<Button Background="{StaticResource MyBrush}"/>
```
XAML loader processes the value `{StaticResource MyBrush}` for the Background property on Button, the resource lookup logic checks:   
>resource dictionary for the Button >> if not found >>   
>resource dictionary for the Page >> if not found >>   
>resource dictionary for the Window >> if not found >>   
>resource dictionary for the Application
