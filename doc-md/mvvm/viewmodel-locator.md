## ViewModelLocator
A view model locator is a custom class that manages the instantiation of view models and their association to views. 
the `ViewModelLocator` class has an attached property, `AutoWireViewModel`, that's used to associate view models with views. In the view's XAML, this attached property is set to true to indicate that the view model should be automatically connected to the view.
The `AutoWireViewModel` property is a bindable property that's initialized to false, and when its value changes the `OnAutoWireViewModelChanged` event handler is called.

## ViewModelLocator Process
* what view is being constructed
* what ViewModel should be instanciated
* instanciate ViewModel
* set `DataContext`

## Create ViewModelLocator Class
`ViewModelLocator.cs`
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
		                                     new PropertyMetadata(false, OnAutoWireViewModelChanged)
						    );
		
        private static void OnAutoWireViewModelChanged(DependencyObject d, DependencyPropertyChangedEventArgs e) {
            if(DesignerProperties.GetIsInDesignMode(d)){
                return;
	    }
	    
            var viewType = d.GetType();
            var viewTypeName = viewType.FullName;
            var viewModelTypeName = viewType + "Model";
            var viewModelType = Type.GetType(viewModelTypeName);
            var viewModel = Activator.CreateInstance(viewModelType);
	    
            ((FrameworkElement)d).DataContext = viewModel;
        }
}
```

## Create ViewModel
`CustomerListViewModel.cs`
```
public class CustomerListViewModel
{
	private ICustomersRepository _repository = new CustomersRepository();
	
	public CustomerListViewModel()
	{
		if (DesignerProperties.GetIsInDesignMode(new System.Windows.DependencyObject()))
		{
			return;
		}

		Customers = new ObservableCollection<Customer>( _repository.GetCustomersAsync().Result);
	}

	public ObservableCollection<Customer> Customers { get; set; }
}
```

## Enable AutoWireViewModel in `xaml`
`CustomerListView.xaml` (=> `local:ViewModelLocator.AutoWireViewModel="True"`)
```
<UserControl x:Class="Demo.CustomerListView"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
             xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
             xmlns:local="clr-namespace:Demo"
	     local:ViewModelLocator.AutoWireViewModel="True"
             mc:Ignorable="d" 
             d:DesignHeight="300" d:DesignWidth="300" >
    <Grid>
        <DataGrid ItemsSource="{Binding Customers}" />
    </Grid>
</UserControl>
```

## `CustomerListView.xaml.cs`
```
public partial class CustomerListView : UserControl
{
    public CustomerListView()
    {
        InitializeComponent();
    }
}
```
