# sync.Mutex

## mutual exclusion

- make sure only one goroutine can access a variable at a time to avoid conflicts
- this concept is called `mutual exclusion`
- the conventional name for the data structure that provides it is `mutex`

- Go standard library provides mutual exclusion with `sync.Mutex` and its two methods:

```go
Lock()
UnLock()
```

- we can also use `defer` to ensure the mutex will be unlocked
