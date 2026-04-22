**Object Oriented Programming**
- we use to model real-life entities.
- **Classes** are blueprints or templates for objects, we use them to describe types of entities.
- **Objects** are living entities, created from classes, they contain states within their fields and present certain behaviors with their methods.

**Classes**
- represents a definition or a type of object. In Java, classes can contain, fields, constructors, and methods.
```java
class Car {
	//fields
	String type;
	String model;
	String color;
	int speed;
	
	//constructor
	Car(String type, String model, String color) {
		this.type = type;
		this.model = model;
		this.color = color;
	}
	
	//methods
	int increaseSpeed(int increment) {
		this.speed = this.speed + increment;
		return this.speed;
	}
}
```
- we use fields to hold the state
- constructor to create objects from this class
- every Java class has an empty constructor by default, if we did not implement our specific implementation as we did above, it will use the default constructor.
```java
Car(){}
```
- the constructor simply initializes all fields of the object with their default values, strings are initialized to null and integers to zero.
- to sum up, class properties are described by fields, which contain the state of objects, and behavior using methods.

**Objects**
- While classes are translated during compile time, objects are created from classes at runtime.
- Objects of a class are called instances, we initialize them with constructors.
```java
Car auris = new Car("Toyota", "Auris", "blue");
auris.increaseSpeed(20);
```
- we can and should define access control to our classes, its constructors, fields, and methods.

**Access Modifiers**
- package-private is default access modifier, which allows access to the class from any other class in the same package.
- we usually use public modifier for constructors to allow access from all other objects.
- **Classes usually have public modifiers, but we tend to keep our fields private**
- we can keep Fields public or private. We achieve this with specific methods called getters and setters.
```java
public class Car {
    private String type;
    // ...

    public Car(String type, String model, String color) {
       // ...
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getSpeed() {
        return speed;
    }

    // ...
}
```
- class is marked public, we can use it on any package.
- constructor is public, we can create an object from this class inside any other object.
- fields are marked private which means they are not accessible from our object, but we provide access to them through getters and setters.
- **we use access control to encapsulate the state of the object.**

---

**Concrete Class**
- a class that we can create an instance of, using the new keyword.
- a full implementation of its blueprint, all of its methods are complete.
- examples are, *HashMap*, *HashSet*, *ArrayList*, and *LinkedList*.

**Java Abstraction vs. Concrete Classes**
- In **Java** we can achieve abstraction using **interfaces and abstract classes.**
- **Interface** is a blueprint for a class.
```java
interface Driveable {
	void honk();
	void drive();
}
```
- it uses the interface keyword instead of class, since Driveable has unimplemented methods, we can't instantiate it with the new keyword.
- **Map, List and Set** are interfaces provided by the JDK.
- **Abstract Classes**
	- abstract class is a class that has unimplemented methods, though it can usually have both
	- we mark abstract classes with the keyword abstract.
	- since Vehicle class has an unimplemented method, honk, we won't be able to use the new keyword.
```java
public abstract class Vehicle {
    public abstract String honk();

    public String drive() {
        return "zoom";
    }
}
```
- **Concrete Class**
	- in contrast with abstract classes, concrete class don't have unimplemented methods. Whether the implementations are inherited or not, so long as each method has an implementation, the class is concrete.
	- int he code below, the FancyCar class provides an implementation for honk and it inherits the implementation of drive from Vehicle.
	- as such, it has no unimplemented methods, therefore we can create a FancyCar class instance using the new keyword.
```java
public class FancyCar extends Vehicle implements Driveable {
    public String honk() { 
        return "beep";
    }
}

FancyCar car = new FancyCar();
```
- Simply put, all classes which are not abstract, we can call concrete classes.

---
**Access Modifiers in Java**
- There are four access modifiers: **public, private, protected**, and **default(no keyword)**, also that top-level classes can only use public or default access modifiers, at the member level, we can all four.
- **Default**
	- all members are visible within the same package, but aren't accessible from within the same package, but not in other packages.
- **Public***
	- making it available to the whole world
	- all other classes in all packages will be able to use it
	- least restrictive access modifier
- **Private**
	- accessible from the same class only
	- most restrictive access modifier, core concept of encapsulation.
		- all data will be hidden from the outside world
- **Protected**
	- between public and private
	- we can access the members of the same package as well as from all subclasses of its class, even if they lie on other packages
	![[Pasted image 20251112223820.png]]
- **Canonical Order of Modifiers**
	- Java Language Specification (JLS) recommends a standard canonical order.
	- Field Modifiers
		- Annotation
		- public/protected/private
		- static
		- final
		- transient
		- volatile
```java
@Id
private static final long ID = 1;
```
	- Class Modifiers
		- Annotation
		- public/protected/private
		- abstract
		- static
		- final
		- strictfp
	- Method Declaration
		- Annotation
		- public/protected/private
		- abstract
		- static
		- final
		- synchronized
		- native
		- strictfp

---
**Constructors**
- https://www.baeldung.com/java-constructors