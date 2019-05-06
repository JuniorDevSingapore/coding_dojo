# Go Lang - Bootstrapping Go Test

*__Note__: This guide assumes you have Go installed and your `$GOPATH` is set.*

1. Create a new package in your `$GOPATH`:

	```
	mkdir -p $GOPATH/src/code.in.spdigital.io/sp-digital/code_kata
	cd $GOPATH/src/code.in.spdigital.io/sp-digital/code_kata
	```

2. Create a new file `main.go` file with the following contents:

	```go
	package main

	func Sum(x, y int) int {
		return x + y
	}

	func main() {
		Sum(5, 5)
	}
	```

3. Create a `main_test.go` test file with the following content:

	```go
	package main

	import "testing"

	func TestSum(t *testing.T) {
		total := Sum(5, 5)
		if total != 10 {
			t.Errorf("Sum was incorrect, got: %d, want: %d.", total, 10)
		}
	}
	```

	*__Note:__ Use `t.Error` or `t.Fail` to indicate a failure.*

	Here's an alternative with [table driven test][go-table-driven-test]:

	```go
	package main

	import "testing"

	var cases = []struct{
		x int
		y int
		result int
	}{
		{ 5, 5, 10 },
		{ 8, 5, 13 },
	}

	func TestSum(t *testing.T) {
		for _, testCase := range cases {
			total := Sum(testCase.x, testCase.y)
			if total != testCase.result {
				t.Errorf("Sum was incorrect, got: %d, want: %d.", total, testCase.result)
			}
		}
	}
	```

4. Run the test.

	```
	go test
	```

	You should see this:

	```
	PASS
	ok  	code.in.spdigital.io/sp-digital/code_kata	0.008s
	```

[go-table-driven-test]: https://github.com/golang/go/wiki/TableDrivenTests