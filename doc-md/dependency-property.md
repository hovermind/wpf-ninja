## What is Dependency Property?
WPF provides a set of services that can be used to extend the functionality of a type's property. Collectively, these services are typically referred to as the WPF property system. 
**A property that is backed by the WPF property system is known as a dependency property.**

Dependency properties are properties of classes that derive from DependencyObject. The main difference is, that the value of a normal .NET property is read directly from a private member in your class, whereas the value of a DependencyProperty is resolved dynamically when calling the GetValue() method that is inherited from DependencyObject.

The nicest thing about them is that they have all the plumbing for data binding built in. If you bind something to them, they'll notify it when they change.

