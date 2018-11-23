---
layout: default
---

# Types

Go is a statically typed programming language. This means that variables always have a specific type and that type cannot change.

Go comes with several built-in data types which we will now look at in more detail.

### Numbers

Like other languages, numbers in go are represented by **integers** and **floating point numbers**

#### Integers
Integers are numbers without a decimal counterpart. Go's integer types are
* `uint8`
* `uint16`
* `uint32`
* `uint64`
* `int8`
* `int16`
* `int32`
* `int64`

`uint` means unsigned integers & `int` means signed integers. Unsigned integers contain only positive numbers including zero (0) 
In addition, Go has two aliases:

* `byte` = `uint8`
* `rune` = `int32`

There are also three machine dependant integer types: `uint`, `int` & `uintptr`. They are machine dependent because their size depends on the type of architecture you are using.

#### Floating point Numbers
Floating point numbers are numbers that contain a decimal component (real numbers). 
* Like most languages, floating point numbers are inxact. 
* Floating point numbers have a certain size (32 bit or 64 bit). Using a larger sized floating point number increases it's precision.
* In addition to numbers there are several other values which can be represented: “not a number” (`NaN`, for things like 0/0) and positive and negative infinity. (+∞ and −∞)
* `float32`
* `float64`
* `complex32`
* `complex64`

`Complex` Types are used to represent numbers that have a complex component (imaginary) associated with it.


### Strings

String literals can be created using double quotes `"Hello World"` or back ticks `` `Hello World` ``. The difference between these is that double quoted strings cannot contain newlines and they allow special escape sequences. For example \n gets replaced with a newline and \t gets replaced with a tab character.

Some common operations that can be performed on `Strings`
* Finding the length of the string - `len("hello world")`
* Access an individual character - `"hello world[1]`
* Concatination - `"hello" + "world"`


### Booleans

A one bit integer type used to represent `true` and `false`.
Three logical operators are used with boolean values
* `&&` - And
* `||` - Or
* `!` - Not

[Variables And Constants >](./variables.html)