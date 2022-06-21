# go程序是如何运行起来的

不管是windows还是linux, go程序最终都会编译成可执行文件, 这篇文章主要探讨下go 程序的初始话, 以及启动main函数之前做的事情.

先写一个简单的函数

```golang
package main

func main() {
	println("Hello world")
}
```

编译成可执行文件

`go build main.go` 

会生成main文件, 接下来使用readelf来查看程序的入口

`readelf -l main`
Elf file type is EXEC (Executable file)
Entry point 0x453b00
There are 7 program headers, starting at offset 64
说明程序的起点是  0x453b00
我们使用gdb来调试这个程序