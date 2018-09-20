## Referring CLR-Object
You can create CLR-object instances as static resource and use in xaml.

* **xml namespace :** `xmlns:local="clr-namespace:<name_space_name>;assembly=<assembly_name>"` (`xmlns:local` => xml namspace name can be anything i.e. instead of "local" we can use "custom" or something else)
* **`assembly=` can be omitted** if the `clr-namespace` referenced is being defined within the same assembly as the application code that is referencing the custom classes
* **`<local:MyViewModel x:Key="MyViewModel">`** : `var MyViewModel = new MyViewModel()`
* **`<local:MyViewModel>`** : `new MyViewModel()`

```
namespace MyApp { 
    public class MyViewModel {  
         // Props ...
         // Ctor 
    }  
}  

<Page x:Class="MyApp.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:local="clr-namespace:MyApp"> 
    
  <Page.Resources>
      <local:MyViewModel xKey="MyViewModel">
  <Page.Resources>
   
   <StackPanel Orientation=Vertical>
   
       <StackPanel.DataContext>
           <Binding Source="{StaticResource MyViewModel}" />
       </StackPanel.DataContext>
       
       <TextBox Text="{Binding Name}" />
       
   </StackPanel>
</Page>  
```

**Notes:**
* when instantiating ViewModel as static resource, default parameter-less constructor will be called i.e. `new MyViewModel()` (can not pass arguments in constructor)

