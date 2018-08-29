Resources are typically definitions of some object that you expect to use more than once. To refer to a XAML resource later, you specify a key for a resource that acts like its name. You can reference a resource throughout an app or from any XAML page within it.

Resources can be defined: 
* locally for a control
* locally for the entire page/window
* globally for the entire application

**See:** [ResourceDictionary and XAML resource references](https://docs.microsoft.com/en-us/windows/uwp/design/controls-and-patterns/resourcedictionary-and-xaml-resource-references)

## Resource in Separate `.xaml` File
The global application resource dictionary is in the App.xaml file. In this file you can include several resource dictionaries as a Merged Dictionary.

#### Step-1 Resource in `.xaml` File
`MyTextStyle.xaml`
```
<ResourceDictionary 
  xmlns=" http://schemas.microsoft.com/winfx/2006/xaml/presentation "
  xmlns:x=" http://schemas.microsoft.com/winfx/2006/xaml ">
  
  <Style TargetType="{x:Type TextBlock}" x:Key="TextStyle">
    <Setter Property="FontSize" Value="22" />
    <Setter Property="Foreground" Value="#58290A" />
  </Style>
  
</ResourceDictionary>
```
**Notes:**
* ResourceDictionary is the root element in the Xml file, so we need to define the default namespaces
* There is ResourceDictionary template is Visual Studio : Right Click > Add Item > ResourceDictionary

#### Step-2 `ResourceDictionary.MergedDictionaries` in `App.xaml`
```
<Application x:Class="MyApp"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    StartupUri="Window1.xaml">
    
    <Application.Resources>
	
      <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
		
          <ResourceDictionary Source="MyTextStyle.xaml" />
	  
	  <ResourceDictionary Source="xyz.xaml" />
		  
        </ResourceDictionary.MergedDictionaries>
      </ResourceDictionary>
	  
      <!-- other styles can appear in the resource dictionary too -->
      <Style ...>
        <Setter Property="Background" Value="#ddd" />
      </Style>
	  
    </Application.Resources>
    
</Application>
```
**Notes:**
* Expression Blend has options to extract design as resource in a file and update existing resource file
* resource in `App.xaml` is Anti-Pattern, since App.xaml files should never directly contain resources because it leads to a completely unmanageable mess

## Resource in Window
Available to pages in the window

## Resource in Page
Available to that page only
```
<Page
    x:Class="MSDNSample.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">

    <Page.Resources>
        <x:String x:Key="greeting">Hello world</x:String>
        <x:String x:Key="goodbye">Goodbye world</x:String>
    </Page.Resources>

    <TextBlock Text="{StaticResource greeting}" Foreground="Gray" VerticalAlignment="Center"/>
</Page>
```
## Resource in Control
Available to that control and child control only






