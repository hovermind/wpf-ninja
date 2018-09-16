## DependencyProperty for Custom Controls
To bind data to the property of a control (i.e. `Background` property of `Button` control), that property must be of type `DependencyProperty`.
WPF controls inherit from `DependencyObject` and properties (i.e. `Background`, `Width` etc.) are of type `DependencyProperty` and therefore they support data binding.   

If you create a custom control and want to have data binding support then properties of that custom control must be of type `DependencyProperty`. Typically custom controls inherits from `UserControl` class (`UserControl` << `Control` << `DependencyObject`)

#### See: [Creating Custom Control with DependencyProperty](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/user-control.md#creating-usercontrol)
