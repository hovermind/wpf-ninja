## ResourceDictionary
Every framework-level element has a Resources property, which is the property that contains the resources as a ResourceDictionary. 
A resource is an object that can be reused in different places in your application. 

WPF supports different types of resources (from actual information to a hierarchy of WPF controls). These resources are primarily two types: 
* XAML resources (i.e. brushes and styles)
* resource data files (non-executable data files that an application needs, i.e .json, .csv)

You can define resources: 
* locally for a control
* locally for the entire page/window
* globally for the entire application

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



