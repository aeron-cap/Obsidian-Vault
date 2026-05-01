- Functions are made like this
```go
func function_name(VAR TYPE, VAR TYPE) RETURN_TYPE {
}
```

**Unit Testing**
- In Go, tests are indicated by filenames with `*_test.go`

**Passing Variables by Value**
- Variables in Go are passed by value, except a few data types. Meaning when a variable is passed into a function, that function receives a copy.

**Return**
- `func function_name () (x int, y int) {}`
- `x, _ := function_name()`
- The Go compiler will return an error on unused variable declarations, so we need to ignore everything we don't intend to use
- We can use Named Return Values like this:
```go
func function_name(x int) (y int, z, int) {
  y = 1
  z = 2
  return y, z
}
```
- Named Returns are better for Documentation purposes
- **Explicit Returns**
	- Returns are named in the return statement and return type
- **Implicit Returns**
	- Blank returns with named return types
- **Early Returns**
	- **Guard Clauses**
		- Ability to return early from a function, or continue to a loop to make nesting one-dimensional

**Functions as Values**
- We can use functions as another functions arguments if they support them

**Anonymous Functions**
- Functions with no names
- Can be used to create a quick closure

**Defer**
- Allows a function to be executed automatically just before its enclosing function returns
- Used to clean up unused database connections, file handlers and the like
- Multiple Defers are executed **last-in-first-out** (stack).

**Block Scope**
- Go is not function scope, its block scoped
- Variables are only accessible inside its scope declaration `{ }`

**Closure**
- Function that references variables from outside its own function body

**Currying**
- Concept from functional programming
- involves partial application of functions

