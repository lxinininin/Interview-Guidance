## 说说你对 JMM 内存模型的理解, 为什么需要 JMM

随着 CPU 和内存的发展速度差异的问题, 导致 CPU 的速度远快于内存, 所以现在的 CPU 加入了高速缓存, 高速缓存一般可以分为 L1, L2, L3 三级缓存, 这会导致缓存一致性的问题, 所以加入了缓存一致性协议, 同时也导致了内存可见性的问题, 而编译器和 CPU 的重排序导致了原子性和有序性的问题, JMM 内存模型正是对多线程操作下的一系列规范约束, 因为不可能让程序员的代码去兼容所有的 CPU, 通过 JMM 我们才屏蔽了不同硬件和操作系统内存的访问差异, 这样保证了 Java 程序在不同的平台下达成一致的内存访问效果, 同时也是保证在高效并发的时候程序能够正确执行

*   **原子性**: Java 内存模型通过 `read`, `load`, `assign`, `use`, `store`, `write` 来保证原子性操作, 此外还有 `lock`, `unlock`, 直接对应 `synchronized` 关键字的 `monitorenter` 和 `monitorexit` 字节码指令

*   **可见性**: Java 保证可见性可以认为通过 `volatile`, `synchronized`, `final` 来实现

*   **有序性**: 由于处理器和编译器的重排序导致的有序性问题, Java 通过 `volatile`, `synchronized` 来保证

*   **happen-before 规则**:

    happens-before 原则是 JMM 中的一个重要概念，它定义了程序中操作之间的一种 happens-before 关系，用来确保程序执行的顺序和可预期性。具体来说，<u>如果操作 A happens-before 操作 B，那么操作 A 的执行结果将对操作 B 可见，即操作 A 在时间上发生在操作 B 之前</u>。

    happens-before 原则定义了一系列规则来确定 happens-before 关系，包括程序顺序性规则（Program Order Rule）、管程锁定规则（Monitor Locking Rule）、volatile 变量规则等。这些规则可以保证程序在不同线程之间的操作顺序是符合预期的。