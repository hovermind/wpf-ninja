## Triggers
A Trigger allows you to dynamically change the appearance and behavior of a control without creating a new control.
For example, suppose you have multiple ListBox controls in your application and want the items in each ListBox to be bold 
and red when they are selected. Your first instinct might be to create a class that inherits from ListBox and override 
the OnSelectionChanged method to change the appearance of the selected item, but a better approach is to add a trigger to a style of 
a ListBoxItem that changes the appearance of the selected item. A trigger enables you to change property values or take actions based 
on the value of a property. An EventTrigger enables you to take actions when an event occurs.

See
* [DataTrigger Class](https://docs.microsoft.com/en-us/dotnet/api/system.windows.datatrigger)
* [Use DataTriggers to Apply Property Values](https://docs.microsoft.com/en-us/dotnet/framework/wpf/data/data-templating-overview#use-datatriggers-to-apply-property-values)
