## XAML - Extensiable Application Marup Language
XAML is a declarative markup language (for a .NET Framework application). You can create UI elements in XAML and then separate the UI definition from the run-time logic by using code-behind files.

* XAML taga are mapped to CLR types to instantiate a run time representation (as partial class)
* [Object Element Syntax](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-syntax-in-detail#object-element-syntax) - Object element syntax is the XAML markup syntax that instantiates a CLR class or structure by declaring an XML element.
* [Attribute Syntax](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-syntax-in-detail#attribute-syntax-properties) - properties of an object can often be expressed as attributes of the object element
* [Property Element Syntax](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-syntax-in-detail#property-element-syntax) - for some properties, attribute syntax is not possible
* property value of underlaying object can be set by attibute or property element tag
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
* instantiated partial class (from `.xaml`) and code behind partial class are merged

## XAML root elements
A XAML file must have only one root element, in order to be both a well-formed XML file and a valid XAML file.
The root element also contains the attributes `xmlns` & `xmlns:x`. These attributes indicate to type definitions in XAML namespaces. Within the default XAML namespace (`xmlns`), object elements in the markup can be specified without a prefix.

## XAML namespaces
XAML namespace implies both a scope of uniqueness for the markup usages, and also influences how markup entities are potentially backed by specific CLR namespaces and referenced assemblies.
* URIs as namespace identifiers (convention)
* using prefixes to provide a means to reference multiple namespaces from the same markup source
* `xmlns` => default namespace
* `xmlns:prefix` => other namespace than default

For most WPF application:
* `xmlns` : http://schemas.microsoft.com/winfx/2006/xaml/presentation
* `xmlns:x` : http://schemas.microsoft.com/winfx/2006/xaml

**See:**
* [Mapping CLR Namespaces to XML Namespaces in an Assembly](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml#mapping-clr-namespaces-to-xml-namespaces-in-an-assembly)
* [XAML Syntax In Detail](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-syntax-in-detail)
