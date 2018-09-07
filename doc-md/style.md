## WPF Style
A Style is a collection of values that represent properties for a control. By using styles, you can create a reusable representation of a desired control appearance and behavior without writing a new control.

See: [Styling and Templating](https://docs.microsoft.com/en-us/dotnet/framework/wpf/controls/styling-and-templating)

## Style with Explicit Key: `x:Key="xxxx"`
`x:Key="MyStyleName"` : only affects the controls to which style is appied
```
<Style x:Key="TitleText">
  <Setter Property="FontSize" Value="26"/>
</Style>

<TextBlock Style="{StaticResource TitleText}" Name="title">Title</TextBlock>
```

## Style with Implicit Key: `TargetType="{x:Type Control}"` or `TargetType="Control"`
`TargetType="{x:Type Control}"`: affects all controls of that Type (i.e. `TextBlock`)
```
<Style TargetType="TextBlock">
  <Setter Property="FontSize" Value="14"/>
</Style>
```
What `TargetType="{x:Type TextBlock}"` / `TargetType="TextBlock"` does:
* sets implicit key: `x:Key="TextBlock"`
* specifies the control type (i.e. `TextBlock`) to which setter properties apply (otherwise you must qualify as `Property="Control.Property"` i.e. `Property="TextBlock.FontSize"` instead of `Property="FontSize"`)

**Notes:** 
* `x:Type` markup extension has a similar function to the `typeof()` operator in C#
* not all properties support string for `TargetType` (i.e. `TargetType="TextBlock"`), in that case you have to use `TargetType="{x:Type TextBlock}"`

## Extending Styles: `BasedOn`
`BasedOn="{StaticResource {x:Type TextBlock}}"` => inheriting from system `TextBlock` style
```
<Style BasedOn="{StaticResource {x:Type TextBlock}}" x:Key="TitleText">

  <Setter Property="prop-name" Value="x"/>

</Style>
```

`BasedOn="{StaticResource myBaseStyle}"` => inheriting from custom style
```
<Style BasedOn="{StaticResource myBaseStyle}" x:Key="TitleText">

  <Setter Property="prop-name" Value="x"/>

</Style>
```

**If both base style and subStyle has `TargetType` property:
* both `TargetType` must be same type
* subStyle `TargetType` must be derived type of baseStyle `TargetType`
```
<Style TargetType="TextBlock" x:Key="myBaseStyle" >

  <Setter Property="prop-name" Value="x"/>

</Style>

<Style BasedOn="{StaticResource myBaseStyle}" TargetType="TextBlock" x:Key="mySubStyle" >

  <Setter Property="prop-name" Value="x"/>

</Style>
```
