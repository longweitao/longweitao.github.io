###谈谈对<strong>Java</strong>的理解,"Java是解释执行"这句话对吗？

从接触到Java到现在，对它最直观的理解就是 **Write once, run anywhere**

Java本身是一种面向对象语言，最显著的特性有两个方面，一是所谓的“一次书写，到处运行”，能够非常容易的获得跨平台能力；另外就是所谓的垃圾收集（GC）, Java通过垃圾收集器（GC）回收分配内存，大部分情况下，程序员不需要自己操心内存的分配和回收。

我们日常会接触到 `JRE` 或者 `JDK` 。`JRE`也就是java运行环境，包含了`java类库`和`JVM`以及一些模块等。而`JDK`可以看作是`JRE`的一个超集，提供了更多的更多工具，如比编译器，各种诊断工具等。

对于`java是解释执行`这句话，这个说法不太准确。我们开发的java源代码，首先通过`javac`编译成字节码（bytecode）,然后在执行时，通过java虚拟机（JVM）内置的解释器讲字节码转换成为最终的机器码。但是常见的 JVM，比如我们大多数情况使用的 Oracle JDK 提供的 Hotspot JVM，都提供了 JIT （Just-In-Time）编译器，也就是通常所说的动态编译成机器码，这种情况下部分热点代码就属于编译执行，而不是解释执行了。

####知识拓展

Java语言特性，包括泛型、Lambda等语言特性; 基础类库，包括集合、IO\NIO、网络、并发、安全等基础类库。



####泛型

根据[《Java编程思想 （第4版）》](http://book.douban.com/subject/2130190/)中的描述，泛型出现的动机在于：

> 有许多原因促成了泛型的出现,而最引人注意的个原因,就是为了创造**容器类**.

#####什么是泛型

> 泛型是Java SE 1.5 的新特性，泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。这种参数类型可以用在类、接口和方法的创建中。分别成为泛型类、泛型接口、泛型方法。Java中引进泛型的好处是安全简单。

- 泛型的类型参数只能是类类型,不能是简单类型。
- 同一种泛型可以对应多个版本（因为参数类型是不确定的），不同版本的泛型类实例是不兼容的。
- 泛型的类型参数可以有多个。
- 泛型的参数类型可以使用extends语句，例如<T extends superclass>。习惯上称为“有界类型”。
- 泛型的参数类型还可以是通配符类型。例如Class<?> classType = Class.forName("java.lang.String");



#####泛型类

```java

public class ObjectTool<T> {
    private T obj;
    
    public void setObj(T obj) {
        this.obj = obj;
    }

    public T getObje() {
        return obj;
    }
}


public class ObjectDemo {
    public  static void main(String[] args){
        ObjectTool<String>  tool1 = new ObjectTool<>();
        tool1.setObj("中国");
        System.out.print(tool1.getObje());
        ObjectTool<Integer> tool2 = new ObjectTool<>();
        tool2.setObj(2);
    }
}

```



#####泛型方法

```java
public class ObjectTool {
    public <T> void show(T t){
        System.out.print(t.toString());
    }
}

public class ObjectDemo {
    public static void main(String[] args) {
        ObjectTool tool = new ObjectTool();
        tool.show("中国");
        tool.show(1);
    }
}

```



#####泛型接口 把泛型定义在接口上

格式 : public  interface 接口名<泛型类型>

```java
public class ObjectTool {
    public <T> void show(T t){
        System.out.print(t.toString());
    }

    public  interface  toolInterface<T>{
          void tool(T t);
    }
}

public class ObjectDemo  implements ObjectTool.toolInterface<Integer> {
    public static void main(String[] args) {
        ObjectTool tool = new ObjectTool();
        tool.show("中国");
        tool.show(1);
    }

    @Override
    public void tool(Integer t) {

    }
}


```



####集合

Collection
├List
│├LinkedList  //双向链表,查找效率低
│├ArrayList   //插入删除效率低
│└Vector
│　└Stack
└Set
Map
├Hashtable
├HashMap
└WeakHashMap

#####Set和List的区别

- Set 接口实例存储的是无序的，不重复的数据。List 接口实例存储的是有序的，可以重复的元素。
- Set检索效率低下，删除和插入效率高，插入和删除不会引起元素位置改变 **<实现类有HashSet,TreeSet>**。
- List和数组类似，可以动态增长，根据实际存储的数据的长度自动增长List的长度。查找元素效率高，插入删除效率低，因为会引起其他元素位置改变 **<实现类有ArrayList,LinkedList,Vector>** 。



```java
public class ListDemo { //遍历ArrayList

    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Hello");
        list.add("Hello");
        list.add("Hello");
        //使用foreach遍历list
        for (String str : list) {
            System.out.print(str);
        }
        //把链表变为数组相关的内容进行遍历
        String[] strArray = new String[list.size()];
        list.toArray(strArray);
        for (String aStrArray : strArray) {
            System.out.print(aStrArray);
        }
        //使用迭代器进行相关遍历
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) { //判断下一个元素之后有值
            System.out.println(iterator.next());
        }
    }
    
}

```

 

```
public class MapDemo {
    //遍历map
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();
        map.put("1", "value1");
        map.put("2", "value2");
        map.put("3", "value3");

        //普遍使用,二次取值
        for (String key : map.keySet()) {
            System.out.print(map.get(key));
        }
        /*
        * Map.Entry 描述在一个Map中的一个元素（键/值对）。是一个Map的内部类。
        * */
        //通过Map.entrySet使用iterator遍历key和value：
        Iterator<Map.Entry<String, String>> iterator = map.entrySet().iterator();
        while (iterator.hasNext()) {
            Map.Entry<String, String> next = iterator.next();
            System.out.print(next.getKey() + "-" + next.getValue());
        }
        // 通过Map.entrySet遍历key和value  推荐，尤其是容量大时
        for(Map.Entry<String, String> entries : map.entrySet()){
            System.out.print(entries.getKey() + "-" + entries.getValue());
        }
        //通过Map.values()遍历所有的value，但不能遍历key
        for(String value : map.values()){
            System.out.print(value);
        }

    }
}

```



####比较器  使用 Java Comparator