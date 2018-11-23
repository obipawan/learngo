---
layout: default
---

# Errors

In Go it’s idiomatic to communicate errors via an explicit, separate return value. This contrasts with the exceptions used in languages like Java and Ruby and the overloaded single result / error value sometimes used in C. Go’s approach makes it easy to see which functions return errors and to handle them using the same language constructs employed for any other, non-error tasks. [ref](https://gobyexample.com/errors)

By convention, errors are the last return value and have type error, a built-in interface.

`errors.New` constructs a basic error value with the given error message.

```go
func div(a, b float32) (float32, error) {
	if b == 0 {
		return -1, errors.New("Divide by zero not allowed")
	}
	return (a / b), nil
}
```

A `nil` value in the error position indicates that there was no error.

### Custom Errors

It’s possible to use custom types as `errors` by implementing the `Error()` method on them. Here’s a variant on the example above that uses a custom type to explicitly represent an argument error.

```go
type customError struct {
	message   string
	errorCode int
}

func (cust *customError) Error() string {
	return fmt.Sprintf("%s: errorCode = %d", cust.message, cust.errorCode)
}

func div(a, b float32) (float32, error) {
	if b == 0 {
		return -1, &customError{"Divide by zero not allowed", -1}
	}
	return (a / b), nil
}
```

[Goroutines & Channels >](./goroutineschannels.html)