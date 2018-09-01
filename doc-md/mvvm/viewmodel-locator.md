## ViewModelLocator

## ViewModelLocator Process
* what view is being constructed
* what ViewModel should be instanciated
* instanciate ViewModel
* set `DataContext`

## `ViewModelLocator.cs`
```
public static class ViewModelLocator {

	public static bool GetAutoWireViewModel(DependencyObject obj) {
		return (bool)obj.GetValue(AutoWireViewModelProperty);
	}

	public static void SetAutoWireViewModel(DependencyObject obj, bool value) {
		obj.SetValue(AutoWireViewModelProperty, value);
	}

	public static readonly DependencyProperty AutoWireViewModelProperty =
		DependencyProperty.RegisterAttached("AutoWireViewModel",
		typeof(bool), typeof(ViewModelLocator),
		new PropertyMetadata(false, AutoWireViewModelChanged));
}
```
