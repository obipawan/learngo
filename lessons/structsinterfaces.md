---
layout: default
---

# Structs
Go’s structs are typed collections of fields. They’re useful for grouping data together to form records.

```go
type person struct {
    name string
    age int
}

func main () {
    fmt.Println(person{"Sherlock", 30})
    s := person{"Sherlock", 30}
}
```

Omitted fields will be zero-valued.

An `&` prefix yields a pointer to the struct.

```go
fmt.Println(&person{name: "Ann", age: 40})
```

Access struct fields with a dot. You can also use dots with struct pointers - the pointers are automatically dereferenced.

```go
s := person{name: "Sean", age: 50}
fmt.Println(s.name)
sp := &s
fmt.Println(sp.age)

sp.age = 51 // Structs are mutable.
```

# Methods

Go supports methods defined on struct types. Methods can be defined for either pointer or value receiver types. Go automatically handles conversion between values and pointers for method calls. You may want to use a pointer receiver type to avoid copying on method calls or to allow the method to mutate the receiving struct.

```go
type rect struct {
	width, height int
}

func (r *rect) area() int {
	return r.width * r.height
}

func main() {
	newRect := rect{10, 10}
	fmt.Println((&newRect).area())
}
```

# Interfaces

Interfaces are named collections of method signatures. Here’s a basic interface for geometric shapes.

```go
type geometry interface {
    area() float32
    perim() float32
}
```

To implement an `interface` in Go, we just need to implement all the methods in the `interface`. Here we implement geometry on rects.

```go
type rect struct {
    width, height float64
}
type circle struct {
    radius float64
}

func (r rect) area() float64 {
    return r.width * r.height
}
func (r rect) perim() float64 {
    return 2*r.width + 2*r.height
}

func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perim() float64 {
    return 2 * math.Pi * c.radius
}

func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}

func main() {
    r := rect{width: 3, height: 4}
    c := circle{radius: 5}
    measure(r)
    measure(c)
}
```

The circle and rect struct types both implement the geometry interface so we can use instances of these structs as arguments to measure.

[Errors >](./errors.html)