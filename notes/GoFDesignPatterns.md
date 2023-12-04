# GoF Design Patterns

## 1. Creational:
The design patterns that deal with the creation of an object.

1.1. **Singleton**
The singleton pattern restricts the initialization of a class to ensure that only one instance of the class can be created.



1.2. **Factory**
The factory pattern takes out the responsibility of instantiating a object from the class to a Factory class.


1.3. **Abstract Factory**
Allows us to create a Factory for factory classes.

1.4. **Builder**
Creating an object step by step and a method to finally get the object instance.

1.5. **Prototype**
Creating a new object instance from another similar instance and then modify according to our requirements.


## 2. Structural:
The design patterns in this category deals with the class structure such as Inheritance and Composition.
2.1. **Adapter**
Provides an interface between two unrelated entities so that they can work together.

2.2. **Composite**
Used when we have to implement a part-whole hierarchy. For example, a diagram made of other pieces such as circle, square, triangle, etc.

2.3. **Proxy**
Provide a surrogate or placeholder for another object to control access to it.

2.4. **Flyweight**
Caching and reusing object instances, used with immutable objects. For example, string pool.

2.5. **Facade**
Creating a wrapper interfaces on top of existing interfaces to help client applications.

2.6. **Bridge**
The bridge design pattern is used to decouple the interfaces from implementation and hiding the implementation details from the client program.

2.7. **Decorator**
The decorator design pattern is used to modify the functionality of an object at runtime.


## 3. Behavioral: 
This type of design patterns provide solution for the better interaction between objects, how to provide lose coupling, and flexibility to extend easily in future.

3.1. **Template Method**
used to create a template method stub and defer some of the steps of implementation to the subclasses.

3.2. **Mediator**
used to provide a centralized communication medium between different objects in a system.

3.3. **Chain of Responsibility**
used to achieve loose coupling in software design where a request from the client is passed to a chain of objects to process them.

3.4. **Observer**
useful when you are interested in the state of an object and want to get notified whenever there is any change.

3.5. **Strategy**
Strategy pattern is used when we have multiple algorithm for a specific task and client decides the actual implementation to be used at runtime.

3.6. **Command**
Command Pattern is used to implement lose coupling in a request-response model.

3.7. **State**
State design pattern is used when an Object change it’s behavior based on it’s internal state.

3.8. **Visitor**
Visitor pattern is used when we have to perform an operation on a group of similar kind of Objects.

3.9. **Interpreter**
defines a grammatical representation for a language and provides an interpreter to deal with this grammar.

3.10. **Iterator**
used to provide a standard way to traverse through a group of Objects.

3.11. **Memento**
The memento design pattern is used when we want to save the state of an object so that we can restore later on.






