## XAML
XAML is a declarative markup language (for a .NET Framework application). 
You can create UI elements in XAML and then separate the UI definition from the run-time logic by using code-behind files, joined to the markup through partial class definitions. **XAML directly represents the instantiation of objects in a specific set of backing types defined in assemblies.**
* XAML types are mapped to CLR types to instantiate a run time representation when the XAML for WPF is parsed
* XAML object elements (tag) - represents a type (class defined in WPF assembly)
* Attribute syntax (properties) - properties of an object can often be expressed as attributes of the object element
* Property element syntax - for some properties, attribute syntax is not possible
* property value of underlaying object can be set by attibute and property element tag
* 'attribute value' or 'property element value' can be set by markup extension

Example
```
<StackPanel>
  <Button Content="Click Me"/>
</StackPanel>

// Attribute
<Button Background="Blue" Content="This is a button"/>

// Property Element
<Button>
  <Button.Background><SolidColorBrush Color="Blue"/></Button.Background>
  <Button.Content>This is a button</Button.Content>
</Button>
```

**Notes**
* `.xaml` file is mapped to a partial class
* code behind `.cs` class is also a partial class
* both instantiated partial class (from `.xaml`) and code behind partial class are merged

## XAML root elements and XAML namespaces
A XAML file must have only one root element, in order to be both a well-formed XML file and a valid XAML file.
The root element also contains the attributes `xmlns` & `xmlns:x`. These attributes indicate to type definitions in XAML namespaces.
The xmlns attribute specifically indicates the default XAML namespace. Within the default XAML namespace, object elements in the markup can be specified without a prefix.

For most WPF application:
* `xmlns` : http://schemas.microsoft.com/winfx/2006/xaml/presentation
* `xmlns:x` : http://schemas.microsoft.com/winfx/2006/xaml.

See: 
* [XAML root elements and XAML namespaces](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-overview-wpf#xaml-root-elements-and-xaml-namespaces)
* [XAML Syntax In Detail](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-syntax-in-detail)
