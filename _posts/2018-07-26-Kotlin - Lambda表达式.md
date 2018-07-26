### Kotlin - Lambda表达式

##### Lambad表达式 的特点

- 匿名函数
- 写法 :  {[参数列表] -> [函数体 ,最后一行作为返回值]}
- 举例   val  sum = {arg1 :Int ,arg2 :Int -> arg1 +arg2}

##### Lambda 的类型表示事例

- () -> Unit   

     	 <font  color =#0099ff  > 无参 ,返回值为Unit   </font> 

- (Int)  -> Int

  ​       <font  color =#0099ff > 传入一个Int  ,返回一个 Int </font>

- (String ,(String)->String) -> Boolean

  ​       <font  color =#0099ff >  传入一字符串,一个Lambda表达式  ,返回一个Boolean </font> 

##### Lambda 表达式如何调用

- 用 () 进行调用
- 等价于invoke()

##### Lambda表达式的简化 

- 函数参数调用是最后一个Lambda可以移出去

- 函数参数只有一个Lambda  ,调用的小括号可以省略

- Lambda 只有一个参数,可以默认为 it  ,可以不在代码中表现出来

- 入参 ,返回值 与形参一致的函数可以用函数引用的方式作为实参传入

  

```kotlin
  //普通函数
    fun sum(arg1: Int, arg2: Int) = arg1 + arg2

    /*
    * lambda  (Int ,Int) -> Int 类型
    * 使用 -> 分割参数与返回值
    * 函数体的最后异常作为返回值
    * 如果没有如参,则可以省略 ->
    */
    val sum = { arg1: Int, arg2: Int ->
        println("$arg1 + $arg2")  // (Any?) -> Unit 类型
        arg1 + arg2
    }

    fun main(args: Array<String>) {
        //使用lambda
        println(sum(1 ,2))
        println(sum.invoke(1 ,2))  //invoke() 运算符重载

        //遍历
        args.forEach { { println(it)} }

    }
	// 如果没有如参,则可以省略 ->
    val printHello = { println("Hello") }   // () -> Unit 类型

```



以 `forEach` 为例 , 变量一个数组

```kotlin
         args.forEach {
            println(it)
        }

```



点击查看`forEach`  的源码 

```kotlin
        /**
         * Performs the given [action] on each element.
         */
        public inline fun <T> Array<out T>.forEach(action: (T) -> Unit): Unit {
            for (element in this) action(element)
        }
```

通过源码可以看出 ,forEach 是Array的一个扩展方法 , 有一个泛型 T , 传入一个 Lambad 表达式为 ` (action : (T) -> Unit)`  类型 ,返回一个 Unit   ,可以得知原始写法

```kotlin
        args.forEach ({ it -> println(it)})
```

继续简写 , 如果一个函数的最后一个参数是一个Lambda表达式 ,则可以把这个Lambda提出来

```kotlin
        args.forEach() { 
            it -> println(it)
        }
```

继续 ,如果 ,只有这个Lambda一个参数,那可以省略 ()

```kotlin
		args.forEach{ 
            it -> println(it)  // 然后继续,Lambda只有一个入参 , 则省略参数
        }
        
        args.forEach{println(it)} //最终
```

#### return 一个forEach

```
    fun main(args: Array<String>) {
        args.forEach(){
            if(it == "a") return 
            //错误写法 , lambda 并不是一个函数,此处return  直接return了main()
            println(it)
        }
        println("The End")   //不会执行
    }
    
    
     fun main(args: Array<String>) {
        args.forEach()forEach@{ //添加一个forEach@ 标签 
            if(it == "a") return@forEach   //在次条件下终止迭代
            println(it)
        }
        println("The End")
    }


```



#### Lambda表达式也有自己的类型

```
 val printHello = { println("Hello") }   // () -> Unit 类型

 println("$arg1 + $arg2")  // (Any?) -> Unit 类型
```







