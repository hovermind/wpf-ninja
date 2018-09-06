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
