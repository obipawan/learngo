---
layout: default
---

# Pointers

Go supports pointers, allowing you to pass references to values and records within your program.

```go
func zero(x int) { // creates a copy of x
  x = 0
}
func main() {
  x := 5
  zero(x)
  fmt.Println(x) // x is still 5
}
```

```go
func zero(xPtr *int) { // passes a pointer to an integer
  *xPtr = 0
}
func main() {
  x := 5
  zero(&x)
  fmt.Println(x) // x is 0
}
```

In Go a pointer is represented using the `*` (asterisk) character followed by the type of the stored value.

Dereferencing a pointer gives us access to the value the pointer points to. When we write `*xPtr = 0` we are saying “store the int `0` in the memory location `xPtr` refers to”. If we try `xPtr = 0` instead we will get a compiler error because `xPtr` is not an `int` it's a `*int`, which can only be given another `*int`.

Finally we use the `&` operator to find the address of a variable. `&x` returns a `*int` (pointer to an int) because `x` is an int. This is what allows us to modify the original variable. `&x` in main and `xPtr` in zero refer to the same memory location.

# New

Another way to get a pointer is to use the built-in `new` function

```go
func one(xPtr *int) {
  *xPtr = 1
}
func main() {
  xPtr := new(int)
  one(xPtr)
  fmt.Println(*xPtr) // x is 1
}
```

`new` takes a type as an argument, allocates enough memory to fit a value of that type and returns a pointer to it. In some programming languages there is a significant difference between using `new` and `&`, with great care being needed to eventually `delete` anything created with `new`. Go is not like this, it's a garbage collected programming language which means memory is cleaned up automatically when nothing refers to it anymore

[Structs & Interface >](./structsinterfaces.html)