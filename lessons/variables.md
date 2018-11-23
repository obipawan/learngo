---
layout: default
---

# Variables And Constants

A variable is a storage location, with a specific type and an associated name. They're explicitly declared and used by the compiler to check for type-correctness for function calls.

```go
var x string = "Hello World"
var a int = 20
```
Variables are created by first using the `var` keyword, then specifying the variable name (x), the type (string) and finally assigning a value to the variable (Hello World). Assignment is however optional.

Multiple initialisations are supported

```go
var x, y, z int = 10, 20, 30
var (
    a = 10
    b = 20
    c = 30
)
```

While initialising, the Go compiler also infers the type of the variable based on the value assigned. So it's not necessary to explicitly specify the type.

```go
var x = "Hello World"
var a = 10
```

Since creating a new variable with an initial value is common, Go supports a shorter statement.

```go
x := "Hello World"
```
Though this shorthand is valid, it's only within the scope of a function and not valid as a global declaration. 

## Constants

Go also has support for constants. Constants are basically variables whose values cannot be changed later. They're created in the same way you create variables but instead of using the `var` keyword we use the `const` keyword.

```go
package main

import "fmt"

func main() {
  const str = "Hello World"
  fmt.Println(str)
}
```

Reassigning `x` would result in a compile time error.

```go
const str = "Hello World"
str = "It's good to see you"
```

```shell
$> .\main.go:7: cannot assign to x
```

[Control Structures >](./controls.html)