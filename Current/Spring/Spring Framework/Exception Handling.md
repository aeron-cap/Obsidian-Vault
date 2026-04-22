```java
              ---> Throwable <--- 
              |    (checked)     |
              |                  |
              |                  |
      ---> Exception           Error
      |    (checked)        (unchecked)
      |
RuntimeException
  (unchecked)
```
- Exceptions are just Java objects with all of them extending from Throwable.
- There are three main categories of exceptional conditions
	- Checked exceptions
		- Java compiler requires us to handle.
		- IOException and ServletException to name a few.
	- Unchecked exceptions / Runtime exceptions
		- Java compiler does not require us to handle
		- If we create an exception that extends RuntimeException, it will unchecked; otherwise it will be checked.
		- NullPointerException, IllegalArgumentException, and SecurityException
	- errors
		- irrecoverable conditions
			- library incompatibility, infinite recursion, or memory leaks.

**Handling Exceptions**
- throw
```java
public int getPlayerScore(String playerFile)
  throws FileNotFoundException {
 
    Scanner contents = new Scanner(new File(playerFile));
    return Integer.parseInt(contents.nextLine());
}
```
- FileNotFoundException is a checked exception.
- parseInt can throw a NumberFormatException, but because it is unchecked, we aren't required to handle it.

- try-catch
	- we can handle it by either rethrowing it or performing recovery steps.
	- finally - it executes regardless of whether an exception occurs, and this is where the finally keyword comes in.
	- can put multiple catch
		- in Java 7 onwards, we can do this
```java
public int getPlayerScore(String playerFile) {
    try (Scanner contents = new Scanner(new File(playerFile))) {
        return Integer.parseInt(contents.nextLine());
    } catch (IOException | NumberFormatException e) {
        logger.warn("Failed to load score!", e);
        return 0;
    }
}
```

**Throwing Exceptions**
- Throwing a checked exception
```java
public List<Player> loadAllPlayers(String playersFile) throws TimeoutException {
    while ( !tooLong ) {
        // ... potentially long operation
    }
    throw new TimeoutException("This operation took too long");
}
```
- Throwing an unchecked exception
```java
public List<Player> loadAllPlayers(String playersFile) throws TimeoutException {
    if(!isFilenameValid(playersFile)) {
        throw new IllegalArgumentException("Filename isn't valid!");
    }
   // ...
}
```
- Wrapping and Rethrowing
```java
public List<Player> loadAllPlayers(String playersFile) 
  throws PlayerLoadException {
    try { 
        // ...
    } catch (IOException io) { 		
        throw new PlayerLoadException(io);
    }
}
```

**Anti-Patterns**
- Swallowing Exceptions
	- don't do this, the least we can do i log an error, or throw a different exception
```java
public int getPlayerScore(String playerFile) {
    try {
        // ...
    } catch (IOException e) {
        throw new PlayerScoreException(e);
    }
}
```
- here we include the *IOException* as the cause of *PlayerScoreException*
- another way to swallow exceptions is to return from the finally block. This is bad since by returning abruptly, the JVM will drop the exception, even if it was thrown from the try block.
- if we throw another exception in the *finally* block, it will erase the original exception from the catch block.

**Common Exceptions and Errors**
- Checked Exceptions
	- IOException - something on the network, filesystem, or database failed.
- Runtime Exceptions
	- ArrayIndexOutOfBoundsException - we treid to access non-existent array index.
	- ClassCastException - we tried to perform an illegal cast, like converting String into List.
	- IllegalArgumentException - one of the provided method or constructor is invalid
	- IllegalStateException - like the state of the object is invalid
	- NullPointerException - we tried to reference a null object.
	- NumberFormatException - tried to convert a String to number, but contained illegal characters.
- Errors
	- StackOverflowError - stack trace is too big. Can happen on Massive applications, usually means that we have some infinite recursion happening to our code.
	- NoClassDefFoundError - class failed to load either due to not being on the classpath or due to failure in static initialization.
	- OutOfMemmoryError - JVM doesn't have any more memory available to allocate.