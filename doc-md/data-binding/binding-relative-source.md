## RelativeSource Properties
[RelativeSource Class](https://docs.microsoft.com/en-us/dotnet/api/system.windows.data.relativesource) exposes three properties to set:
 exposes three properties to set:
* `Mode` : an enum with four values
* `AncestorType` : when mode is `FindAncestor` then define what type of ancestor
* `AncestorLevel` : when mode is `FindAncestor` then what level of ancestor (it's optional)

Usage Example:
```
 <TextBlock Text="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType = {x:Type Border}, AncestorLevel = 2}, Path = Name}" />
```

## [RelativeSourceMode Enum](https://docs.microsoft.com/en-us/dotnet/api/system.windows.data.relativesourcemode)
Synatx: `<object property="{Binding RelativeSource={RelativeSource ModeVal} ...}" />`    

`Mode Enum Values:`
* `Self`
* `FindAncestor`
* `TemplatedParent`
* `PreviousData`

**Note: RelativeSourceMode is different that Binding Mode (OneWay, TwoWay)**

### Mode == `Self`
Instead of:
```
<Rectangle Fill="Red" Name="rectangle" 
                Height="100" Stroke="Black" 
                Canvas.Top="100" Canvas.Left="100"
                Width="{Binding ElementName=rectangle,
                Path=Height}" />
```
We can avoid `ElementName=rectangle`:
```
<Rectangle Fill="Red" Height="100" 
               Stroke="Black" 
               Width="{Binding RelativeSource={RelativeSource Self},
               Path=Height}" />
```
Using `Parent` property for `Path`
```
 <TextBlock Width="{Binding RelativeSource={RelativeSource Self},
               Path=Parent.ActualWidth}"/>
```

### Mode == `FindAncestor`
```
<Canvas Name="Parent0">
    <Border Name="Parent1"
             Width="{Binding RelativeSource={RelativeSource Self},
             Path=Parent.ActualWidth}"
             Height="{Binding RelativeSource={RelativeSource Self},
             Path=Parent.ActualHeight}">
        <Canvas Name="Parent2">
            <Border Name="Parent3"
            Width="{Binding RelativeSource={RelativeSource Self},
           Path=Parent.ActualWidth}"
           Height="{Binding RelativeSource={RelativeSource Self},
              Path=Parent.ActualHeight}">
               <Canvas Name="Parent4">
               <TextBlock FontSize="16" 
               Margin="5" Text="Display the name of the ancestor"/>
               <TextBlock FontSize="16" 
                 Margin="50" 
            Text="{Binding RelativeSource={RelativeSource  
                       FindAncestor,
                       AncestorType={x:Type Border}, 
                       AncestorLevel=2}, Path=Name}" 
                       Width="200"/>
                </Canvas>
            </Border>
        </Canvas>
     </Border>
   </Canvas>
```

### Mode == `TemplatedParent`
```
<Window.Resources>
<ControlTemplate x:Key="template">
        <Canvas>
            <Canvas.RenderTransform>
                <RotateTransform Angle="20"/>
                </Canvas.RenderTransform>
            <Ellipse Height="100" Width="150" 
                 Fill="{Binding 
            RelativeSource={RelativeSource TemplatedParent},
            Path=Background}">

              </Ellipse>
            <ContentPresenter Margin="35" 
                  Content="{Binding RelativeSource={RelativeSource  
                  TemplatedParent},Path=Content}"/>
        </Canvas>
    </ControlTemplate>
</Window.Resources>
    <Canvas Name="Parent0">
    <Button   Margin="50" 
              Template="{StaticResource template}" Height="0" 
              Canvas.Left="0" Canvas.Top="0" Width="0">
        <TextBlock FontSize="22">Click me</TextBlock>
    </Button>
 </Canvas>
```

### [Mode == `PreviousData`](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/relativesource-markupextension#remarks)

