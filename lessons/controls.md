---
layout: default
---

# Controls

## For

Unlike most programming languages, Go's only looping construct is `for`.

Here are three basic ways of working `for`

* Single Condition

```go
i := 1
for i <= 3 {
    fmt.Println(i)
}
```

* Initialise - Evaluate - After

```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

* While-ish for

```go
for {
    fmt.println("Mujhe rang de")
}
```

## If

Branching in Go with `if` and `else` is pretty straight-forward.

* `if` without an `else`
```go
x := 11
if x > 10 {
    fmt.Println("x is larger than 10")
}
```

* `if` with an `else`
```go
x := 11
if x > 10 {
    fmt.Println("x is larger than 10")
} else {
    fmt.Println("x might be smaller than 10")
}
```

* Nested `if` with initialisations
```go
if x := 11; x > 10 {
    fmt.Println("x is larger than 10", x)
} else if x < 10 {
    fmt.Println("x is smaller than 10", x)
} else {
    fmt.Println("x is 0", x)
}
```
All variables declared (`x`) in the `if` statement are available at all branches.

Go doesn't support **ternary if** and braces are required.

## Switch

`switch` statements express conditions across many branches

Here's a basic `switch` example. It works on the values of any type.

```go
i := 10
switch i {
    case 1:
        fmt.Println("one")
    case 2:
        fmt.Println("two")
    case 3:
        fmt.Println("three")
        ..
        ..
        ..
}

// works with values of any type
x := "hello"
switch x {
    case "hello":
        fmt.Println("world")
    default:
        fmt.Println(x)
}
```
A `case` in Go `break`'s implicitly, hence, providing a `break` for every `case` is not required. However, should you need a fallthrough after a `case`, you can then instruct Go to do so with the `fallthrough` keyword. A `fallthrough` should be the last statement in a `case`.

```go
switch i := 10 {
    case 1:
        fmt.Println("one")
        fallthrough
    case 2:
        fmt.Println("two")
        fallthrough
        ..
        ..
        ..
}
```

Multiple cases can be clubbed together separated by commas.

```go
switch time.Now().Weekday() {
    case time.Saturday, time.Sunday:
        fmt.Println("Weekend")
    default:
        fmt.Println("Weekday")
}
```



[Advanced Types >](./advancedtypes.html)