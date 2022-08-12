# Getting started with fuzzing

- with fuzzing, random data is run against your test in an attempt to find vulnerabilites or crash inputs.
- fuzzing can test:
1. SQL injection
2. buffer overflow
3. denial of service
4. cross-site scripting attacks

```go
func Reverse(s string) string {
	b := []byte(s)
	for i, j := 0, len(b) - 1; i < len(b) / 2; i, j = i+1, j-1 {
		b[i], b[j] = b[j], b[i]
	}
	return string(b)
}
```

## Add a unit test

```go
func TestReverse(t *testing.T) {
	testcases := []struct {
		in, want string
	}{
		{"Hello, world", "dlrow ,olleH"},
		{" ", " "},
		{"!12345", "54321!"},
	}
	for _, tc := range testcases {
		rev := Reverse(tc.in)
		if rev != tc.want {
			t.Errorf("Reverse: %q, want %q", rev, tc.want)
		}
	}
}
```

## Add a fuzz test

- the unit test has limitations, namely that each input must be added by the developer
- one benefit of fuzzing is that it comes up with inputs for your code
- you can keep unit tests, benchmarks, and fuzz tests in the same *_test.go file

```go
func FuzzReverse(f *testing.F) {
	testcases := []string{"Hello, World", " ", "!12345"}
	for _, tc := range testcases {
		f.Add(tc) // Use F.Add to provide a seed corpus
	}
	f.Fuzz(func(t *testing.T, orig string) {
		rev := Reverse(orig)
		doubleRev := Reverse(rev)
		if orig != doubleRev {
			t.Errorf("Before: %q, after: %q", orig, doubleRev)
		}
		if utf8.ValidString(orig) && !utf8.ValidString(rev) {
			t.Errorf("Reverse produced invalid UTF-8 string %q", rev)
		}
	})
}
```

- limitations with fuzzing
1. you can't predict the expected output, since you don't have control over the inputs

- the syntax differences between the unit test and fuzz test.
1. the function begins with `FuzzXxx` instead of `TestXxx`, and takes `*testing.F` instead of `*testing.T`
2. the inputs from your unit test are provided as `seed corpus` inputs using `F.Add`

### runing the fuzzing test

1. run the fuzz test without fuzzing it to make sure the seed inputs pass.

```shell
$ go test
```

- you can also run `go test -run=FuzzReverse` if you have other tests in the file
- and you only wish to run the fuzz test.

2. Run `FuzzReverse` with fuzzing

`go test -fuzz=Fuzz`

```
fuzz: elapsed: 0s, gathering baseline coverage: 0/3 completed
fuzz: elapsed: 0s, gathering baseline coverage: 3/3 completed, now fuzzing with 4 workers
fuzz: elapsed: 0s, execs: 1950 (7702/sec), new interesting: 9 (total: 12)
--- FAIL: FuzzReverse (0.26s)
    --- FAIL: FuzzReverse (0.00s)
        reverse_test.go:36: Reverse produced invalid UTF-8 string "\x89\xd8"
    
    Failing input written to testdata/fuzz/FuzzReverse/084056594d871a3f301147132e452b48bd9d68f5dceb1d78bb5c269f00462845
    To re-run:
    go test -run=FuzzReverse/084056594d871a3f301147132e452b48bd9d68f5dceb1d78bb5c269f00462845
FAIL
exit status 1
FAIL    jake-ress.com/fuzzing   0.896s
```

- a failure occured while fuzzing
- and the input that causes the problem is written to a seed corpus file that will be run the next time `go test` is called
- even without the `-fuzz` flag
- to view the input cause the failure, open the corpus file written to the `testdata/fuzz/FuzzReverse/`
```
go test fuzz v1
string("؉")
```

- `go test fuzz v1` indicates the encoding version.
- each following line represents the value of each type making up the corpus entry.
- since the fuzz target only takes 1 input, there is only 1 value after the version

3. run `go test` again without the `-fuzz` flag, the new failing seed corpus entry will be used.

## Fix the invalid string error

```go
func FuzzReverse(f *testing.F) {
	testcases := []string{"Hello, World", " ", "!12345"}
	for _, tc := range testcases {
		f.Add(tc) // Use F.Add to provide a seed corpus
	}
	f.Fuzz(func(t *testing.T, orig string) {
		rev := Reverse(orig)
		doubleRev := Reverse(rev)
		t.Logf("Number of runes: orig=%d, rev=%d, doubleRev=%d", utf8.RuneCountInString(orig), utf8.RuneCountInString(rev), utf8.RuneCountInString(doubleRev))
		if orig != doubleRev {
			t.Errorf("Before: %q, after: %q", orig, doubleRev)
		}
		if utf8.ValidString(orig) && !utf8.ValidString(rev) {
			t.Errorf("Reverse produced invalid UTF-8 string %q", rev)
		}
	})
}
```

- the `t.Logf` will print to the command line if an error occurs
- or if executing the test with `-v`, which can help you debug this issue


- the fuzz test will run util it encounts a failing input unless you pass the `-fuzztime` flag
- the defaults is to run forever if no failure occur

`go test -fuzz=Fuzz -fuzztime 30s`
