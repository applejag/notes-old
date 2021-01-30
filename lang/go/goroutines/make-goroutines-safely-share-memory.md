---
date: 2021-01-30T13:41
tags: 
  - go/concurrent programming
---

# Make goroutines safely share memory

Use the [`Mutex`](https://golang.org/pkg/sync/#Mutex) and
[`RWMutex`](https://golang.org/pkg/sync/#RWMutex) types from the
[golang.org/pkg/sync](https://golang.org/pkg/sync/) package to lock access to a
given variable.

If multiple goroutines write to a variable, or do writing operations on a
datatype (ex mutating a map or a slice), the data might get corrupt and in most
cases it will just result in some panic errors from the Go runtime.

## Lock with Mutex

> This builds on the sample from [[make-goroutines-wait-for-each-other]].

```go
import (
    "fmt"
    "sync"
)

totalSum := 0

func AddToTotalSum(delta int, m *sync.Mutex) {
    m.Lock()
    defer m.Unlock()
    totalSum += sum
}

func SumSlice(slice []int, wg *sync.WaitGroup, m *sync.Mutex) {
    defer wg.Done()
    var sum int
    for _, num := range slice {
        sum += num
    }
    AddToTotalSum(sum, m)
}

func main() {
    slice := 
    wg := &sync.WaitGroup{}
    m := &sync.Mutex{}

    wg.Add(3)
    go PrintSum([]int{1, 2, 3, 4, 5}, wg, m)
    go PrintSum([]int{2, 4, 6, 8, 10}, wg, m)
    go PrintSum([]int{11, 22, 33, 44}, wg, m)
    wg.Wait()
    
    fmt.Printf("Total sum: %d\n", totalSum)
}
```

The `Mutex.Lock()` method will hault the goroutine if the lock is already being
held by a different goroutine, until that lock is then released by
`Mutex.Unlock()`.

## Lock with RWMutex

Reading data without mutating it is non-destructive and could therefore be done
in parallel. Consider the following truthtable:

| Parallel reading | Parallel writing | Outcome         |
| ---------------- | ---------------- | --------------- |
| Yes              | Yes              | ERR             |
| No               | Yes              | ERR             |
| Yes              | No               | OK              |
| No               | No               | Nothing happens |

Using a regular `Mutex` does not allow for this sole-reading use case. While this
is not too common, the use case does come up here and there. For example in
caches.

This is where the [`RWMutex`](https://golang.org/pkg/sync/#RWMutex) comes in
handy and can sometimes introduce a major performance boost where there is a lot
of locking going on.

The `RWMutex` allows parallel *reading*, but as long as there is any writing
involved it will start acting as a regular `Mutex` and hault the goroutines
until the resource is unlocked.

```go
import (
    "fmt"
    "sync"
)

usernameCache := map[int]string

func FetchFromCache(id int, m *sync.RWMutex) (string, bool) {
    m.RLock()
    defer m.RUnlock()
    name, ok := usernameCache[id]
    return name, ok
}

func FetchFromDB(id int, m *sync.RWMutex) (string, bool) {
    if name, err := db.fetchUsernameByID(id); err != nil {
        // Store it in cache
        m.Lock()
        defer m.Unlock()
        usernameCache[id] = name
        // then return
        return name, true
    }
    return "", false
}

func PrintUsername(id int, wg *sync.WaitGroup, m *sync.Mutex) {
    defer wg.Done()

    name, ok = FetchFromCache(id, m)
    if !ok {
        name, ok = FetchFromDB(id, m)
        if !ok {
            fmt.Printf("Unable to find user by ID: %d\n", id)
        } else {
            fmt.Printf("Found user by ID from DB: %d: %q\n", id, name)
        }
    } else {
        fmt.Printf("Found user by ID from cache: %d: %q\n", id, name)
    }
}

func main() {
    wg := &sync.WaitGroup{}
    m := &sync.Mutex{}

    wg.Add(3)
    go PrintUsername(1, wg, m)
    go PrintUsername(2, wg, m)
    go PrintUsername(123, wg, m)
    wg.Wait()
}
```

Keep in mind that using `RWMutex` with just regular `.Lock()` and `.Unlock()` is
has a slight bigger performance hit than using the basic `Mutex`. Only use
`RWMutex` when you can take advantage of it.

## References

- Mike Van Sickle. (2015, June 5). *Concurrent Programming with Go* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-concurrent-programming>
