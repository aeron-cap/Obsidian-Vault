- Principle in software engineering which transfers the control of objects or portion of a program to a container or framework. Often used in the context of object-oriented programming.
- Unlike traditional programming where custom code call to a library, IoC enables a framework to take control of the flow of a program and make call to out custom code.
- Abstraction is used by frameworks to enable this behavior.
- Advantages include decoupling the execution of a task from its implementation; making it easier to switch between them; **great modularity, greater ease in testing**.
- We can achieve Inversion of Control through various mechanisms such as: Strategy design pattern, Service Locator pattern, Factory pattern, and **Dependency Injection** (DI).

**Dependency Injection (DI)**
- Pattern that we can use to implement IoC, where the control being inverted is setting an object's dependencies.
- Connecting object with other objects or "injecting", is done by an assembler (Spring Framework) rather than by the objects themselves.
```java
public class Store {
   private Item item;
   
   public Store() {
      item = new ItemImpl1();
   }
}
//this example shows we need to instantiate an implementation of the interface within the Store class itslef.
```
- By using DI, we can rewrite the example without specifying the implementation of the Item we want.
- There are 3 options in Dependency Injections
	`1. Constructor Injection`
```java
public class Controller {
   private Service service;
   
   public Controller(Service service) {
      this.service = service;
   }
   
   public void handleRequest(){
      service.doSomething();
   }
}
```
	2. Setter Injection
```java
public class Controller {
   private Service service;
   
   public void setService(Service service) {
      this.service = service;
   }
   
   public void handleRequest(){
      service.doSomething();
   }
}
```
	3. Field Injection (Loose Coupling)
```java
public class Controller {
   
   @Autowired
   private Service service;

   public void handleRequest(){
      service.doSomething();
   }
}
```
