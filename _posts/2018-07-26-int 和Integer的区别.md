### int 和Integer的区别

- Int 是一个基本的数据类型 ,而Integer 是int 的包装类;
- Integer变量必须实例化之后才能使用,而int不需要;
- Integer 是对象,是一个引用指向这个对象,而int是基本类型,直接存储数值;
- Integer默认值是null ,而int是0;



####  知识扩展

 1 . 由于Integer变量实际是对`对象` 的引用 ,所以两个`通过new生成` 的Integer是永远不可能相等的. 

```java
 		Integer integer1 = new Integer(100);
        Integer integer2 = new Integer(100);
        System.out.println(integer1 == integer2); //false

```



2. Integer变量 和int变量比较时 ,只有两个变量的值相同,则结果一定是相同的 ,(`因为包装类型Integer和int基本数据类型比较时,会自动拆箱成int类型,实际就是两个int类型的比较 ` )

   

   ```
   		Integer integer1 = new Integer(100);
           int i = 100;
           System.out.println(integer1 == i); //true
   ```

   

3. 非new 生成的Integer变量和new生成的Integer变量比较结果,结果为false ,(因为非new 生成的Integer变量,指向的事java常量池中的对象,而new生成的对象是指向堆中新建的对象)

```java

        Integer integer1 = new Integer(100);
        Integer integer3 = 100;
        System.out.println(integer3 == integer1);  //false

```

4. 对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false

   ```java
           Integer i1 = 100;
           Integer i2 = 100;
   
           System.out.println(i1 ==i2); //true
   
   ```

   ```java
           Integer i3 = 128;
           Integer i4 = 128;
           System.out.println(i3 == i4); //false
   
   ```

   