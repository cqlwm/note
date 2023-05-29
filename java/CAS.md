# CAS

## 什么是CAS

## 基于CAS的非阻塞无锁算法

为了在并发编程中保证线程安全，通常我们会对某个资源进行上锁。如果发生多个线程同时操作一个资源，那么只有拿到资源对应锁的一个或多个线程可以对该资源进行操作，其余线程都将陷入一种等待资源的阻塞状态当中。

如果拿到锁的线程由于一些I/O操作、或内存缺页、或超时网络请求等情况，那么很可能会出现所有需要锁资源的线程都不能继续执行下去。

因此，在基于锁的算法中可能会发生各种活跃性故障。

### 非阻塞？无锁？

1. 如果在某种算法中，一个线程的失败或挂起不会导致其他线程也失败或挂起，那么这种算法就被称为非阻塞算法。
2. 如果在算法的每个步骤中都存在某个线程能够执行下去，那么这种算法也被称为无锁（Lock-Free）算法。
3. 如果在算法中仅将CAS用于协调线程之间的操作，并且能正确地实现，那么它既是一种无阻塞算法，又是一种无锁算法。

> 在非阻塞的算法中，不会存在死锁，但却可能会存在活锁。
> 活锁：当线程获取锁失败之后会最终返回，不会始终阻塞，且在失败后反复重试。像这种反复获取锁、且最终获取不到的情况，一般被称为活锁。

### 非阻塞的栈

> 使用Treiber算法(Treiber, 1986)构造的非阻塞栈

```java
public class ConcurrentStack<E> {
    AtomicReference<Node<E>> top = new AtomicReference<Node<E>>();

    public void push(E item) {
        Node<E> newHead = new Node<E>(item);
        Node<E> oldHead;
        do {
            oldHead = top.get();
            newHead.next = oldHead;
        } while (!top.compareAndSet(oldHead, newHead));
    }

    public E pop() {
        Node<E> oldHead;
        Node<E> newHead;
        do {
            oldHead = top.get();
            if (oldHead == null) return null;
            newHead = oldHead.next;
        } while (!top.compareAndSet(oldHead, newHead));
        return oldHead.item;
    }

    private static class Node<E> {
        public final E item;
        public Node<E> next;

        public Node(E item) {
            this.item = item;
        }
    }
}
```

### CAS提供线程安全的根本原因

ConcurrentStack能够保证线程安全，或者说CAS能够保证线程安全的根本原因在于，在CAS的底层不仅提供了原子性，还提供了可见性。