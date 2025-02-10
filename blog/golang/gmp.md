Golang 的 GMP 模型是其并发编程的核心，GMP 分别代表：

1. **G（Goroutine）**：轻量级线程，由 Go 运行时管理，创建和切换成本低。
2. **M（Machine）**：操作系统线程，负责执行 Goroutine。
3. **P（Processor）**：逻辑处理器，管理 Goroutine 队列并调度到 M 上执行。

### 关键点

1. **Goroutine 调度**：
   - Go 运行时将 Goroutine 分配到 P 的本地队列。
   - P 将 Goroutine 交给 M 执行。
   - 当 Goroutine 阻塞时，M 会解绑 P 并执行其他 Goroutine。

2. **工作窃取**：
   - 当 P 的本地队列为空时，会从其他 P 的队列或全局队列中“窃取” Goroutine 执行。

3. **系统调用**：
   - Goroutine 进行系统调用时，M 会解绑 P，以便其他 Goroutine 继续执行。
   - 系统调用结束后，M 会尝试重新绑定 P，若失败则将 Goroutine 放入全局队列。

4. **P 的数量**：
   - 默认等于 CPU 核心数，可通过 `GOMAXPROCS` 调整。

### 示例代码

```go
package main

import (
    "fmt"
    "sync"
)

func main() {
    var wg sync.WaitGroup
    for i := 0; i < 10; i++ {
        wg.Add(1)
        go func(i int) {
            defer wg.Done()
            fmt.Println("Goroutine", i)
        }(i)
    }
    wg.Wait()
}
```

### 总结

- **Goroutine**：轻量级线程。
- **M**：操作系统线程。
- **P**：逻辑处理器，负责调度。

GMP 模型通过 Goroutine 的轻量级、P 的调度和 M 的执行，实现了高效的并发处理。