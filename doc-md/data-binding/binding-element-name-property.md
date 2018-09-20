## Path Property
Refers to the property of scope/context object (context is set by `DataContext` or `Source` property). The default is `null`.


**With Source:** `Text="{Binding Source="{StaticResource MyViewModel}", Path=X"}"`    
**With DataContext:** `Text="{Binding Path=X"}"`    
**Syntactic Sugar:** `Text="{Binding X"}"`    

**Notes:**
* `Text="{Binding}"` means current data source or `DataContext`
* `Text="{Binding Path=.}"` is equivalent to `Text="{Binding}"` 

See:
* [Path Property Details](https://docs.microsoft.com/en-us/dotnet/api/system.windows.data.binding.path?view=netframework-4.7.2#remarks)
* [PropertyPath XAML Syntax](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/propertypath-xaml-syntax)
