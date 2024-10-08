## equals 与 == 的区别

1.  `==` 操作符用于比较两个对象的引用是否指向相同的内存地址。换句话说，它检查的是对象的引用是否相同，而不是对象的内容是否相同。
2.  `equals()` 方法用于比较两个对象的内容是否相等。默认情况下，`equals()` 方法在 Object 类中是使用 `==` 运算符来比较两个对象的引用，因此它与 `==`  的作用相似。但是，`equals()` 方法可以被子类重写，以实现自定义的相等比较逻辑。
3.  通常情况下，当我们想要比较两个对象的内容时，应该使用 `equals()` 方法而不是 `==` 运算符。

4.  对于基本数据类型（如 int, double, char 等），`==`  运算符用于比较它们的值是否相等。但对于对象类型，`==`  运算符用于比较它们的引用是否相等。



## hashCode() 和 equals()

因为两个相等的对象的 `hashCode` 值必须是相等。也就是说如果 `equals` 方法判断两个对象是相等的，那这两个对象的 `hashCode`值也要相等。如果重写 `equals()` 时没有重写 `hashCode()` 方法的话就可能会导致 `equals` 方法判断是相等的两个对象，`hashCode` 值却不相等。

1.  **`equals()` 方法**：这个方法用于比较两个对象是否相等。默认情况下，它与 `==`  运算符的作用相同，即比较两个对象的引用是否相同。但是，它可以被子类重写以实现自定义的相等比较逻辑。通常情况下，如果你重写了 `equals()` 方法，就应该同时重写 `hashCode()` 方法。
2.  **`hashCode()` 方法**：这个方法返回对象的哈希码值，哈希码是对象根据其内容生成的一个整数。哈希码通常用于确定对象在哈希表等数据结构中的存储位置。**如果两个对象通过 `equals()` 方法被判断为相等，那么它们的哈希码应该是相同的**。因此，如果你重写了 `equals()` 方法，就应该同时重写 `hashCode()`  方法，以确保对象在使用哈希表的集合中的正确行为。

在Java中，HashSet 是基于哈希表实现的集合类，它使用了哈希算法来存储元素，并提供了快速的插入、删除和查找操作。当我们向 HashSet 中添加元素时，HashSet 会使用每个元素的哈希码来确定其在内部数组中的存储位置，从而实现快速的查找。

然而，如果我们不重写 hashCode() 方法，而仅仅重写了 equals() 方法，那么在使用 HashSet 等基于哈希表的集合类时，可能会出现问题。这是因为默认的 hashCode() 方法是根据对象的内存地址生成的，如果两个对象的内存地址不同，它们的哈希码也会不同，即使它们的内容相同。这样就会导致相等的对象被视为不同的对象，从而影响 HashSet 的正确行为。