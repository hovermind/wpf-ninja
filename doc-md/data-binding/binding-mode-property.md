## Mode Property
**Indicates the direction of the data flow in the binding**. Default value is `Mode.Default` returns the default binding mode value of the target dependency property. 
However, the default value varies for each dependency property. In general, user-editable control properties, such as those of text boxes and check boxes, default to two-way bindings, 
whereas most other properties default to one-way bindings.
```
<TextBox Text="{Binding Name, Mode=OneWay}" /> 

<TextBox Text="{Binding Name, Mode=TwoWay}" /> // TextBox Default
```

Mode values:
* One Way
* Two Way
* One Way to source
* One Time

**Note: there is `Mode` property for [RelativeSource](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/data-binding/binding-relative-source.md) too**
