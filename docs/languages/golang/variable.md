---
layout: default
title: Variable
nav_order: 3
parent: Golang
grand_parent: Programming Languages
permalink: /docs/languages/golang/variable
---

# Other

## Zero Values

Unlike JavaScript, Go does not have something akin to the JavaScript undefined primitive value.

Variables declared without an explicit initial value are given their zero value.

- _further info:_
  - [data types - zero value]({% link docs/languages/golang/data-types.md %}#zero-value)


## Difference between `new()` and `make()` in Golang [^1]

<details markdown="block">
  <summary> in short...  </summary>

In the Go programming language, `new()` and `make()` are two commonly used functions for creating and initializing variables of different types.

`new()` is used to create a variable of a specified type with a zero value and returns a pointer to that variable.

In variable declaration, when we don’t specify initial values for variables, their default values are their zero values.

```go
numPtr := new(int)
```

`make()` is used to create and initialize variables of reference types, such as slices, maps, and channels.

It is suitable for creating these variables because they are not set to zero values but are initialized based on their types.

```go
slice := make([]int, 3)
```

<!-- in short... -->
-----
</details>

<details markdown="block">
  <summary> demystifying...  </summary>

These functions `new()` and `make()`[^2] which might seem similar at first serve different purposes and are crucial for _memory allocation_ and _data initialization_ in Go.

Both `new()` and `make()` are built-in functions in Go, used to allocate memory. However, they are used for different data types and scenarios:

- `new()` function:
  - `new()` is used to allocate memory for value types (e.g., integers, floats, structs) and returns a pointer to the newly allocated zeroed value.
  - it takes a single argument
  - the syntax of the new() function is straightforward as shown below.
    - `func new(Type) *Type`
    - here, `Type` represents the type of the value we want to allocate memory for.
    - ```go
      type Person struct {
        Name string
        Age  int
      }
      p := new(Person)
      ```
- `make()` function:
  - `make()` is used to create and initialize slices, maps, and channels, which are reference types in Go.
  - it takes two or three arguments
  - the syntax of the `make()` function varies depending on the type it is used with
    - for __slices__
      - `func make([]Type, len, cap) []Type`
        - `Type`: The type of elements the slice will hold.
        - `len`: The initial length of the slice.
        - `cap`: The capacity of the slice, which is optional and used to specify the underlying array's capacity. If not provided, it defaults to the same value as the length.
      - ```go
        // using make() to create a slice of integers
        numbers := make([]int, 5, 10)
        ```
    - for __maps__
      - `func make(map[KeyType]ValueType, initialCapacity int) map[KeyType]ValueType`
        - `KeyType`: The type of keys in the map.
        - `ValueType`: The type of values associated with the keys.
        - `initialCapacity`: The initial capacity of the map. This is optional but can be used to optimize performance when the number of elements is known in advance.
      - ```go
        // using make() to create a map of string keys and int values
        scores := make(map[string]int)
        ```
    - for __channels__
      - `func make(chan Type, capacity int) chan Type`
        - `Type`: The type of values that can be sent and received through the channel.
        - `capacity`: The buffer size of the channel. If set to 0, the channel is unbuffered.
      - ```go
        // using make() to create an unbuffered channel of integers
        ch := make(chan int)
        ```

To summarize[^2]:
- use `new()` to allocate memory for value types and obtain a pointer to the zeroed value.
- use `make()` to create and initialize slices, maps, and channels (reference types) _with their respective types and initial capacities_.

-----
<!-- demystifying... -->
</details>

In Golang, there are two ways to allocate memory: and new . While both of these keywords can be used to allocate memory, they are used for different purposes.

The `new` keyword in Golang is used to create a new instance of a variable, and it __returns a pointer__ to the memory allocated. It is used for allocating memory for the value of a certain type. `new` takes a type as its argument and returns a pointer to a newly allocated zero value of that type.

The `make` keyword in Golang is used to create slices, maps, and channels, and it returns a value of the type that was created. Unlike `new`, `make` __returns a value__ of the type being created, __not a pointer__ to the type.

Keypoints
- `new` returns a pointer to the memory allocated, while `make` returns the value of the type being created.
- `new` only works with basic types such as `int`, `float`, `bool`, etc. `make` is used for creating slices, maps, and channels.
- `new` allocates zeroed memory, while `make` allocates memory and initializes it.

```golang
import "fmt"

func main() {
  var x *int = new(int)
  *x = 5

  y := new(int)
  *y = 6

  fmt.Println(*x)
  fmt.Println(*y)

  var s []int = make([]int, 3)
  s[0] = 1
  s[1] = 2
  s[2] = 3

  r := make([]int, 2)
  r[0] = 7
  r[1] = 8

  w := make([]int, 4)

  fmt.Println(s)
  fmt.Println(r)
  fmt.Println(w)

  // output
  // 5
  // 6
  // [1 2 3]
  // [7 8]
  // [0 0 0 0]
}
```

- _further info:_
  - [go pointers - new vs make]({% link docs/languages/golang/pointer.2023a03m05d.md %}#new--make)

## Conversion

### Converting map to struct


One way is to roundtrip it through JSON. Otherwise see much more [here]({% link docs/languages/golang/json.md %}#converting-map-to-struct) on how to convert map to struct and vice-versa.
```golang
package main
import (
  "bytes"
  "encoding/json"
)
func transcode(in, out interface{}) {
  buf := new(bytes.Buffer)
  json.NewEncoder(buf).Encode(in)
  json.NewDecoder(buf).Decode(out)
}
```

Example:
```golang
package main
import "fmt"
type myStruct struct {
  Name string
  Age  int64
}
func main() {
  myData := map[string]interface{}{
    "Name": "Tony",
    "Age": 23,
  }
  var result myStruct
  transcode(myData, &result)
  fmt.Printf("%+v\n", result) // {Name:Tony Age:23}
}
```

----

# Footnotes

[^1]: [Difference between new() and make() in Golang](https://saeed0x1.medium.com/difference-between-new-and-make-in-golang-f163b33236ee)
[^2]: [Demystifying new() and make() Functions in Go](https://medium.com/the-bug-shots/demystifying-new-and-make-functions-in-go-845590ee1603)
