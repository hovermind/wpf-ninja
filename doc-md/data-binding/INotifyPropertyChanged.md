## Why do We Need `INotifyPropertyChanged`
WPF data binding doesn't need `INotifyPropertyChanged` interface in order to work but It is needed to notify of changes in property values of `ViewModel` to view (after they are first presented).

In MVVM pattern, `ViewModel` class is not directly tied to the View, instead ViewModel's fields are exposed via Properties with change notifiaction where the 'change notifiaction' is provided through `INotifyPropertyChanged`.

When implemented, the interface communicates to `Control` and `ViewModel`- any change will be reflected on both directions:
* `INotifyPropertyChanged` has an event `PropertyChangedEventHandler PropertyChanged` which will be fired by WPF control i.e. `TextBox` when `TextBox` input is changed and therefore bounded `ViewModel` property value will be updated
* when underlying data is changed, you will invoke `PropertyChanged` event in setter of your `ViewMddel` property so that new value is shown to the bounded control i.e. `TextBox`

## Implementing `INotifyPropertyChanged`
`PersonViewModel.cs`
```
public class PersonViewModel : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    private string givenName;
	private string familyName;
		
    public string GivenName
    {
        get => givenName;
        set
        {
            if (value != givenName)
            {
                givenNames = value;
                OnPropertyChanged("GivenName"); // updates given name TextBox
                OnPropertyChanged("FullName");  // updates full name TextBox
            }
        }
    }

    public string FamilyName
    {
        get => familyName;
        set 
        {
            if (value != familyName)
            {
                familyName = value;
                OnPropertyChanged("FamilyName"); // updates given name TextBox
                OnPropertyChanged("FullName");   // updates full name TextBox
            }
        }
    }

    public string FullName => $"{GivenName} {FamilyName}";

    public virtual void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
```
GivenName & FamilyName properties of PersonViewModel are bound to `TextBox`. If any of these changes, FullName will be updated accordingly.

## Using Fody Assembly Weaver
* Fody: https://www.nuget.org/packages/Fody/
* PropertyChanged2.Fody: https://www.nuget.org/packages/PropertyChanged2.Fody/
* PropertyChanged2.Fody wiki: https://github.com/Fody/PropertyChanged/wiki/

**Step 1: Install Fody (Nuget Package)**    
**Step 2: Add `FodyWeavers.xml` in project folder (Latest version of Nuget does not allow to put xml in the project folder)**
```
<?xml version="1.0" encoding="utf-8" ?>
<Weavers>

</Weavers>
```
**Step 3: Install PropertyChanged2.Fody**   
**Step 4: Build & then add  `<PropertyChanged/>` in `FodyWeavers.xml`**
```
<?xml version="1.0" encoding="utf-8" ?>

<Weavers>

  <PropertyChanged />
  
</Weavers>
```

**Step 5: Buiuld & add `[ImplementPropertyChanged]` annotation**
```
[ImplementPropertyChanged]
public class MyViewModel
{

    // properties go here
}
```
**Step 6: Build & It should work**
