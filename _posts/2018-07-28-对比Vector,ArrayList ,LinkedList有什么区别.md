### 对比Vector,ArrayList ,LinkedList有什么区别

三者都实现集合框架中的`List`  ,也就是所谓的`有序集合`  ,因此功能也比较相近 ,比如都提供按照位置进行`定位`  ,`添加` 或者`删除` 操作,都提供迭代器以遍历器内容等.但因为具体的设计区别,在行为,线程,安全等方面,表现又有很大不同.

**Vector** 是java早期提供的线程安全的动态数组 ,如果不需要线程安全,不建议使用,毕竟同步是有额外开销的. Vector内部是使用`对象数组` 来保存数据 ,可以根据需要自动的增加容量，当数组已满时，会创建新的数组，并拷贝原有数组数据。

**ArrayList** 是应用更加广泛的**动态数组** 实现,它本身不具备线程安全,所以性能要好很多.与Vector相似 ,ArrayList也需要调整容量,不过两者的调整逻辑有不同的区别 ,Vector在扩容时会增加一倍,而ArrayList会增加50%

**LinkedList** 是java提供的双向链表,所以不需要调整容量 ,也不是线程安全的. 进行节点`插入` ,`删除` 要高效很多.但随即访问的性能要比动态数组慢



#### 知识扩展

List   存储一组不唯一,有序的对象

Set 存储一组唯一,无序的对象

Map 存储一组键值对,提过  key 到 value  的映射

在Java9中 ,java标准库 提供了一系列的静态工厂方法 ,比如List.of() ,Set.of() , 大大简化了构建小的容器实例的代码量.

```java
        ArrayList<String> arrayList = new ArrayList<>();
        arrayList.add("Hello");
        arrayList.add("World");

        //而利用新的容器静态工厂方法，一句代码就够了，并且保证了不可变性
        List<String>  list = List.of("Hello" ,"World");

```



##### 内部排序 :     

-  归并排序

  -  是将两个或者两个以上的有序表合并成一个有序表 .归并排序是建立在归并操作上的一种有效的排序算法 .该算法是采用分治发的一个典型的应用.

-  交换排序 (冒泡,快排)  两两比较待排序元素的关键字 .

  - 冒泡排序 ,是众多排序算法中比较简单的一个 .在要排序的一组数种 ,对当前还未拍好序的范围内所有数 ,自上而下相邻的两个数依次比较和调整,让比较大的下沉,较小的往上冒 .

  - ```java
        public static void main(String[] args) {
            int[] a = {1, 4, 2, 6, 5, 3, 7, 9, 8, 0};
            System.out.println(Arrays.toString(function(a)));
        }
    
        private static int[] function(int[] a) {
            for (int i = 0; i < a.length; i++) {
                for (int j = a.length - 1; j > i; j--) {
                    if (a[j] < a[j - 1]) {
                        int temp = a[j];
                        a[j] = a[j - 1];
                        a[j - 1] = temp;
                    }
                }
            }
            return a;
        }
    
    ```

  - 

- 选择排序

  - 在一次遍历种找到元素关键字最小的元素的角标位置 ,然后把他放到数组的首端.

- 插入排序 

##### 外部排序 

掌握利用内存和外部存储处理超大数据集，至少要理解过程和思路。





