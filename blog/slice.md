slice和数组区别

slice扩容机制, slice扩容函数
usr/local/go/src/runtime/slice.go
growslice函数 扩容机制如下
```golang
	if cap > doublecap {
		newcap = cap
	} else {
		if old.cap < 1024 {
			newcap = doublecap
		} else {
			// Check 0 < newcap to detect overflow
			// and prevent an infinite loop.
			for 0 < newcap && newcap < cap {
				newcap += newcap / 4
			}
			// Set newcap to the requested cap when
			// the newcap calculation overflowed.
			if newcap <= 0 {
				newcap = cap
			}
		}
	}

```

当slice cap小于1024是,翻倍增长, 大于1024时, 增长因子变为1.25

