### 谈谈 final  finally  finalize 的区别

final  可以用来修饰类,方法,变量,分别有不同的意义 , final 修饰的class代表不可以被继承扩展,final的变量是不可以修改的,final的方法不可以被重写(override)

finally 则是java 保证重点代码一定要执行的一种机制. 我们可以使用 try -catch -final 来进行类似关闭JDBC连接 的操作

finalize 是基础类java.Util.Object中的一个方法,它的目的是保证垃圾收集前完成特定资源的回收, final 机制现在已经不推荐使用

