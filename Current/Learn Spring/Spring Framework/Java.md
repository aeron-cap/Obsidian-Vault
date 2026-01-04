**Fundamentals Quick Run-through**
- Data Types
	- Primitives
		- basic data types that store simple data (int, long, byte, short, char, boolean).
		- ![[Pasted image 20251027212249.png]]
	- Reference
		- objects that contain references to values and/or other objects, or to the special value null to denote the absence of value (String) since the example "Hello World" is a sequence of characters.
		- instance of a class is called an object.
- Declaring Variables in Java
	- **An identifier is a name of any length, consisting of letters, digits, underscore, and dollar sign,** that conforms to the following rules:
		- starts with a letter, an underscore (_), or a dollar sign ($)
		- can’t be a reserved keyword
		- can’t be _true_, _false,_ or _null_
- Arrays
	- reference type
	- type[] identifier = new type[length];
	- ```java
		int[] intArr = { 0,1,2,3,4 }; 
		```
- Java Keywords
	- **Keywords are reserved words that have special meaning in Java.**
	- For example, *public, static, class, main, new, instanceof,* are keywords in Java, and as such, we can’t use them as identifiers (variable names).
- Operators
	- Arithmetic (+, -, *, /, %)
	- Logical (&&, ||, !)
	- Comparator (< , <=, >, =>, = =, !=)
- Java Program Structure
	- Basic unit of a Java program is a Class.
	- For a class to be executable, it must have a main class
- Compiling and Executing a Program
	- javac my_program.java
	- java my_program
	

---

**Java main() Method Explained**
- start of execution
- public static void main(String[] args) { }
	- public - access modifier, global visibility
	- static - method can be accessed straight from the class, we don't have to instantiate an object to have a reference and use it
	- void - doesn't return a value
	- main - JVM looks for this when executing a Java program
	- args - it represents the values received by the method, meaning an array of strings
- different methods of writing the main function
	- public static void main(String []args) { }
	- public strictfp static void main(Srting[] args) { }
		- strictfp - is used for compatibility between processors when working with floating point values.
- Having more than one main() Methods
	- some people use it as a primitive test technique to validate individual classes (JUnit is way more indicated for this activity)
	- we use a MANIFEST.MF to specify the JVM which main() is the entry point
		- Main-Class: mypackage.ClassWithMainMethod
		- located in: _META-INF/MANIFEST.MF_
	

---

**Control Structures**
	- Conditional branches - if/else/else if , ternary operator, and switch
	- Loops - for, while, do while
		- Labeled for loops
		- Iterable forEach() using lambda expressions
	- Branching statements - break and continue


---
- **Java Packages**
	- Java uses packages to group related classes, interfaces, and sub-packages
	- Benefits
		- making related types easier to find
		- avoiding naming conflicts
		- controlling access
- **Creating Packages**
	- package com.example.packages;
	- we should avoid using unnamed or default packages in real-world application
	- **Naming Conventions**
		- names in all lower case
		- period-delimited
		- names are also determined by the company or organization that creates them
		- usually reversing the company URL
	- **Directory Structure
		- each package and sub package has its own directory
		- com . example . app has its own directory structure
- **Using Package Members**
	- Importing : import com.example.app.domain.*;
- **Compiling with javac**
	- javac {class path}
	- javac -classapath . {compile both classes}
	- java com.example.packages.App

---
**Pass by Value and Pass by Reference**
	- Pass by value
		- the caller and the callee method operate on two different variables which are copies of each other. Any changes to one variable don't modify the other.
		- parameters passed to the callee method will be clones of the original parameter
	- Pass by Reference
		- caller and callee operate on the same object
		- the unique identifier of the object is sent to the method
- Parameter Passing
	- Arguments in Java are always passed-by-value.
	- Primitive variables store actual values, whereas non-primitives store the reference variables which point to the addresses of the objects they're referring to. Both values and references are stored in the stack memory.
	- During method invocation, a copy of each argument, whether its a value or reference, is created in stack memory which is then passed to the method.
	- In case of primitives, the value is simply copied inside stack memory which is then passed to the callee method; in case of non-primitives, a reference in stack memory points to the actual data which resides in the heap.
	- Passing Primitive Types
		- Stores directly in stack memory.
	-  Passing Object References
		- All objects in Java are stored in Heap source under the hood.
		- These objects are referred from references called reference variables.
		- Objects are stores in two stages, the reference variables are stores in stack memory, and the object that they're referring to, are stored in Heap memory. 

