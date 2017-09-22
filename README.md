# GoLang BitFlag

## Installation

`go get github.com/mvpninjas/go-bitflag`

## API

| Description        | Function  |
| ------------------ |:----------|
| Set flags | `flag.Set(opts ...Flag)` |
| Unset flags | `flag.Unset(opts ...Flag)` |
| All flags are setted | `flag.Isset(opts ...Flag) bool` |
| One of flags is setted | `flag.One(opts ...Flag) bool` |
| Clear all flags | `flag.Clear()` |


## Example

```
package main

import (
	"fmt"
	bitflag "github.com/mvpninjas/go-bitflag"
)

const (
	A flag.Flag = 1 << flag.Flag(iota)
	B
	C
	D
)

func main() {

	var flag bitflag.Flag

	flag.Set(A)
	flag.Set(B, C)
	flag.Set(C|D)

	flag.Clear()

	flag.Set(A, B, C, D)

	flag.Unset(A)

	flag.Unset(B, C)

	flag.Unset(A|C)

	if flag.Isset(A) {
		fmt.Println("A")
	}

	if flag.Isset(B) {
		fmt.Println("B")
	}

	if flag.Isset(C) {
		fmt.Println("C")
	}
	
	if !flag.Isset(D) {
		fmt.Println("D")
	}
	
	flag.Set(C)
	
	if !flag.One(D) {
		fmt.Println("E")
	}
}

```


## Example without this library 

```

type Flag byte

const (
	A = Flag(1 << iota)
	B
	B
)

var flag Flag

// set A
flag |= A

// check if A setted
if flag & A > 0 {
	// Flag setted
}

// remove A
flag ^= A

```
