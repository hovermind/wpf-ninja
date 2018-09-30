## `ToolTip` Property
#### Setting `ToolTip` in control itself
```
<TextBox Text="{Binding Username, ValidatesOnDataErrors=True, UpdateSourceTrigger=PropertyChanged}" 
    ToolTip="{Binding ...}"/>

<TextBox Text="{Binding Username, ValidatesOnDataErrors=True, UpdateSourceTrigger=PropertyChanged}" 
    ToolTip="{Binding ErrorCollection[Username]}"/>
```

#### Setting `ToolTip` in `Style.Triggers`
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
