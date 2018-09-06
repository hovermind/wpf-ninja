## Data Template
DataTemplate is about the presentation of data. A DataTemplate enables you to customize how data is displayed on a control. For example, a DataTemplate can be used to specify how data is displayed in a ListBox Or by using a DataTemplate, you can create a ComboBox in which each item contains a check box.

See: [Data Template Details](http://www.wpftutorial.net/datatemplates.html)

## DataTemplate Usage
```
<DataTemplate x:Key="myItemsTemplate">
  <StackPanel>
    <TextBlock Text="{Binding Path=Name}" />
    <TextBlock Text="{Binding Path=Id}"/>
  </StackPanel>
</DataTemplate>

<DataTemplate x:Key="myContentTemplate">
  <TextBlock Text="{Binding}" FontSize="12" FontWeight="Bold" TextWrapping="Wrap"></TextBlock>
</DataTemplate>
```

#### ItemsControl : `ItemTemplate="{StaticResource myItemsTemplate}"` (ItemsControl => i.e. `ListBox`)
```
<ListBox Width="400" Margin="10"
         ItemsSource="{Binding Source={StaticResource personList}}"
         ItemTemplate="{StaticResource myItemsTemplate}"/>
```

#### ContentControl : `ContentTemplate="{StaticResource myContentTemplate}"` (ContentControl => `Button`)
```
<ContentControl ContentTemplate="{StaticResource myContentTemplate}" Content="..."/>
```

## [The DataType Property](https://docs.microsoft.com/en-us/dotnet/framework/wpf/data/data-templating-overview#the-datatype-property)
The `DataTemplate` class has a DataType property that is very similar to the `TargetType` property of the `Style` class. You can use `DataType` instead of `x:Key`:
```
<DataTemplate DataType="{x:Type local:Task}">
  <StackPanel>
    <TextBlock Text="{Binding Path=TaskName}" />
    <TextBlock Text="{Binding Path=Description}"/>
    <TextBlock Text="{Binding Path=Priority}"/>
  </StackPanel>
</DataTemplate>
```

**When `DataType` is used**
* `DataTemplate` gets applied automatically to all Task objects used in `ItemsControl`(`ContentControl` does not use the above `DataTemplate` automatically) 
* `x:Key` is set implicitly
* both `DataType` & `x:Key` are used => you are overriding the implicit x:Key and the `DataTemplate` would not be applied automatically


