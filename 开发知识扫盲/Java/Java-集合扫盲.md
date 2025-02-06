# Java集合扫盲

## 1. 集合概述

### 1. Java集合概览

Java集合分为两大类。即Collection和Map。

Collection支持使用迭代器Iterator遍历，而Map不支持。

Collection下有：

- List
- Set
- Queue

三个接口，各自的数据结构实现和用途都不同。

### 2. 说说不同集合之间区别 √

- List：有序，可重复
- Set：不可重复
- Queue：有序，先入先出，可重复
- Map：不可重复，键值对形式存储

### 3. 集合框架底层数据结构总结 √

- List

  - ArrayList：顺序表(数组)

  - LinkedList：链表

- Set

  - HashSet：数组＋链表 + 红黑树
  - TreeSet：红黑树
  - LinkedSet：数组 + 链表

- Map

  - HashMap：数组 + 链表 + 红黑树
  - TreeSet：红黑树
  - LinkedHashMap：数组+链表

- Queue：队列
  - ArrayQueue：双端数组
  - PriorityQueue：堆
  - DelayQueue：基于PriorityQueue实现

### 4. 如何选用集合 *

- 需要使用键值对获取值时，使用Map集合。
  - 不需要排序时，选用HashMap即可。
  - 需要排序时，选用TreeMap。
  - 需要实现线程安全时，选用ConcurrentHashMap。

- 需要保存值时使用Collection集合。
  - 需要保证元素唯一时，选用Set。
  - 需要保证元素可重复，且能够顺序或随机访问时选用List。

### 5. 为什么使用集合

（通常结合数组和集合的区别来回答）

对于一个语言而言，数组是最基本的实现。通过数组可以完成各种各样的数据结构。而集合的出现，就是为了简化开发者对数据结构的创建，JDK提供了丰富的数据结构以及API供开发者调用，避免重复造轮子。

因此，使用集合的最主要原因就是避免造轮子，通过泛型即可完成对各个类的数据结构操作。

## 2. List

### 1. ArrayList和Array的区别、Vector呢

- Array：即数组，最原始的数据结构，能够通过索引直接访问数据。
- ArrayList：List集合类的实现。底层是Array，特点是可扩容，提供丰富的API对底层数组进行操作。
- Vector：List集合类的实现。和ArrayList的区别是该类线程安全。但是性能较差。

### 2. ArrayList可以添加null值吗

可以。

### 3. ArrayList/LinkedList插入和删除元素的时间复杂度

- ArrayList：
  - 插入/删除时间复杂度：如果是追加操作，则时间复杂度为O(1)。如果是中间操作，则时间复杂度为O(n)。
- LinkedList：
  - 插入/删除时间复杂度：如果是头尾操作，则为O(1)。如果是指定位置操作，则为O(n)。

### 4. LinkedList为什么不能实现RandomAccess接口

RandomAccess是一个标记型接口，旨在声明该类可以被随机访问。而LinkedList无法随机访问。

### 5. ArrayList和LinkedList区别

- 数据结构上：ArrayList底层是数组，而LinkedList底层是链表。
- 继承/实现类列表不同。
- 剩下的区别，就是数组和链表的区别了。

### 6. ArrayList扩容机制

#### 1.  初始化插入

在ArrayList没有传入capacity参数时，底层默认为一个空数组。当第一次add时，会触发扩容机制。此时会为数组分配空间。初次通常分配capacity=10的空间。

#### 2. 扩容

当ArrayList的某次add将会让size等于最大容量时，会先触发扩容，再add该对象。扩容策略是将最大容量变为原来的1.5倍。

## 3. Set

### Comparable和Comparator的区别 *

