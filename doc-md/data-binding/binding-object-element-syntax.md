## Object Element Syntax
Although ou can specify most of the properties of the `Binding` class in [Markup Extension Usage](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/data-binding/binding-markup-extension-usage.md), `MultiBinding` and `PriorityBinding` 
do not support a XAML extension syntax. You would instead use property elements.

When to use:
* markup extension does not support your scenario
* non-string type for which no type conversion exists

```
<TextBlock Name="myconvertedtext" >
  <TextBlock.Text>
    <Binding Path="TheDate" Converter="{StaticResource MyConverterReference}"/>
  </TextBlock.Text>
</TextBlock>
```

#### Example
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.Resources>
        <local:EmployeeViewModel x:Key="EmployeeViewModel" />
    </Window.Resources>
	
	<TextBlock DataContext="{StaticResource EmployeeViewModel}">
	  <TextBlock.Text>
		<Binding Path="Name"/>
	  </TextBlock.Text>
	</TextBlock>
	
</Window>
```
