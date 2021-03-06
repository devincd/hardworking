### 底层编程
#### 开篇
Go 语言实现刻意隐藏了很多底层细节。我们无法知道一个结构体真实的内存布局，也无法获取一个运行时函数
对应的机器码，也无法知道当前的 goroutine 是运行在哪个操作系统线程之上。事实上，Go 语言调度器会
自己决定是否需要将某个 goroutine 从一个操作系统线程转移到另一个操作系统线程。一个指向变量的指针
也没有展示变量真实的地址。因为垃圾回收期可能会根据需要移动变量的内存位置，当然变量对应的地址也会
被自动更新。

在本章中，我们将展示如何使用 unsafe 包来摆脱 Go 语言规则带来的限制，讲述如何创建 C 语言函数库
的绑定，以及如何进行系统调用。

unsafe 包是一个采用特殊方式实现的包，虽然它可以跟普通包一样的导入和使用，但它实际上是有编译器
实现的，它提供了一些访问语言内部特性的方法，特别是内存布局相关的细节。unsafe 包会广泛地用于
比较低级的包，例如 runtime、os、syscall 和 net 包等，因为它们需要和操作系统密切配合，但是
对于普通的程序一般是不需要使用 unsafe 包的。



