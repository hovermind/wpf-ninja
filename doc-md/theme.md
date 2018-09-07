## Theme
A typical WPF application might have multiple UI resources that are applied throughout the application. Collectively, this set of resources
can be considered the theme for the application. WPF provides support for packaging UI resources as a theme by using a resource dictionary that is encapsulated as the `ResourceDictionary` class.

* themes are defined by using the styling and templating mechanism
* theme resources are stored in embedded resource dictionaries (in the same assembly as the code itself or in a side-by-side assembly)
* theme becomes the last place to look when searching for the style of an element. Typically, the search will begin by walking up the element, then look in the application resource collection and finally query the system
