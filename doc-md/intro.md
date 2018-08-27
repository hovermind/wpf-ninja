## XAML
XAML is a declarative markup language (for a .NET Framework application). 
You can create visible UI elements in the declarative XAML markup, and then separate the UI definition from the run-time logic by using code-behind files, joined to the markup through partial class definitions. 

XAML directly represents the instantiation of objects in a specific set of backing types defined in assemblies.

* a XAML tag represents a class in XAML library
* XAML parser/processor process XAML tags and creates corresponding objects (class instances)
* property value of underlaying object (instanciated by XAML processor by reading XAML tags) can be set by attibute and property tag (property element tag)
* an attribute decorates UI element where property element set/get value (state of instantiated object)
* attribute value or property element value can be set by markup extension

Example
```
<StackPanel>
  <Button Content="Click Me"/>
</StackPanel>
```
## Markup Extension
A markup extension is a feature of XAML whereby you specify an object reference (string tokens), the markup extension processes the string and return the object to a XAML loader.
```
<Page.Resources>
    <SolidColorBrush x:Key="MyBrush" Color="Green"/>
</Page.Resources>
```

**Using markup extension for Attribute**
```
<Button Background="{StaticResource MyBrush}"/>
```

**Using markup extension for Property Element**
```
<Setter Property="Background" Value="{StaticResource MyBrush}" /> 
```

Nesting of multiple markup extensions is supported, and each markup extension will be evaluated deepest first
```
<Setter Property="Background"  
  Value="{DynamicResource {x:Static SystemColors.ControlBrushKey}}" /> 
```
See: [WPF Markup Extension Details](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/markup-extensions-and-wpf-xaml)
