## Attached Property
Attached property (a special kind of DependencyProperties) is the property of a control that needs the data from another control in a specific context. 
It allows you to attach a value to an object that does not know anything about this value. For example an element that is aligned by a parent layout panel.

To set the value of an attached property, add an attribute in XAML with a prefix of the element that provides the attached property
```
<Canvas>
    <Button Canvas.Top="20" Canvas.Left="20" Content="Click me!"/>
</Canvas>
```
