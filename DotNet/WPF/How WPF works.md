- At its core, a xaml View file is connected to a Binding/DataContext.
- The DataContext is more commoly known as the ViewModel.
- The ViewModel contains properties which will be binded to a xaml control and vice versa.
- it up to your viewmodel class to add logic to the xaml property.
#### How to call methods on XAML?
- simply create a method on the viewmodel, then set that method to a property with data type of `RelayCommand` or a custom like `CentryCommand`.
	- these are already built datatypes that define a function, which allows you to bind a function to the xaml.

