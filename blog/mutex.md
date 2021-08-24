# golang 锁

sync.Mutex

```go
type Mutex struct {
   state int32
   sema  uint32
}
```

锁有两种模式 正常模式和饥饿模式

state 锁的状态

    01 locked 锁定
    10 woken 唤醒
    11 starv	饥饿
    00 waitershift