title: Go 指南练习
author: andyhui
tags:
  - golang
categories:
  - Go
date: 2019-03-12 22:42:00
update: 2019-03-18 12:10:00
---
## [Go 指南](https://tour.go-zh.org/list)
> Go语言官方给出了一份教程，基本涵盖了涵盖了该语言的大部分重要特性
>
> 形式是`知识点 + 代码`的形式，很喜欢这样的学习方式
>
> 这篇博客记录下每道练习题的自己的解答及官方解答。

<!-- more -->

### [练习：循环与函数](https://tour.go-zh.org/flowcontrol/8)
> 作为练习函数和循环的简单途径，用牛顿法实现开方函数。
>
> 在这个例子中，牛顿法是通过选择一个初始点 *z* 然后重复这一过程求 `Sqrt(x)` 的近似值：
>
> #### $z=z-\frac{z^{2}-x}{2z}$
>
> 为了做到这个，只需要重复计算 10 次，并且观察不同的值（1，2，3，……）是如何逐步逼近结果的。 然后，修改循环条件，使得当值停止改变（或改变非常小）的时候退出循环。观察迭代次数是否变化

>提示：定义并初始化一个浮点值，向其提供一个浮点语法或使用转换：

```go
z := float64(1)
z := 1.0
```
#### my solution
```go
package main

import (
	"fmt"
	"math"
)

func Sqrt(x float64) float64 {
	z := float64(x/2)
	for s := 1; s <= 1<<20; s++ {
		z -= (z*z - x) / 2 * z
	}
	return z
}

func main() {
	n := 2
	fmt.Println(Sqrt(float64(n)))
	fmt.Println(math.Sqrt(float64(n)))
}
```

#### go Team solution

loops.go

```go
package main

import (
	"fmt"
	"math"
)

const delta = 1e-6

func Sqrt(x float64) float64 {
	z := x
	n := 0.0
	for math.Abs(n-z) > delta {
		n, z = z, z-(z*z-x)/(2*z)
	}
	return z
}

func main() {
	const x = 2
	mine, theirs := Sqrt(x), math.Sqrt(x)
	fmt.Println(mine, theirs, mine-theirs)
}
```



### [练习：slice](https://tour.go-zh.org/moretypes/18)

> 实现 `Pic`。它返回一个 slice 的长度 `dy`，和 slice 中每个元素的长度的 8 位无符号整数 `dx`。当执行这个程序，它会将整数转换为灰度（好吧，蓝度）图片进行展示。

> 图片的实现已经完成。可能用到的函数包括 `(x+y)/2 `、 `x*y` 和 `x^y`（使用 [`math.Pow`](http://golang.org/pkg/math/#Pow)计算最后的函数）。
>
> （需要使用循环来分配 `[][]uint8` 中的每个 `[]uint8`。）
>
> （使用 `uint8(intValue)` 在类型之间进行转换。）



#### my solution
```go
package main

import (
	"golang.org/x/tour/pic"
	"math"
)

func cal(x, y, n int) uint8 {
	var res uint8
	switch n {
	case 1:
		res = uint8((x + y) / 2)
	case 2:
		res = uint8(x * y)
	case 3:
		res = uint8(x ^ y)
	case 4:
		res = uint8(x * int(math.Log(float64(y))))
	case 5:
		res = uint8(x % (y + 1))
	}
	return res
}

func Pic(dx, dy int) [][]uint8 {
	res := make([][]uint8, dy)
	for y := range res {
		res[y] = make([]uint8, dx)
		for x := range res[y] {
			res[y][x] = cal(x,y,5)
		}
	}
	return res
}
func main() {
	pic.Show(Pic)
}
```



运行结果

![结果](http://githubblog.andyhui.top/image/go/slice.png)

#### go Team solution

slices.go

```go
package main

import "golang.org/x/tour/pic"

func Pic(dx, dy int) [][]uint8 {
	p := make([][]uint8, dy)
	for i := range p {
		p[i] = make([]uint8, dx)
	}

	for y, row := range p {
		for x := range row {
			row[x] = uint8(x * y)
		}
	}

	return p
}

func main() {
	pic.Show(Pic)
}
```



![结果](http://githubblog.andyhui.top/image/go/slice2.png)







### [练习：map](https://tour.go-zh.org/moretypes/23)

> 实现 `WordCount`。它应当返回一个含有 `s`中每个 “词” 个数的 map。函数 `wc.Test`针对这个函数执行一个测试用例，并输出成功还是失败。

> 你会发现 [strings.Fields](http://golang.org/pkg/strings/#Fields) 很有帮助。

#### my solution == go Team solution

maps.go

```go
package main

import (
	"strings"
	"golang.org/x/tour/wc"
)

func WordCount(s string) map[string]int {
	count := make(map[string]int)
	for _, word := range strings.Fields(s) {
		count[word]++
	}
	return count
}

func main() {
	wc.Test(WordCount)
}
```





### [练习：斐波纳契闭包](https://tour.go-zh.org/moretypes/26)

> 现在来通过函数做些有趣的事情。

> 实现一个` fibonacci` 函数，返回一个函数（一个闭包）可以返回连续的[斐波纳契数列](https://zh.wikipedia.org/wiki/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97) `(0, 1, 1, 2, 3, 5, ...)`。


#### my solution
```go
package main

import "fmt"

// fibonacci is a function that returns
// a function that returns an int.
func fibonacci() func(int) int {
	dp := []int{0, 1}
	for i := 2; i < 100; i++ {
		dp = append(dp, dp[i-1] + dp[i-2])
	}
	return func(x int) int {
		return dp[x]
	}
}
func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Println(f(i))
	}
}
```

#### go Team solution

fib.go

```go
package main

import "fmt"

// fibonacci is a function that returns
// a function that returns an int.
func fibonacci() func() int {
	f, g := 1, 0
	return func() int {
		f, g = g, f+g
		return f
	}
}

func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Println(f())
	}
}
```



### [练习：Stringer](https://tour.go-zh.org/methods/18)

> 通过让 `IPAddr` 类型实现 `fmt.Stringer` 来打印点号分隔的地址。
>
> 例如，`IPAddr{1, 2, 3, 4}`应当打印为 `"1.2.3.4"`。

#### my solution == go Team solution

stringers.go

```go
package main

import "fmt"

type IPAddr [4]byte

func (ip IPAddr) String() string{
	return fmt.Sprintf("%d.%d.%d.%d", ip[0],ip[1],ip[2],ip[3])}

func main() {
	hosts := map[string]IPAddr{
		"loopback":  {127, 0, 0, 1},
		"googleDNS": {8, 8, 8, 8},
	}
	for name, ip := range hosts {
		fmt.Printf("%v: %v\n", name, ip)
	}
}
```

#### result

```shell
loopback: 127.0.0.1
googleDNS: 8.8.8.8
```

### To be continue...