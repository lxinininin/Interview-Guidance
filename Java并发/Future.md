## Future 类有什么用？

-   **同步**：发出一个调用之后，在没有得到结果之前， 该调用就不可以返回，一直等待。
-   **异步**：调用在发出之后，不用等待返回结果，该调用直接返回。

`Future` 类是<u>异步思想</u>的典型运用，主要用在一些需要执行耗时任务的场景，避免程序一直原地等待耗时任务执行完成，执行效率太低。具体来说是这样的：当我们执行某一耗时的任务时，可以将这个耗时任务交给一个子线程去异步执行，同时我们可以干点其他事情，不用傻傻等待耗时任务执行完成。等我们的事情干完后，我们再通过 `Future` 类获取到耗时任务的执行结果。这样一来，程序的执行效率就明显提高了。

这其实就是多线程中经典的 **Future 模式**，你可以将其看作是一种设计模式，核心思想是异步调用，主要用在多线程领域，并非 Java 语言独有。

在 Java 中，`Future` 类只是一个泛型接口，位于 `java.util.concurrent` 包下，其中定义了 5 个方法，主要包括下面这 4 个功能：

-   取消任务；
-   判断任务是否被取消;
-   判断任务是否已经执行完成;
-   获取任务执行结果。

```java
// V 代表了Future执行的任务返回值的类型
public interface Future<V> {
    // 取消任务执行
    // 成功取消返回 true，否则返回 false
    boolean cancel(boolean mayInterruptIfRunning);
    // 判断任务是否被取消
    boolean isCancelled();
    // 判断任务是否已经执行完成
    boolean isDone();
    // 获取任务执行结果
    V get() throws InterruptedException, ExecutionException;
    // 指定时间内没有返回计算结果就抛出 TimeOutException 异常
    V get(long timeout, TimeUnit unit)

        throws InterruptedException, ExecutionException, TimeoutExceptio

}
```

简单理解就是：我有一个任务，提交给了 `Future` 来处理。任务执行期间我自己可以去做任何想做的事情。并且，在这期间我还可以取消任务以及获取任务的执行状态。一段时间之后，我就可以 `Future` 那里直接取出任务执行结果。



## Callable 和 Future

Callable 接口类似于 Runnable, 但是 Runnable 不会返回结果, 并且无法抛出返回结果的异常, 而 Callable 功能更强大一些, 被线程执行后, 可以返回值, 这个返回值可以被 Future 拿到, 也就是说, <u>Future 可以拿到异步执行任务的返回值, Callable 可以认为是带有回调的 Runnable</u>

Future 接口表示异步任务, 是还没有完成的任务给出的未来结果; 所以说 <u>Callable 用于产生结果, Future 用于获取结果</u>

<u>Callable 和 Future 通常一起使用，通过 Callable 提交一个带返回值的任务，并通过 Future 来获取任务的执行结果</u>。这种方式可以使得任务的执行和结果的获取分离，使得任务的执行与结果的处理更加灵活和异步。