---
**Varargs**
- Introduced in Java 5 and provide a short-hand for methods that support an arbitrary number of parameters of one type.
- Before Java 5, we must pass all the arguments one by one.
- Varargs help us avoid writing boilerplate code by introducing the new syntax that can  handle an arbitrary number of parameters automatically, its just using an array under the hood.
```java
public String formatWithVarArgs(String... values) {
}
```
- Each method can only have one varargs parameters
- the varargs must be the last parameter
- Using varargs can lead to Heap pollution.
	- Heap pollution is a situation that arises when a variable of a parameterized type refers to an object that is not of that parameterized type.
	- Varargs are safe if and only if we don't store anything in the implicitly created array; and we don't let a reference to the generated array escape the method.
	- When we use varargs, Java compiler creates an array to hold the given parameters, in this case the compiler creates an array with generic type components to gold the arguments.

---
**Hashcode**
- Hashing is a fundamental concept of computer science.
- Efficient hashing algorithms stand behind some of the most popular collections, such as the HashMap and the HashSet.
- Several Map interface implementations are hash tables.
- hashCode() returns an integer value, generated by the hashing algorithm.
- Objects that are equal (according to their equals()) must return the same hash code.
- Whenever it is invoked on the same object more than once during an execution of a Java application, hashCode() must consistently return the same value, provided no modification happened.
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.30</version>
</dependency>
```
- Auto Generate an efficient implementation using ***Lombok***.
```java
@EqualsAndHashCode 
public class User {
    // fields and methods here
}
```
- Annotate the User class with @EqualsAndHashCode
- Alternatively, we can use Apache Commons Lang's HashCodeBuilder class to generate a hashCode() implementation
```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.14.0</version>
</dependency>
```
- it can be implemented like this
```java
public class User {
    public int hashCode() {
        return new HashCodeBuilder(17, 37).
        append(id).
        append(name).
        append(email).
        toHashCode();
    }
}
```
- All implementations use 31 in some form, since it has a nice property. Its multiplication can be replaced by a bitwise shift, which is faster than the standard multiplication.
- **Handling Hash Collisions**
	- This situation is commonly known as a hash collision, and various methods exist for handling it, with each one having their pros and cons. Java’s HashMap uses the separate chaining method for handling collisions.
	- “When two or more objects point to the same bucket, they’re simply stored in a linked list. In such a case, the hash table is an array of linked lists, and each object with the same hash is appended to the linked list at the bucket index in the array.

---
**Switch Statement**
```java
String result;
switch (animal) {
	case "DOG":
		result = "bark";
		break;
	case "CAT":
		result = "meow";
		break;
	default:
		result = "unidentified";
		break;
}
```
- if we forget to write a break, the blocks underneath will be executed.
- switch statement work with byte & Byte, short & Short, int & Integer, char & Character, enum, and String.
- We can't pass null values as an argument to a switch statement.
- If we try to replace case values with different variables, the code won't compile until we mark the variable as final.
- switch operator implements equals() method under the hood.
- JDK 13 brings new version of switch
```java
var result = switch(month) {
    case JANUARY, JUNE, JULY -> 3;
    case FEBRUARY, SEPTEMBER, OCTOBER, NOVEMBER, DECEMBER -> 1;
    case MARCH, MAY, APRIL, AUGUST -> 2;
    default -> 0; 
};
```
- -> instead of colon, and no break keyword needed, comma delimited criteria.
- the yield keyword gives the possibility to obtain fine-grain control over what's happening on the right side of the expression by using code blocks.
```java
var result = switch (month) {
    case JANUARY, JUNE, JULY -> 3;
    case FEBRUARY, SEPTEMBER, OCTOBER, NOVEMBER, DECEMBER -> 1;
    case MARCH, MAY, APRIL, AUGUST -> {
        int monthLength = month.toString().length();
        yield monthLength * 4;
    }
    default -> 0;
};
```
- Return inside the switch expressions
```java
switch (month) {
    case JANUARY, JUNE, JULY -> { return 3; }
    default -> { return 0; }
}
```
- expressions vs statements
	- expressions produces output
	- statements is an instruction to the computer to do something.
- switch expressions will be valid when all possible cases are covered.
- switch statements doesn't need that all cases are covered

---
**forEach**()
- a concise way to iterate over a collection
```java
void forEach(Consumer<? super T> action)
```
- Example of an implementation of for-loop
```java
List names = List.of("Aeron", "Caponpon");

for (String name :  names) {
	LOG.info(name);
}

