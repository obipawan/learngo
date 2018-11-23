---
layout: default
---

# Hello World

Here's a simple hello world program,

```go
package main

import "fmt"

func main () {
    fmt.Println("hello world")
}

```

To run this program, execute

```shell
$>go run hello_world.go
```

To build an executable binary, execute

```shell
$>go build hello_world.go
$>./hello_world
```

The `package` keyword simply indicates a directory with multitude of modules, each performing it's own function or a feature from a single reference point. So for main packages, which would be the entry package for our program, we call them `package main`. A main package must have a `main` function, again, since it's the entry package to our program. The main function will be the entry function for our program.

To use other packages, we use the `import` keyword. So importing the `fmt` package is what we'd typically use to handle formatted I/O, or input/output. So when we call the `Println` function from the `fmt` package, we're basically printing `"hello world"` string to the standard output.

A very important remark while designing your package code is the difference between exported functions and unexported functions. Exported functions are functions that start with an upper-case letter. When a function starts with an uppercase letter, that means it's exportable which other packages can see it and use it. However, if the function starts with a lowercase letter, it means that it is an internal or a private function that can only be used within it's defined package.

[Types >](./types.html)