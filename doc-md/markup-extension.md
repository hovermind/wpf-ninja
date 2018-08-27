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