//for an enhanced version
name.forEach(name -> {
	LOG.info(name);
})
```
- Making the code more declarative in Java functional programming paradigm
```java
List names = List.of("Aeron", "Caponpon");
nams.forEach(name -> logger.info(name));
```
- Iterating over a Map
	- Maps are not iterable, but they do provide their own variant of forEach() that accepts a BiConsumer
	- Java 8 introduces a BiConsumer instead of Consumer in Map's forEach() so that an action can be performed on both the key and value of a Map simultaneously.
```java
Map<Integer, String> namesMap = new HashMap<>();
namesMap.put(1, "Larry");
namesMap.put(2, "Steve");
namesMap.put(3, "James");
```
- now to iterate over namesMap
```java
namesMap.forEach((key, value) -> LOG.info(key + " " + value));
```
 - iterating over a Map by iterating entrySet()
```java
namesMap.entrySet().forEach(entry -> LOG.info(entry.getKey() + " " + entry.getValue()));
entry.getValue();
```
- For large collections, using forEach() with a paralled stream can imrove performance by utilizing multiple CPU cores.
```java
List names = List.of("Aeron", "Caponpon");
names.parallelStream().forEach(LOG::info);
```
- the code above runs in parallel. However, parallel execution may increase resource consumption.
**Limitations of forEach()**
- we can't directly invoke the method on an array.
```java
String[] foodItems = {"rice", "meat"};
foodItems.forEach(food -> logger.info(food));

```
- we can make it compile by converting the array to a stream:
```java
Arrays.stream(foodItems).forEach(food -> logger.info(food));
```
- we can't modify the collection itself using the method:
```java
List<String> names = List.of("Larry", "Steve", "James", "Conan", "Ellen");
names.forEach(name -> {
    if (name.equals("Larry")) {
        names.remove(name);
    }
});
```
- the code above throws a ConcurrentModification Exception error since modifying the collections while iterating over it with forEach() is not allowed.
- forEach() also does not support break or continue
- cannot access the next or previous element
	- will have to use a traditional for loop
**forEach() vs. Traditional for Loop**
- traditional for-loop explicitly defines the control variables, conditions, and increments, while forEach() method abstracts these details.
- enhanced for-loop is an external iterator whereas the new forEach method is internal.

---
**Immutable Objects in Java**
- an object whose internal state remains constant after it has been entirely created
- it means that the public API of an immutable object guarantees us that it will behave in the same way during its whole lifetime
- In Java, variables are mutable by default, meaning we can change the value they hold.
- *final* only forbids us from changing the reference the variable holds, it doesn't protect us from changing the internal state of the object it refers to by using its public API.
- immutable objects are side-effects free

---
**Java Platform Module System (JPMS)**
- A Module is a group of closely related packages and resources along with a new module descriptor file.
- "package for Java Packages"
- Each module is responsible for its resources, like media or configuration files
- **Creating a Module**
	- **Module Descriptor**
		- Name - the name of our module
			- we either use project-style *(my.module)*
			- reverse DNS (_com.baeldung.mymodule_)
		- Dependencies - a list of other modules that this module depends on
		- Public Packages - a list of all packages we want accessible from outside the module
		- Services Offered - we can provide service implementations that can be consumed by other modules
		- Services Consumed - allows the current module to be a consumer of a service
		- Reflection Permissions - explicitly allows other classes to use reflection to access the private members of a package.
	- **Module Types**
		- System Modules - modules listed when we run the list-modules command, include the Java SE and JDK.
		- Application Modules - these are what we usually want to build when we decide to use Modules. They are named and defined in the compiled *module-info.class* file included in the assembled JAR.
		- Automatic Modules - Unofficial modules by adding existing JAR files to the module path. The name of the module will be derived from the name of the JAR. They will have full read access to every other module loaded by the path.
		- Unnamed Module - when a class JAR is loaded onto the classpath, but not the module path, it's automatically added to the unnamed module. It’s a catch-all module to maintain backward compatibility with previously-written Java code.
	- **Distribution**
		- as a JAR file or as an "exploded" compiled project
		- we can only have one module per JAR file.
		- when we setup our build file, we need to make sure to bundle each module in out project as a separate jar.
- **Default Modules**
	- Java 9 we can see that the JDK now has a new structure.
	- These modules are split into four major groups: _java, javafx, jdk,_ and _Oracle_.
	- java --list-modules
	- javafx modules are the FX UI libraries
- **Module Declarations**
	- We need to put a special file at the root of our packages named module-infor.java
```java
	module myModuleName {
	}
```
- Requires
	- our first directive is required
```java
module my.module {
	requires module.name;
}
```
- now my.module has both a runtime and complie-time dependency on module.name