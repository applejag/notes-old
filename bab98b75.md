---
date: 2021-01-30T13:37
tags: 
  - go/concurrent programming
---

# Make go code run in the background

Given the following code:

```go
var sum int
for _, num := range slice {
    sum += num
}
fmt.Println(sum)
```

To run it in the background, do three things:

- Wrap the entire function in an anonymous function (`func() {}`), or move it
  to a function of its own.
  
- Encapsulate all scoped variables as parameters to the new function so the
  goroutine can store the values in its own stack instead of some shared memory.
  
- Add the keyword `go` to the function call. This will start the functions as a
  goroutine.
  
```go
go func(slice []int) {
    var sum int
    for _, num := range slice {
        sum += num
    }
    fmt.Println(sum)
}(slice)
```

## References

- Mike Van Sickle. (2015, June 5). *Concurrent Programming with Go* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-concurrent-programming>
