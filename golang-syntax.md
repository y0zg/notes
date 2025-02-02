# golang syntax

if statement initialization

```go
if  var declaration;  condition {
    // code to be executed if condition is true
}
```

```go
    if sys, ok := fi.Sys().(*Header); ok {
        ...
    }
```

`&` = a pointer to the value
`*` = dereferences a pointer, returning the value it points to
`...` = arbitrary number of arguments, see [Variadic Functions](https://gobyexample.com/variadic-functions)

When two or more consecutive named function parameters share a type, you can omit the type from all but the last, eg:

```go
func add(x int, y int) int { ...
```

can be shortened to

```go
func add(x, y int) int { ...
```

## Type alias vs type definition

An alias declaration has the form

```go
type T1 = T2
```

as opposed to a standard type definition

```go
type T1 T2
```

See [Type alias explained](https://yourbasic.org/golang/type-alias/)

## Embedding structs

```go
type Ball struct {
    Radius   int
    Material string
}

type Football struct {
    Ball
}
```

NB: It is not possible to typecast to the embedding struct. Embedding is not the same as inheritance.

See [Type embedding in Go](https://travix.io/type-embedding-in-go-ba40dd4264df)

## mismatched types \*string and untyped string

eg:

```go
if event.Action == "requested" {
    ...
}
```

event.Action is a `*string` so deference it, eg:

```go
if *event.Action == "requested" {
    ...
}
```
