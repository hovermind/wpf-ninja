## Model-View-ViewModel Pattern
The Model-View-ViewModel (MVVM) pattern is an application pattern that isolates the user interface from the underlying business logic. 
MVVM belongs to a class of patterns called Separated Presentation. These patterns provide a clean separation between the UI and 
the rest of the application. This improves the testability of the application and allows the application and its UI to evolve more 
easily and independently. The MVVM pattern consists of the following parts:
* The Model, which provides a view-independent representation of your business entities. The design of the model is optimized for the logical relationships and operations between your business entities, regardless of how the data is presented in the user interface.
* The View class which is the user interface. It displays information to the user and fires events in response to user interactions.
* The ViewModel class, which is the bridge between the view and the model. Each View class has a corresponding ViewModel class. The ViewModel retrieves data from the Model and manipulates it into the format required by the View. It notifies the View if the underlying data in the model is changed, and it updates the data in the Model in response to UI events from the View.

**Relationship between the View, the ViewModel, and the Model**   

![mvvm-diagram](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/mvvm/mvvm-diagram.png)


**See:**
* [MVVM Details](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/enterprise-application-patterns/mvvm)
* [MVVM Best Practices](https://blog.rsuter.com/recommendations-best-practices-implementing-mvvm-xaml-net-applications/)
