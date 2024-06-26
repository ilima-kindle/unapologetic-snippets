---
layout: default
title: Pointer
nav_order: 3
parent: Golang
grand_parent: Programming Languages
permalink: /docs/languages/golang/pointer
---

Other examples:
- [go pointers]({% link docs/languages/golang/pointer.2023a03m05d.md %}) [^2]
- [did u really know about pointers in golang?]({% link docs/languages/golang/pointer.2023a04m08d.md %}) [^1]
- [what is nil?]({% link docs/languages/golang/pointer.nil.2023a07m02d.md %})


# Pointer

<details markdown="block">
  <summary>
    a gentle introduction to Pointers
  </summary>


When assigning a value to a variable in Go, the value is stored at a particular address in the computer's memory.

Use the reference operator `&` to get this address, like so:

```golang
package main
import "fmt"
func main() {
  var answer int = 42
  fmt.Println(&answer) // prints something like 0x14000122008
}
```

When using the `&` operator on a variable it actually returns a pointer.

In simple terms, a pointer is a variable that hols the memory address of another variable. Think of them as "pointing to" a specific spot in memory.

Like the variables that they point to, pointers in Go also have types. A pointer with the type `*int` can only hold the memory address of an `int` variable. And a pointer with the type `*string` can only hold the memory address of a `string` variable. And so on.

```golang
package main
import "fmt"
func main() {
  var answer int = 42
  var answerPtr *int = &answer
  fmt.Println(answerPtr) // prints something like 0x1400012c008
}
```

Use the deference operator `*` to read or set the underlying value that a pointer points to. This is often known as indirection.

```golang
package main
import "fmt"
func main() {
  answer := 42
  answerPtr := &answer
  fmt.Println(answerPtr)  // prints something like 0x14000122008
  fmt.Println(*answerPtr) // prints 42
  *answerPtr = 99         // use the dereference operator to assign a new value
  fmt.Println(answer)     // prints 99
}
```

----

<!-- A gentle introduction to Pointers -->
</details>

a one-pager to understanding pointers in Go

```golang
package main

import "fmt"

func main() {
  // a pointer is a variable that holds the memory address of another variable
  var p1 *int
  x := 42
  y := 40
  // to create a pointer to a variable, use the & operator followed by the variable's name
  p1 = &x
  p2 := &y
  // to access the value of the variable pointed to by a pointer, you use the * operator followed by the pointer variable name
  *p1 = 100

  increment(&y)
  increment(p2)

  fmt.Println(x)
  fmt.Println(p2)
  fmt.Println(&p2)
  fmt.Println(*p2)
}

// passing pointers to functions
// one common use of pointers is to pass a variable to a function by reference, allowing the function to modify the variable directly.
func increment(p *int) {
  *p++
}
```


```golang
package main

import "fmt"

func main() {
  var creature string = "shark"
  var pointer *string = &creature

  fmt.Println("creature = ", creature)
  fmt.Println("pointer = ", pointer)

  fmt.Println("*pointer = ", *pointer)
  fmt.Println("&creature = ", &creature)

  // output
  // creature = shark
  // pointer = 0xc000014260
  // *pointer = shark
  // &creature = 0xc000014260

  var creatureB Creature = Creature{Species: "shark"}
  fmt.Printf("1) %+v\n", creatureB)
  changeCreature(&creatureB)
  fmt.Printf("3) %+v\n", creatureB)
  // output
  // 1) {Species:shark}
  // 2) &{Species:jellyfish}
  // 3) {Species:jellyfish}

  var creatureC *Creature = &Creature{Species: "shark"}
  fmt.Printf("1) %+v\n", creatureC)
  changeCreature(creatureC)
  fmt.Printf("3) %+v\n", creatureC)
  // output
  // 1) {Species:shark}
  // 2) &{Species:jellyfish}
  // 3) &{Species:jellyfish}

  creatureD := &Creature{Species: "shark"}
  fmt.Printf("1) %+v\n", creatureD)
  changeCreature(creatureD)
  fmt.Printf("3) %+v\n", creatureD)
  // output
  // 1) {Species:shark}
  // 2) &{Species:jellyfish}
  // 3) &{Species:jellyfish}
}

type Creature struct {
  Species string
}

func changeCreature(creature *Creature) {
  creature.Species = "jellyfish"
  fmt.Printf("2) %+v\n", creature)
}
```

## Pointer in function

Function argument passing is value copying, which also applies to pointer arguments. When `doubleInt(p)` is called, a copy of pointer `p` is created first and then passed to the function `doubleInt`. The modification on the copy of the pointer `p` in `doubleInt` will not reflect on the original pointer `p` in the main function.

<details markdown="block">
  <summary>
    pointer in function sample
  </summary>
```golang
package main

import "fmt"

func doubleInt(x int) {
  x = x * 2
}
func main() {
  a := 1
  doubleInt(a)
  fmt.Println(a) // 1
}
```

```golang
package main

import "fmt"

func doubleInt(x *int) {
  *x = *x * 2
  x = nil // update the pointer x to nil
}

func main() {
  a := 1
  p := &a
  doubleInt(p)
  fmt.Println(a) //2 fmt.Println(p == nil) //false
}
```
</details>

### NIL pointer

The zero value of a pointer type is nil. if you try to dereference a pointer which points to nothing (`nil`), it will cause a runtime panic.
With that being said, we should always check if the pointer is `nil` before trying to dereference it.

<details markdown="block">
  <summary>
    a nill pointer sample
  </summary>
```golang
package main

import "fmt"

func main() {
  var ptr *int
  fmt.Println(ptr) // <nil>
  ptrValue := *ptr // panic: runtime error: invalid memory address or nil
  fmt.Println(ptrValue)
}
```
</details>

## What really is `unsafe.Pointer`?

To get a start, let’s examine its definition in the code:

```go
type Pointer *ArbitraryType
```

Unlike a `*int`, which can only point to an `int`, or a `*bool`, which is restricted to bool values, `unsafe.Pointer` has the
liberty to point to any arbitrary type, sweet flexibility right?

`unsafe.Pointer` is a special kind of pointer that turns off the usual safety rules. When you use it, you're telling the Go compiler: _“I know what I'm doing, so trust me”_. Be careful, because you're going around the normal safety checks.

```go
var a int64 = 10
aPtr := unsafe.Pointer(&a)
b := (*float64)(aPtr)
```

----

[^1]: [Did u really know about Pointers in Golang?](https://medium.com/@achmadrizkinf/did-u-really-know-about-pointers-in-golang-3e8be6ff668c)
[^2]: [Go Pointers](https://medium.com/@nurettinabaci/go-pointers-a538c457a62e)
