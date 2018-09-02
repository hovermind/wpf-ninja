## ViewModelLocator

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
		                                     new PropertyMetadata(false, AutoWireViewModelChanged)
						    );
		
        private static void AutoWireViewModelChanged(DependencyObject d, DependencyPropertyChangedEventArgs e) {
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

## Enable AutoWireViewModel in `xaml`
`CustomerListView.xaml` (`ViewModelLocator.AutoWireViewModel="True"`)
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

## ViewModel
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
