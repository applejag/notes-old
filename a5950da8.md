---
date: 2021-01-30T13:36
tags: 
  - go/concurrent programming
---

# Make goroutines wait for each other

Use the [`WaitGroup`](https://golang.org/pkg/sync/#WaitGroup) type from the
[golang.org/pkg/sync](https://golang.org/pkg/sync/) package as a
[semaphore](https://en.wikipedia.org/wiki/Semaphore_(programming)) to tell
goroutines to wait or release handles.

```go
import (
    "fmt"
    "sync"
)

func PrintSum(slice []int, wg *sync.WaitGroup) {
    defer wg.Done()
    var sum int
    for _, num := range slice {
        sum += num
    }
    fmt.Println(sum)
}

func main() {
    slice := 
    wg := &sync.WaitGroup{}

    wg.Add(3)
    go PrintSum([]int{1, 2, 3, 4, 5}, wg)
    go PrintSum([]int{2, 4, 6, 8, 10}, wg)
    go PrintSum([]int{11, 22, 33, 44}, wg)
    wg.Wait()
}
```

## References

- Mike Van Sickle. (2015, June 5). *Concurrent Programming with Go* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-concurrent-programming>
