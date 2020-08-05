Java 4种引用关系

1 强引用

概念 被强引用关联的对象不会被回收。

使用 new 一个新对象的方式创建强引用。 

```java
Object obj = new Object();
```

2 弱引用

被弱引用关联的对象一定会被回收，也就是说它只能存活到下一次垃圾回收发生之前。

使用 WeakReference 类来创建弱引用。

```java
Object obj=new Object();
WeakReference<Object> wf=new WeakReference<Object>(obj);
obj=null;
```



3 虚引用

又称为 幽灵引用 或者幻影引用，一个对象是否有虚引用的存在，不会对其生存时间造成影响，也无法通过虚引用得到一个对象。

为一个对象设置虚引用的唯一目的是能在这个对象被回收时收到一个系统的通知。

使用PhantomReference 来创建虚引用。

```java
Object obj=new Object();
PhantomReference<Object> pf=new PhantomReference<object>(obj,null);
obj=null;

```

4 软引用

被软引用关联的对象只有在内存不够的情况下才会被回收。

使用SoftReference 类 来创建软引用。

```java
Object obj=new Object();
SoftReference<Object> sf=new SoftReference<Object>(obj);
obj=null // 使对象只能被软引用关联。
```





