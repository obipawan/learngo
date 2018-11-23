---
layout: default
---

# Defer

Go has a special statement called defer which schedules a function call to be run after the function completes.

```go
func first() {
    fmt.Println("1st")
}
func second() {
    fmt.Println("2nd")
}
func main() {
    defer second()
    first()
}
```

`defer` is often used when resources need to be free'd in some way. For example when we open a file we need to make sure to close it later. With `defer`

```go
f, _ := os.Open(filename)
defer f.Close()
```

This constructs would seem cleaner and easier to understand as a `Close` call is near to the `Open` call.
`Defer` functions run even if a runtime `panic` occurs.

```go
defer func() {
    str := recover()
    fmt.Println(str)
}()
panic("panic in the disco")
```

# Panic & Recover
A `panic` typically means something went unexpectedly wrong. Mostly we use it to fail fast on errors that shouldn’t occur during normal operation, or that we aren’t prepared to handle gracefully.
A common use of `panic` is to abort if a function returns an error value that we don’t know how to (or want to) handle. 
A `panic` immediately stops execution.

```go
func panicFunc(a, b float32) float32 {
	if b == 0 {
		panic("divide by zero!")
	}
	return a / b
}
```

A `recover` function stops a `panic` and returns the value that was passed to the `panic` call.

[Pointers >](./pointers.html)