## XAML
XAML is a declarative markup language (for a .NET Framework application). 
You can create visible UI elements in the declarative XAML markup, and then separate the UI definition from the run-time logic by using code-behind files, joined to the markup through partial class definitions. 

XAML directly represents the instantiation of objects in a specific set of backing types defined in assemblies.

* XAML object elements (tag) - represents a type (class defined in WPF assembly)
* Attribute syntax (properties) - properties of an object can often be expressed as attributes of the object element
* Property element syntax - for some properties, attribute syntax is not possible
* a XAML tag represents a class in XAML library (XAML processor reads tags and creates corresponding objects)
* property value of underlaying object can be set by attibute and property element tag
* 'attribute value' or 'property element value' can be set by markup extension

**Note**
* `.xaml` file is mapped to a partial class
* code behind `.cs` class is also a partial class
* both instantiated partial class (from `.xaml`) and code behind partial class are merged

Example
```
<StackPanel>
  <Button Content="Click Me"/>
</StackPanel>

<Button Background="Blue" Content="This is a button"/>

<Button>
  <Button.Background><SolidColorBrush Color="Blue"/></Button.Background>
  <Button.Content>This is a button</Button.Content>
</Button>
```

## XAML root elements and XAML namespaces
A XAML file must have only one root element, in order to be both a well-formed XML file and a valid XAML file.
The root element also contains the attributes `xmlns` & `xmlns:x`. These attributes indicate to type definitions in XAML namespaces.
The xmlns attribute specifically indicates the default XAML namespace. Within the default XAML namespace, object elements in the markup can be specified without a prefix. For most WPF application scenarios the default XAML namespace is mapped to the WPF namespace http://schemas.microsoft.com/winfx/2006/xaml/presentation. The `xmlns:x` attribute indicates an additional XAML namespace, which maps the XAML language namespace http://schemas.microsoft.com/winfx/2006/xaml.

See: [Details](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-overview-wpf)

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
