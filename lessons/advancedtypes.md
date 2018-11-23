---
layout: default
---

# Advanced Types

## Arrays

An array is a numbered sequence of elements of single type with a fixed length. 

An example of an array containing 5 items would look like this

```go
var x [5] int = [5]int{1, 2, 3, 4, 5}
fmt.Println(x)
```

We can set a value at an index using the `array[index] = value` syntax, and get a value with `array[index]`.

The builtin `len` returns the length of an array.

Example of looping through an array

```go
var x := [5]int { 1, 2, 3, 4, 5 }
for i, value := range x {
    fmt.Println("value=", value, "index=", i)
}
```
In this `for` loop `i` represents the current position in the array and `value` is the same as `x[i]`. We use the `range` keyword followed by the name of the variable we want to loop over. 


```go
var x := [5]int { 1, 2, 3, 4, 5 }
for _, value := range x {
    fmt.Println("value=", value)
}
```

A single `_` (underscore) is used to tell the compiler that we don't need this. (In this case we don't need the iterator variable).

## Slices

A slice is a segment of an array. Like arrays slices are indexable and have a length. Unlike arrays this length is allowed to change.

```go
slice := []int
var slice []int
```

If you want to create a slice you should use the built-in make function.

```go
x := make([]int, 5)
```

This creates a slice that is associated with an underlying `int` array of length 5. Slices are always associated with some array, and although they can never be longer than the array, they can be smaller. The `make` function also allows a 3rd parameter.

```go
x := make([]int, 5, 10)
```

10 represents the capacity of the underlying array which the slice points to:

![Slices](../assets/imgs/slices1.png)

Another way to create slices is to use the `[low : high]` expression.

```go
arr := [5]float64{ 1, 2, 3, 4, 5 }
x := arr[ 0 : 5 ]
```

`low` is the index of where to start the slice and `high` is the index where to end it (but not including the index itself). For example while `arr[ 0 : 5 ]` returns `[ 1, 2, 3, 4, 5 ]`, `arr[ 1 : 4 ]` returns `[ 2, 3, 4 ]`.

For convenience we are also allowed to omit `low`, `high` or even both. The following demonstrates the syntax.

```go
// statements that all mean the same
fmt.Println(arr[ 0 : len(arr) ])
fmt.Println(arr[ 0 :])
fmt.Println(arr[: len(arr)])
fmt.Println(arr[:])
```

Here's a great blog [post](https://blog.golang.org/go-slices-usage-and-internals) by the Go team on slices and internals.

Go includes two built-in functions with slices - `Append` & `Copy`.

#### Append

```go
x := []int{1, 2, 3}
y := append(x, 4, 5)
fmt.Println(y) // [1, 2, 3, 4, 5]
```

Append creates a new slice by taking an existing slice (the first argument) and appending all the following arguments to it.

#### Copy

```go
x := []int{1, 2, 3}
y := make([]int, 2)
copy(y, x)
fmt.Println(x, y)
```

After running this program `x` has `[1,2,3]` and `y` has `[1,2]`. The contents of `x` are copied into `y`, but since `y` has room for only two elements only the first two elements of `x` are copied.

## Maps

A map is an unordered collection of key-value pairs. Also known as an associative array, a hash table or a dictionary, maps are used to look up a value by its associated key.

```go
x := make(map[string]int)
m["key"] = 1
```

Get a value for a key with `name[key]`.

`len` returns the number of key/value pairs when called on a `map`.

```go
x := make(map[string]int)
m["key"] = 1
len(m) // 1
```

`delete` removes a key-value pair from `map`s

```go
x := make(map[string]int)
m["key"] = 1
len(m) // 1
delete(m, "key")
len(m) // 0
```

Accessing an element of a `map` can return two values instead of just one. The first value is the result of the lookup, the second tells us whether or not the lookup was successful

```go
m := make(map[string]int)
m["key"] = 10
value, present := m["key"]
fmt.Println(value, present) // 10, true
value, present = m["key1"]
fmt.Println(value, present) // 0, false
```

[Functions >](./functions.html)