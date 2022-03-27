### Introduction
Dependency occurs when an object (a client) relies on another object (a service) to exist. An injector passes the service code to the client. The client object does not build a new object that it requires. Instead, it mocks the service object through an injector. This is knowns as Dependency Injection.

An injection, that is, passing the service to the client, is a primary key for this pattern. The client does not have to create or find the service.

Dependency injection makes unit testing- testing single units of the source code to ensure they are fit for use- efficient. Dependency injection also improves code readability and reuse.

### Table of Contents
- [Prerequisite](#prerequisite)
- [An overview of dependency injection](#an-overview-of-dependency-injection)
- [Interfaces](#interfaces)
- [implementing dependency injection using constructor injection](#implementing-dependency-injection-using-constructor-injection) 
- [Implementing dependency injection using method injection](#implementing-dependency-injection-using-method-injection)
- [Implementing dependency injection using property injection](#implementing-dependency-injection-using-property-injection)
- [Implementing dependency injection using interface based injections](#implementing-dependency-injection-using-interface-based-injections)
- [Merits of dependency injection](#merits-of-dependency-injection)
- [Demerits of dependency injection](#demerits-of-dependency-injection)
- [Conclusion](#conclusion)

### Prerequisites
- The learner should have basic knowledge of programming. 
- They should be equipped with knowledge of the c-sharp programming language.
- Have [Visual studio](https://visualstudio.microsoft.com/downloads/) installed.

### An overview of dependency injection
A class dependent on a client class creates an object of the client class within itself. This complicates the code in a way that:
- The code becomes coupled such that the inner class becomes dependent on the client class.
- Testing the class becomes hard since testing the client class is not easy.
- Changes to the client class will affect the inner class it depends on.
- The inner class cannot be reused since it is tied to the client class.

Dependency Injection allows one to write loosely coupled code -where two objects are independent of each other. This is achieved by separately creating the client's dependency from its behavior. Introducing dependency injection in the above example results in loosely coupled code- the inner class will not be dependent on the client class.

### Interfaces
**Suppose** A client class A requires two service classes, class B and class C, but cannot directly instantiate them. A programmer can introduce an abstraction, i.e., IClass, to client class A rather than implementing classes B and C. This allows one to change IClass interface implementation at any time (for any number of times) without affecting class A's code.

The client expects an interface to be its dependency. The client is only required to know its name and interface. The client is not affected by changes made to the interface.

Dependency injection can be implemented using:
- Constructor injection
- Method injection
- Property injection
- Interface based injection

Let us look at ways we can implement dependency injection.

### Implementing dependency injection using constructor injection
Dependency injection using constructor injection is the most widely used way to implement dependency injection. A parameterized constructor is required in this constructor dependency requiring an argument to be passed during object creation. 

A constructor is a method called when a class object is created. In constructor injection, the client is required to provide a parameter. This makes sure the client instance/object is in a valid state. The dependency is passed as a constructor argument.
The injection component can be used anywhere in the class.

The following is a c-sharp code implementing constructor injection.

```c#
using System;
public interface IClass {
 void Serve();
}
public class Resource1: IClass{
 public void Serve() {
     Console.WriteLine("Resource1 is Initialized"); 
 }
}
public class Resource2: IClass {
 public void Serve() {
     Console.WriteLine("Resource2 is Initialized"); 
 }
}
public class Client {
 private IClass _service;
 public Client(IClass service) {
    _service = service;
 }
 public void Serve() {
    _service.Serve(); 
 }
}
class Program {
 static void Main(string[] args){
 Resource1 r1 = new Resource1();
 Client cA=new Client(r1);
 cA.Serve();

 Resource2 r2 = new Resource2(); 
 cA = new Client(r2);
cA.Serve(); 
 }
}
```

Output

```bash
Resource1 is Initialized
Resource2 is Initialized

```

`public interface IClass` becomes the client class' dependency with the method serve() used to inject the dependency to class serviceA and class serviceB.
Class serviceA and ServiceB implement the Iclass interface as seen in `public class Resource1: IClass` and `public class Resource2: IClass`. They contain a string message to be passed during the serve method call in object creation.

```c#
 Resource1 r1 = new Resource1();
 Client cA=new Client(sA);
 cA.Serve();

 Resource2 r2 = new Resource1(); 
 cA = new Client(r2);
cA.Serve();
```

Here we create objects of class serviceA and serviceB, which are passed as parameters to object of the client class. The client class object cA calls the serve() method that prints the string.

The client class takes an object of type IClient in the constructor where the injection happens, bypassing the service implementing the IClass interface. The dependency is passed during the creation of the client object.

### Implementing dependency injection using method injection
This is a rarely used way to implement dependency injection where the dependency object is supplied/injected through a public method of the client class. A client class implemented interface declares which method will deliver the dependency. The injector delivers the dependence to the client class using the interface implemented by the client class. 

This method is proper when the entire class does not require the dependency, instead only the method with the dependence.

The following is a c-sharp code implementing method injection.

```c# 
using System;

public interface IClass {
 void Serve();
}
public class Resource1: IClass {
 public void Serve() {
       Console.WriteLine("Resource1 is Called"); 
   }
}
public class Resource2: IClass {
 public void Serve() {
       Console.WriteLine("Resource1 is Called"); 
   }
}
public class Client {
 private IClass _service;
 public void Start(IClass service) {
     service.Serve();
   }
}
class Program{
 static void Main(string[] args){
 Resource1 r1 = new Resource1();
 Client client = new Client(); 
 client.Start(r1); 

 Resource2 r2 = new Resource2(); 
 client.Start(r2);
 }
}
```

Output

```bash
Resource1 is Called
service is Called
```
From the above code.
```c#
public class Client {
 private IClass _service;
 public void Start(IClass service) {
     service.Serve();
   }
```
This block of code is used to supply the injection with a start () method used by the client class implemented interface to supply the dependency.
```c#
client.Start(r1); 
client.Start(r2);
```
The client class object passes the service classes objects to the start() method. 

The Service classes A and B implement the Iclass interface, including the  Serve() method. The injector client class uses this method to inject the dependent class services  A and B the client class.

The Client class includes the Start() method to set the object of the type class. The dependency is passed during the creation of the client object.

### Implementing dependency injection using property injection
Also known as Setter Injection, dependency is supplied through a public property of the client class.  
Instantiation of a new object or modification of an already existing object is not required.

The dependency can also be passed through
- using a setter method that stores the dependency in a variable.
- making use of lazy loading, that is, not initializing the concrete class until the property of the dependent class is called.

The following is a c-sharp code implementing property injection.

```c#
using System;

public interface IClass{
 void Serve();
}
public class ServiceA : IClass{
 public void Serve() { 
    Console.WriteLine("ServiceA is Called"); 
 }
}
public class ServiceB : IClass{
 public void Serve() { 
    Console.WriteLine("ServiceB is Called"); 
 }
}
public class Client {
 private IClass _service;
 public IClass Service {
 set { 
    _service = value; 
 }
 }
 public void Serve() {
     _service.Serve(); 
 }
}
class Program{
 static void Main(string[] args){
 Client client = new Client();

 ServiceA sA = new ServiceA(); 
 client.Service = sA;
 client.Serve();

 ServiceB sB = new ServiceB(); 
 client.Service = sB;
 client.Serve();
 }
}
```

Output

```bash
ServiceA is Called
service is Called
```
From the above code.
```c#
public class Client {
 private IClass _service;
 public IClass Service {
 set { _service = value;}
 }
 public void Serve() {_service.Serve();}
}
```

Client class is dependent on the property of type IClient through the `Iclass _service`.
The set method sets the object property where the dependency is injected.
We inject the dependency through a public property of the client class. We use a setter method to set the object of the setter property. The dependency is then passed during client object creation.

Property dependency injection is used when we intend to create the dependency object when it is required.

### Implementing dependency injection using interface-based injections
In interface-based injection, an injector method, provided through an interface, injects the dependency into a client passed to it. The dependency becomes the injector.

An interface-based injection is similar to property injection, using default getter and setter methods. However, interface-based injection sets the interface property using an explicit setter getter interface.

The following is a c-sharp code implementing property injection.

```c#
//interface-based.
using System;

public interface IClass {
    void Serve();
}
public class Service: IClass{
    public void Serve(){
        Console.WriteLine("Service is called.");
    }
}
interface IClassA{
    void Client(IClass Serve);
}
public class Idependency: IClassA{
    IClass _service;
    public void Client(IClass service){
        _service = service;
    }
    public void Serve(){
            _service.Serve();
        }
    }
class program{
     public static void Main(String[] args){
        Idependency interA = new Idependency();
         Service sA= new Service();
       // objA = new Client();
        interA.Serve(sA);
    }
}
```

Output

```bash
Service is called.
```

From the above code.
```c#
interface IClassA{
    void Client(IClass Serve);
}
```

This interface provides the injector method that injects the dependency into the client class, making the dependence the injector.
The dependency is then passed during the creation of the interface class object.

### Merits of dependency injection
As mentioned above, 
- Dependency Injection helps reduces class coupling (where alterations in one class do not force other classes to change).
- Dependency Injection increases code reuse, maintainability and improves testing.
- Dependency Injection can be implemented in various ways, dependency injecting on the application.

### Demerits of dependency injection
Though dependency injection comes a long way in writing loosely coupled and easily maintained code, critics argue that;
- Clients implemented demand configuration where defaults are available.
- Separating a client's behavior from its dependency makes it difficult to trace the code.
- It affects the automation of the integrated development environment since it implements dynamic programming.
- It contributes to framework dependency.
 
### Conclusion
Dependency injection is a powerful technique for handling class interactions in any application. The method is seemingly everywhere and is essential in several frameworks and domains.

Objects and services in dependency injection are easier to create, maintain, and flexible to changes.

Happy coding!
