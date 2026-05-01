- Constants are declared using the `const` keyword
- They can be used to assign primitive types but not complex types like slices, maps or structs.
- We cannot declare a constant that can only be computed on runtime

**Formatting Strings in Go**
- `fmt.Printf()` prints a formatted string to `stdout`
- `fmt.Sprintf()` returns a formatted string
	- Default Representation
		- `%v` prints any value
		- `%s` prints string
		- `%d` prints integers
		- `%f` prints floats
			- can also do `%.nf` where n is the places to round off
		- `%t` for bool
		- `%T` to print the type
		- `\n` for newline in `stdout`

**Runes and String Encoding**
- `rune` is `int32` large enough to hold a Unicode code point
- a "character" is is a single byte, ASCII
- when we `len()` an emoji for example, we get 4