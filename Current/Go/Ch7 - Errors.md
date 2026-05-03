- Go programs express errors with `error` values.
- Errors are just interfaces in code, so we can implement it using structs.

**Panic Function**
- `fmt.Errorf("%w", err)`
- When a function calls a `panic()` function, it yeets control out of the current function and up the call stack until it reaches a function that `defers a recover`
- If no functions calls `recover()`, the program (`goroutine`) crashes
- `log.Fatal` prints a message and exit the program
```go
import (
	"error"
)
errors.New("ERROR STRING")
```
