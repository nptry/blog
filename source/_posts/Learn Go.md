---
title: Learn Go
date: 2020-11-12
updated: 2020-11-12
categories:
- 学习中
tags:
- 学习中
---

# 语法
- [defer](https://tour.go-zh.org/flowcontrol/12)

- [指针](https://tour.go-zh.org/moretypes/1)

	`*int  &i  *p`
```
	var p *int

	i := 42
	p = &i

	fmt.Println(*p)
```

- [结构体struct](https://tour.go-zh.org/moretypes/2)
```
type Vector struct {
	X int
	Y int
}
v := Vector{1, 2}
fmt.Println(v.X)
```