## ViewModel
The view model implements properties and commands to which the view can data bind to, and notifies the view of any state changes through change notification events. The properties and commands that the view model provides define the functionality to be offered by the UI, but the view determines how that functionality is to be displayed.

**See:**
* [ViewModel Details](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/enterprise-application-patterns/mvvm#viewmodel)

### Equation of MVVM
```
view.DataContext = ViewModel
```

### ViewModel Instantiation
* **View first composition:** ViewModel is instantiated by view and attached to DataContext
* **ViewModel first composition:** ViewModel is instantiated first and view is constructed by ViewModel (view first composition approach calls default constructor, if you want to create ViewModel instance with parameters, use ViewModel ViewModel first composition)
