## ItemsControl
WPF has a wide range of controls for displaying a list of data. They come in several shapes and forms and vary in how complex they are and how much work they perform for you. 
The simplest variant is the ItemsControl, which is pretty much just a markup-based loop - you need to apply all the styling and templating, but in many cases, that's just what you need.

The ItemsControl is great when you want full control of how your data is displayed, and when you don't need any of your content to be selectable. 
If you want the user to be able to select items from the list, then you're better off with one of the other controls, e.g. the ListBox or the ListView.

## Items and ItemsSource Properties
The Items and ItemsSource properties are mutually exclusive – it makes sense to set only one of them and any attempt to use both will result in an exception. 
ItemsSource allows us to give the ItemsControl a data source from which to materialize the items it displays. This could be an XML document or a list of CLR objects. 
In practice I have found XML document data sources to be of use only in standalone demos, so I am going to ignore them here. In a production system, 
you will almost certainly want to create view models around your data – whether it’s XML-based or otherwise – and bind your ItemsControl to them instead.

```
<ItemsControl>
    <Label>A Label</Label>
    <Button>A Button</Button>
    <CheckBox>A CheckBox</CheckBox>
</ItemsControl>
```

#### Items Property
```
<ItemsControl>
    <ItemsControl.Items>
        <Label>A Label</Label>
        <Button>A Button</Button>
        <CheckBox>A CheckBox</CheckBox>
    </ItemsControl.Items>
</ItemsControl>
```

#### ItemsSource Property
```
public MainWindow()
{
    InitializeComponent();
 
    this.DataContext = new List<string>
    {
        "London",
        "Amsterdam",
        "Adelaide"
    };
}

<ItemsControl ItemsSource="{Binding}"/>
```

**See:**
* [WPF ItemsControl - The Basics](https://www.dotnetcurry.com/wpf/1160/wpf-itemscontrol-fundamentals-part1)
* [WPF ItemsControl – Advanced](https://www.dotnetcurry.com/wpf/1211/wpf-items-control-advanced-topic)
