
## `Validation.ErrorTemplate` Property
`Validation.ErrorTemplate="{StaticResource errorTemplate}"`
```
<TextBox Text="{Binding Username, ValidatesOnExceptions=True, UpdateSourceTrigger=PropertyChanged}" 
	Validation.ErrorTemplate="{StaticResource errorTemplate}"/>
```

## ErrorTemplate
#### Error Message Inside TextBox
```
<ControlTemplate x:Key="errorTemplate">
  <Border BorderBrush="OrangeRed" BorderThickness="2">
    <Grid>
      <AdornedElementPlaceholder/>
      <TextBlock Text="{Binding [0].ErrorContent}" Foreground="OrangeRed"
             VerticalAlignment="Center" HorizontalAlignment="Right"
             Margin="0,0,4,0"/>
    </Grid>
  </Border>
</ControlTemplate>


// Set ErrorTemplate property of TextBox
<TextBox Text="{Binding Username, ValidatesOnExceptions=True, UpdateSourceTrigger=PropertyChanged}" 
	Validation.ErrorTemplate="{StaticResource errorTemplate}"/>
```

#### Red Dot on Right Side
When hovering on dot (`ToolTip` property of `Ellipse`) => `ToolTip="Invalid Input"`
```
<ControlTemplate x:Key="errorTemplate">
	<DockPanel>
		<Ellipse DockPanel.Dock="Right" Margin="2,0" Width="10" Height="10" ToolTip="Invalid Input">
			<Ellipse.Fill>
				<LinearGradientBrush>
					<GradientStop Color="#11FF1111" Offset="0" />
					<GradientStop Color="#FFFF0000" Offset="1" />
				</LinearGradientBrush>
			</Ellipse.Fill>
		</Ellipse>
		<AdornedElementPlaceholder />
	</DockPanel>
</ControlTemplate>


// Set ErrorTemplate property of TextBox
<TextBox Text="{Binding Username, ValidatesOnExceptions=True, UpdateSourceTrigger=PropertyChanged}" 
	Validation.ErrorTemplate="{StaticResource errorTemplate}"/>
```

## Implicitly Setting ErrorTemplate in Style
`<TextBox ... Validation.ErrorTemplate="{StaticResource errorTemplate}"/>` is explicit & **below is implicit** (both does the same)
```
<ControlTemplate x:Key="errorTemplate">
    //... ... ...
</ControlTemplate>


<Style TargetType="TextBox">
    //... ... ...
    <Setter Property="Validation.ErrorTemplate" Value="{StaticResource errorTemplate}" />
</Style>
```
