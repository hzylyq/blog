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

Elf file type is EXEC (Executable file), Entry point 0x453b00
说明程序的起点是  0x453b00, 我们使用gdb来调试这个程序

> gdb main

> b *0x453b00

Breakpoint 1 at 0x453b00: file /usr/local/go/src/runtime/rt0_linux_amd64.s, line 8.
至此我们得出了程序的起始位置

```s
TEXT _rt0_amd64_linux(SB),NOSPLIT,$-8
	JMP	_rt0_amd64(SB)

TEXT _rt0_amd64(SB),NOSPLIT,$-8
	MOVQ	0(SP), DI	// argc
	LEAQ	8(SP), SI	// argv
	JMP	runtime·rt0_go(SB)
```

接下来使用gdb的调试命令n, 看下go程序初始化会调用哪些函数
去掉一些检查函数

	CALL	runtime·args(SB), 函数入参
	CALL	runtime·osinit(SB) os初始化
	CALL	runtime·schedinit(SB) 调度任务GMP初始化

然后就是将主程序入口放入一个goroutinue运行
	MOVQ	$runtime·mainPC(SB), AX		// entry
	PUSHQ	AX
	PUSHQ	$0			// arg size
	CALL	runtime·newproc(SB)



