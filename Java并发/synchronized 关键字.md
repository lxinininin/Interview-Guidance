## 说一说自己对于 synchronized 关键字的了解

`synchronized` 是 Java 中用于实现线程同步的关键字，它可以用于代码块和方法上，主要用于控制对共享资源的访问，保证多个线程之间的安全访问。

1.  **对象锁**：`synchronized` 可以用于代码块或方法上，作用于对象实例或者类。<u>当 `synchronized` 用于实例方法时，它锁定的是当前对象实例，称为对象锁；当 `synchronized` 用于静态方法时，它锁定的是类的 `Class` 对象，称为类锁</u>。
2.  **互斥性**：<u>`synchronized` 保证了同一时刻只有一个线程可以获取到锁</u>，并且其他线程必须等待该线程释放锁之后才能获取锁，从而避免了多个线程同时访问共享资源导致的数据竞争和数据不一致问题。
3.  **可重入性**：<u>同一个线程可以多次获取同一个锁</u>，即允许在同一个线程中嵌套使用 `synchronized` 块，这种机制称为锁的可重入性。这样的设计简化了并发编程的复杂性，避免了死锁的发生。
4.  **内存可见性**：`synchronized` 除了实现互斥性之外，还具有内存可见性的特性，即<u>当一个线程释放锁时，它会将最新的变量值刷新到主内存中，从而保证其他线程能够及时看到变量的最新值</u>。
5.  **性能影响**：虽然 `synchronized` 是 Java 中最基本的同步机制，但是它的性能相对较低，因为它会引入线程的上下文切换和竞争锁的开销。<u>在高并发情况下，可以考虑使用 `ReentrantLock` 等更高级的锁机制来替代 `synchronized`，以提高性能</u>。

综上所述，`synchronized` 关键字是 Java 中用于实现线程同步的基本机制，它保证了多个线程之间的安全访问共享资源，具有互斥性、可重入性和内存可见性等特性。



## 说说自己是怎么使用 synchronized 关键字

1.   **修饰实例方法 (锁当前对象实例)**：

     ```java
     public synchronized void synchronizedMethod() {
         // 需要保护的共享资源操作
     }
     ```

     这种方式适用于需要对整个方法进行同步的场景，<u>它可以确保同一时刻只有一个线程可以执行该方法，避免了多个线程同时访问共享资源的问题</u>。

2.   **修饰静态方法 (锁当前类)**：

     ```java
     public static synchronized void synchronizedStaticMethod() {
         // 需要保护的共享资源操作
     }
     ```

     对于静态方法，我也可以使用 `synchronized` 关键字来实现同步，<u>它会锁定类的 `Class` 对象，从而确保同一时刻只有一个线程可以执行静态方法</u>。

3.   **修饰代码块 (锁指定对象/类)**：

     ```java
     public void someMethod() {
         synchronized (lock) {
             // 需要保护的共享资源操作
         }
     }
     ```

     对括号里指定的对象/类加锁：

     -   `synchronized(object)` 表示进入同步代码库前要获得 **给定对象的锁**。
     -   `synchronized(类.class)` 表示进入同步代码前要获得 **给定 Class 的锁**



## synchronized 和 volatile 有什么区别？

`synchronized` 关键字和 `volatile` 关键字是两个互补的存在，而不是对立的存在！

-   `volatile` 关键字是线程同步的轻量级实现，所以 `volatile`性能肯定比`synchronized`关键字要好 。但是 `volatile` 关键字只能用于变量而 `synchronized` 关键字可以修饰方法以及代码块 。
-   `volatile` 关键字能保证数据的可见性，但不能保证数据的原子性。`synchronized` 关键字两者都能保证。
-   `volatile`关键字主要用于解决变量在多个线程之间的可见性，而 `synchronized` 关键字解决的是多个线程之间访问资源的同步性。