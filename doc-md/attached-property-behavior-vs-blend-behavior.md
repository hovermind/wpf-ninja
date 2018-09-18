## Attached Pproperty vs Attached Behavior
"Normal" [Attached Pproperty](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/attached-property.md) is there as metadata for some other piece of code to modify its own behavior based on the presence of that attached property.   
Example:
```
<DockPanel>
  <CheckBox DockPanel.Dock="Top">Hello</CheckBox>
</DockPanel>
```
`DockPanel.Dock` is attached properties for `TextBox` and  metadata for container `DockPanel`. Based on the presence of that metadata (`DockPanel.Dock`), `DockPanel` places the `TextBox` in right place.
Attached properties are like attributes in C# – they don’t do any work themselves, they are just there to influence behavior implemented somewhere else.

**When an attached property has a change handler that acts on the exposed API of the `DependencyObject` to which it is attached, it is an attached behavior.**
In this case it is much more like an extension method in C# – a chunk of code that can be associated with that object to supplement that object’s behavior or functionality without that object’s knowledge.

## Attached Behavior vs Blend Behavior
|  [Attached Behavior](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/attached-behavior.md) | [Blend Behavior](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/blend-behavior.md) |
|--------------------|----------------|
| static class       | non-static class |
| can not be used in visaul designer | can be used in visaul designer |

See: [Attached Behavior vs Blend Behavior](http://briannoyesblog.azurewebsites.net/2012/12/20/attached-behaviors-vs-attached-properties-vs-blend-behaviors/)


