## `ToolTip` Property
Tooltip property can be set in:
* Control
* ErrorTemplate
* Style Trigger

## Setting `ToolTip` in control itself
```
<TextBox Text="{Binding Username, ValidatesOnDataErrors=True, UpdateSourceTrigger=PropertyChanged}" 
    ToolTip="{Binding ...}"/>

<TextBox Text="{Binding Username, ValidatesOnDataErrors=True, UpdateSourceTrigger=PropertyChanged}" 
    ToolTip="{Binding ErrorCollection[Username]}"/>
```

## Setting `ToolTip` in `Style.Triggers`
Implicit Style
```
<Style TargetType="TextBox">
  <Style.Triggers>
    <Trigger Property="Validation.HasError" Value="true">
      <Setter Property="ToolTip" Value="{Binding RelativeSource={x:Static RelativeSource.Self}, Path=(Validation.Errors).CurrentItem.ErrorContent}" />
    </Trigger>
  </Style.Triggers>
</Style>
```
## Setting `ToolTip` in `ErrorTemplate`
```
<ControlTemplate x:Key="errorTemplate">
	<DockPanel>
		<Ellipse ToolTip="{Binding Path="(Validation.Errors).CurrentItem.ErrorContent" RelativeSource="{x:Static RelativeSource.Self}"}">
			<Ellipse.Fill>

			</Ellipse.Fill>
		</Ellipse>
		<AdornedElementPlaceholder />
	</DockPanel>
</ControlTemplate>
```
