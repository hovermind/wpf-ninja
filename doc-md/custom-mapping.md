## Custom Mapping
```
namespace SDKSample {  
    public class ExampleClass : ContentControl {  
        public ExampleClass() {  
           //...  
        }  
    }  
}  
```
`clr-namespace:` &  `assembly=`
```
<Page x:Class="WPFApplication1.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary">  
  ...  
  <custom:ExampleClass/>  
...  
</Page>  
```
`assembly=` can be omitted if the clr-namespace referenced is being defined within the same assembly as the application code that is referencing the custom classes.
```
<Page x:Class="WPFApplication1.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:custom="clr-namespace:SDKSample">  
  ...  
  <custom:ExampleClass/>  
...  
</Page> 
```