![image-20241102153325190](https://web-tilas-zhaozhong.oss-cn-shenzhen.aliyuncs.com/zhaozhong-typora-resources/202411021533282.png)

### 无序性和不可重复性的含义是？

无序性：指Set的添加是顺序与获取顺序不同。

不可重复性：指Set集合中不能存在相同的元素。

## 4. Queue

### 1. Queue与Deque的区别

#### Queue

Queue是JDK1.5出来的，底层数据结构是单端队列，符合先入先出原则，通常用于实现阻塞队列。

#### Deque

Deque是JDK1.6出来的，继承并扩展了Queue，Deque的底层数据结构是双端队列，主要用于实现队列或栈。

### 2. ArrayDeque与linkedList的区别

1. 实现形式：ArrayDeque通过可变长数组和双指针实现的，而LinkedList是通过链表实现的。
2. 插入形式：ArrayDeque通过循环数组+双指针来定位头尾，插入时可能会触发扩容。LinkedList每次插入都会new一个对象。
3. ArrayDeque插入null会报空指针异常，而LinkedList可以插入null。
4. 

### 3. 说说PriorityQueue



### 4. 什么是BlockingQueue？以及其实现类 *



## 5. Map

### 1. HashMap和 HashTable的区别

- 线程安全：HashMap线程不安全，HashTable线程安全。
- 效率：因为HashTable所有操作都上了重量级锁，所以效率比HashMap低很多。
- 是否支持存null：HashTable不支持null键和null值的保存，hashMap可以保存一个null键，多个null值。
- 哈希冲突的解决：HashMap在1.8后通过红黑树解决链过长的问题，而HashTable保持使用拉链法。

### 2. HashMap和HashSet的区别

- 存储方式：HashMap以键值对形式存储。HashSet只存储值。
- 取值方式：HashMap以键获取值，而HashSet中一般不取值。

### 3. HashMap和TreeMap的区别 *

1. TreeMap可根据Comparator或Comparable中的compare方法对元素进行排序。HashMap则是乱序的。
2. 底层数据结构：TreeMap是根据红黑树实现的，而HashMap是根据数组+链表+红黑树实现的。

### 4. HashSet如何检查重复？

HashSet通过HashMap的Key来检查重复。因为HashMap的Key是不可重复的。

### 5. HashMap的底层实现

HashMap底层使用数组存储元素，hash冲突采用了拉链法解决。在1.8后，当链长达到一定程度时，为了降低时间复杂度，将链表红黑树化。

### 6. HashMap的长度为什么是2的n次方 *

1. hashMap扩容时用到了`&`来取余，以减少调用hashCode的次数，这需要2的n次方才能做到，位运算能够使效率更高。
2. 在重新hash的过程中，2的n次方能够使元素分布更平均。

### 7. HashMap的多线程操作导致死循环的情况 *

在1.7中，hashMap是采用头插法进行拉链的。因此在扩容的时候会发生链表倒置。假如有两个线程，线程1执行完扩容，将链表倒置后，线程2还是原来的链表结构，就会导致循环链表，遍历无法结束的问题。

1.8中，HashMap改用尾插法进行拉链，解决了链表倒置问题。

### 8. HashMap为什么线程不安全

HashMap没有做任何的线程同步操作，因此必然会出现某个时刻的值覆盖等问题。

### 9. HashMap常见的遍历方式 √

1. EntrySet
2. KeySet
3. HashMap::foreach - lambda
4. Streams API

### 10. ConcurrentHashMap和HashTable的区别

#### 1. 线程安全的实现方式

ConcurrentHashMap在1.7中通过分段锁实现，在1.8中通过CAS和Synchronized实现。比HashTable对每个操作都上重量级锁性能更佳。

#### 2. 其他

其他的区别和HashMap/HashTable的区别一致。

### 11. ConcurrentHashMap线程安全如何保证

#### 1.7

通过分段锁实现。在1.7的ConcurrentHashMap中，默认有16个段，hashMap通过为这些段上悲观锁来实现线程安全。这相比HashTable锁全表的好处是，如果不是同一个段内的数据，是可以同时操作的。

#### 1.8

显然，分段锁的粒度还是很大，因为一次操作就会锁住一段不相干的数据。在1.8中，ConcurrentHashMap使用了粒度更小的CAS锁住桶元素，同时使用Synchronized对拉链或树化的数据上锁。这样做的好处是锁的粒度更小，同时使用CAS进行操作的效率十分高。

### 12. JDK1.7和1.8ConcurrentHashMap的实现

- 锁粒度：1.7通过分段锁实现，默认最多支持16的并发量。而1.8通过CAS+Synchronized实现，最多支持size的并发量。
- 哈希冲突解决：1.7采用拉链法，1.8为了解决链长过长的问题，引入链转树的方法。

### 13. ConcurrentHashMap为什么key不能为空

key为空在单线程环境下是没有问题的，

### 14. ConcurrentHashMap能保证复合操作的原子性吗 *

不能。但是可以使用复合操作的API来保证原子性。



