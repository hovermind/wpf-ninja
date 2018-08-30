## WPF Style
A Style is a collection of values that represent properties for a control. By using styles, you can create a reusable representation of a desired control appearance and behavior without writing a new control.


## Style with Explicit Key
`x:Key="MyStyleName"` : only affects the controls to which style is appied
```
<Style x:Key="TitleText">
  <Setter Property="FontSize" Value="26"/>
</Style>

<TextBlock Style="{StaticResource TitleText}" Name="title">Title</TextBlock>
```

## Style with Implicit Key
`TargetType="Control"`: affects all controls of type (i.e. `TextBlock`)
```
<Style TargetType="TextBlock">
  <Setter Property="FontSize" Value="14"/>
</Style>
```
What `TargetType="TextBlock"` does (`TargetType="{x:Type TextBlock}" x:Key="TextBlock"`)
* sets implicit key: `x:Key="TextBlock"`
* specifies the control type (i.e. `TextBlock`) to which setter properties apply (otherwise you must qualify as `Property="Control.Property"` i.e. `Property="TextBlock.FontSize"` instead of `Property="FontSize"`)

**Note:** `x:Type` markup extension has a similar function to the `typeof()` operator in C# 
