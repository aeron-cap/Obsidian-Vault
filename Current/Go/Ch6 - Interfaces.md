- Interfaces allow devs to focus on what a type does rather than how its built.
- It allows us to write reusable code by defining methods that different types can share.
- Interfaces are just collections of methods signatures.

**Type Assertions**
```go
c, ok := s.(circle)
if ok {
	//do something
}
```
- We can also do type switches
```go
switch v := num.(type) {
case int:
	//do something
case string:
	//do something
default:
	//do something
}
```
- 