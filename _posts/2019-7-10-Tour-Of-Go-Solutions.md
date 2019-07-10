---
layout: post
title: Solutions to Tour of Go
category: Programming, Go
---

Tour of Go is great for anyone looking ot jump start their journey in Go.
https://tour.golang.org/


## Concurrency

### Binary Equivalent Trees

```go
package main

import "golang.org/x/tour/tree"
import "fmt"

// Walk walks the tree t sending all values
// from the tree to the channel ch.
func Walk(t *tree.Tree, ch chan int) {
	if t.Left != nil {
		Walk(t.Left, ch)
	}
	ch <- t.Value
	if t.Right != nil {
		Walk(t.Right, ch)
	}
}

// Same determines whether the trees
// t1 and t2 contain the same values.
func Same(t1, t2 *tree.Tree) bool {
	ch1 := make(chan int)
	ch2 := make(chan int)

	go func() {
		Walk(t1, ch1)
		close(ch1)
	}()
	go func() {
		Walk(t2, ch2)
		close(ch2)
	}()
	var v1 int
	var v2 int
	ok1 := true
	ok2 := true
	for ok1 && ok2 {
		v1, ok1 = <-ch1
		v2, ok2 = <-ch2

		if ok1 && ok2 && v1 != v2 {
			return false
		}
	}
	return true
}

func main() {
	fmt.Println(Same(tree.New(1), tree.New(1)))
	fmt.Println(Same(tree.New(1), tree.New(2)))
}
```

