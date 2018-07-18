### 对比Error和Exception,另外,运行时异常和一般异常有什么区别

Exception 和Error都继承了`Throwable`类, 在Java中只有`Throwable`类型的实例才可以被`抛出(throw)`或者`捕捉(catch)` ,它是异常处理机制的基本组成类型.

Exception 和 Error 提现了Java平台设计者对不同异常情况的分类.

Exception 是程序正常运行中,可以预料的意外情况,并且可以捕获,进行相应处理.

Error是正常程序下,不大可能出现的情况,绝大多数的Error会导致程序处于非正常的,不可恢复的状态.既然是非正常状态,所以不便于与不需要捕捉,常见的比如`OutOfMemoryError` 之类,都是Error的子类.

Exception 又分为可检查（checked）异常和不检检查（unchecked）异常，可检查异常在源代码里必须显式地进行捕获处理，这是编译期检查的一部分.

不检查异常就是所谓的运行时异常，类似 `NullPointerException` ,`ArrayIndexOutOfBoundsException` 之类,通常可以在代码中避免.



#### 知识拓展

- 掌握那些应用最为广泛的子类,以及如何自定义异常

- NoClassDefFoundError 和 ClassNotFoundException 有什么区别,也是经典的入门题

- try-catch-final块

  

  ```java
         /*
          * 这段代码的问题在于
          * 尽量不要捕获类似 Exception 这种通用异常,而是应该捕获特定异常
          * 不要生吞异常 ->
          *       如果我们不把异常抛出来,或者也没有输出日志,程序可能在后续以不可控的方式结束
          * */
          try{
              //业务代码
              Thread.sleep(1000L);
          } catch (Exception e){
  
          }
  
  ```



	#### 自定义异常

```java
public class CustomException extends Exception {
   public CustomException(){
       super();
   }
   public CustomException(String message){
       super(message);
   }
   public CustomException(Throwable cause){
       super(cause);
   }
   public CustomException(String message ,Throwable cause){
       super(message ,cause);
   }
}


public class TestException {
    public  void test(String params ) throws  CustomException{
        if(TextUtils.isEmpty(params))
         throw  new CustomException("不能为空");
    }
}

```



##### 从性能角度审视Java 的异常处理机制

- try -catch 代码会产生额外的性能开销, 它往往会影响JVM对代码进行优化 , 所以建议仅捕捉有必要的异常代码 

- java 每实例化一个Exception ,都会对当时的栈进行一次快照,这是一个相对比较中的操作,如果非常频繁,那就不能忽略不计了.

  





















