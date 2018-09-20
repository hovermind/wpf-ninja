## ElementName Property
Gets or sets the name of the element (wpf control) to use as the binding source object. You specify a string that represents the element you want to bind to. 
This property is useful when you want to bind a property of one control to the property of another control in the same view.

Example:
* to use a `Slider` to control the height of another control in your application
* to bind the `Content` of your control to the `SelectedValue` property of your `ListBox` control

#### CheckBox to Enable Button
```
<Window x:Class="MyApp.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
	
    <Grid>
        <CheckBox Content="Enable Button" Name="myCheckBox" />
        <Button Content="ClickMe" IsEnabled="{Binding ElementName=myCheckBox, Path=IsChecked}"/>
    </Grid>
	
</Window>
```

#### Slider to TextBox
```
<Window x:Class="MyApp.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
	
    <Grid>
	    <Slider Name="mySlider" />
       <TextBox Text="{Binding ElementName=mySlider, Path=Value}"/>
    </Grid>
</Window>
```

#### ListBox to TextBox
```
<Window x:Class="MyApp.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
	
    <Grid>
        <ListBox Margin="12,52,12,110" Name="myListBox">
            <ListBoxItem>c:</ListBoxItem>
            <ListBoxItem>d:</ListBoxItem>
            <ListBoxItem>e:</ListBoxItem>
            <ListBoxItem>f:</ListBoxItem>
            <ListBoxItem>g:</ListBoxItem>
            <ListBoxItem>h:</ListBoxItem>
        </ListBox>
		
		<TextBox Text="{Binding ElementName=myListBox, Path=SelectedItem.Content}"/>
    </Grid>
</Window>
```
