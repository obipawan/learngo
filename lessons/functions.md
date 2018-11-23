---
layout: default
---

# Functions

A function is an independent section of code that maps zero or more input parameters to zero or more output parameters.

Here’s a function that takes two ints and returns their sum as an int.

```go
func plus(a int, b int) int {
    return a + b
}
```

When you have multiple consecutive parameters of the same type, you may omit the type name for the like-typed parameters up to the final parameter that declares the type.

```go
func plus(a, b int) int {
    return a + b
}
```

Go is also capable of returning multiple values from a function

```go
func foo() (int , string) {
    return 10, "bar"
}
```

## Variadic Functions

There is a special form available for the last parameter in a Go function:

```go
func add(args ...int) int {
    total := 0
    for _, value := range args {
        total += value
    }
    return total
}
```

By using `...` before the type name of the last parameter you can indicate that it takes zero or more of those parameters

## Closure

A closure is a function that has an environment of its own. In this environment, there is at least one bound variable (a name that has a value, such as a number). The closure's environment keeps the bound variables in memory between uses of the closure. [wiki](https://simple.wikipedia.org/wiki/Closure_(computer_science))

```go
func evenGen() func () int {
    i := 0
    return func () (ret int) {
        ret = i
        i += 2
        return
    }
}

func main () {
    nextEven := evenGen()
    fmt.Println(nextEven()) // 0
    fmt.Println(nextEven()) // 2
    fmt.Println(nextEven()) // 4
}
```

[Defer, Panic & Recover >](./deferpanicrecover.html)