### 理解字符串 ,String StringBuffer ,StringBuilder有什么区别

```String```   是java语言中非常基础和重要的类,提供了构造和管理字符串的各种逻辑,它是典型的Immutable类,被声明为final class ,所有属性也都是final的 ,由于它的不可变性 ,类似,拼接,裁剪字符串的操作 ,都会生成一个新的String对象,由于字符串操作的普遍性，所以相关操作的效率往往对应用性能有明显影响 .

`StringBuffer` 是为解决上面提到字符串频繁拼接产生过多对象问题而提供的一个类,我们可以用append和add方法,把字符串添加到已有序列的末尾或制定位置.StringBuffer本质是一个线程安全的可修改字符序列,它保证了线程安全, 随之带来了额外的开销,所以除非有线程安全的必要,否则推荐使用`StringBuilder` 

`StringBuilder` 是java1.5中新增的,在能力上和`StringBuffer` 没什么区别,只不过去除了线程安全,有效的减少了开销.是绝大部分情况下进行字符串拼接的首选





