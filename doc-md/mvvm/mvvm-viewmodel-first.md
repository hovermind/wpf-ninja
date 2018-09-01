## ViewModel First Approach
`MainWindow.xaml.cs`
```
public MainWindow()  
{  
    InitializeComponent();  
    DataContext = new EmployeeViewModel();  
}
```
**Note:** here `DataContext` is the property of `MainWindow.xaml`
