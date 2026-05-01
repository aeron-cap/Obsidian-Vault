**Go Program Structure**
1. `package main()` lets the GO compiler know that this is not a library but a standalone program
2. `import "fmt"` is a formatting package from the standard library 
3. `func main()` is the main entry point for a Go program

**2 kinds of errors**
1. **Compilation Error** means that the compiler can't translate our code into machine code due to it having syntax errors. It generally better to have compilation errors since we can catch them before the program executes.
2. **Runtime Error** means that an error that occurs while the program is running. This is generally worse since it is unexpected behavior.

**Fast and Compiled**
- Go programs are fast and compiled, meaning they are faster than interpreted languages like Python, JavaScript, and Ruby. However, Go is don't run quite as fast as other compiled languages like C, Rust, and Zig counterparts. Despite this, it compiles much faster than other compiled languages. It a mixture of fast and fast, meaning, faster than interpreted languages, and faster to compile than other compiled languages.

**Type Sizes**
- Integers, uints, floats, and complex numbers all have type sizes.
	- Signed integers
		- `int - int64` (`int32` is the default)
	- Unsigned integers
		- `uint - uint64`, `uintptr` (`uint64` is the default)
	- Signed Decimal numbers
		- `float32` and `float64` (`float64` is default)
	- Complex numbers
		- `complex64` and `complex128`
- Some types are easy to convert
	- `floatval := 1.2`
	- `intval := int64(floatval) //becomes 1 since it truncates the decimal portion`

**Compiled vs. Interpreted**
- We can run compiled programs without the original source code. Unlike interpreted languages where we need a separate interpreter in a server to run the source code.
![[Pasted image 20260501110708.png]]

**Go Runtime**
- There is always a chunk of Go code included when we compile which is the Go runtime. This manages memory.
- This implements garbage collection, concurrency, stack management, and other critical features.
- Analogous to `libc`
- **[[Garbage Collection]]**
	- automatic memory management
	- attempts to reclaim memory that is allocated by the program but isn't referenced anymore