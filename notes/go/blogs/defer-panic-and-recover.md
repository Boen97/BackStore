# Defer, Panic and Recover

[blog url](https://go.dev/blog/defer-panic-and-recover)

- `Defer` is commonly used to simplify functions that perform various clean-up actions.

```go
func CopyFile(dstName, srcName string) (written int64, err error) {
	src, err := os.Open(srcName)
	if err != nil {
		return
	}
	defer src.Close()

	dst, err := os.Create(dstName)
	if err != nil {
		return
	}
	defer dst.Close()

	return io.Copy(dst, src)
}
```

- Defer statements allow us to think about closing each file after opening it
- guarantee the file will be closed

## the behaviour of defer statements

- the behaviour of defer statements is straightforward and predictable

1. A deferred function’s arguments are evaluated when the defer statement is evaluated.

```go
func a() {
	i := 0
	defer fmt.Println("defer", i)
	i++
	fmt.Println("before defer", i)
}

// output

// before defer 1
// defer 0
```

2. Deferred function calls are executed in Last In First Out order after the surrounding function returns.

3. Deferred functions may read and assign to the returning function's named return values.

- this function returns 2

```go
func c()(i int) {
	defer func() {i++}()
	return 1
}
```

> this is convenient for modifying the error return value of a function

## Panic

> Panic is a built-in functions that stops the ordinary flow of control and begins panicking.

- when the function F calls panic, execution of F stops, any deferred functions in F are executed normally
- and then F returns to its caller.
- to the caller, F then behaves like a call to panic
- the process continues up the stack until all functions in the current `goroutine` have returned
- at which point the program crashes

- Panics can be initiated by invoking panic directly.
- they can also be caused by runtime errors, such as out-of-bounds array accesses.

## Recover

- Recover is a built-in function that regains control of a panicking goroutine.
- Recover only useful inside deffered functions.
- During normal execution, a call to recover will return nil and have no other effect
- if the current goroutine is panicking, a call to recover will capture the value given to panic and resume normal execution.

> The convention in the Go libraries is that even when a package uses panic internally, its external API still presents explicit error return values

- Other uses of defer (beyond the file.Close example given earlier) include releasing a mutex:
```go
mu.Lock()
defer mu.Unlock()
```
