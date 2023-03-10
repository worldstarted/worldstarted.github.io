# Java核心技术

## 第三章 基本类型

不建议使用char类型的原因：

> 因为Unicode编码有时会占两个代码单元，造成两个char表示一个字符的情况，这样会导致程序出现未知错误。



Java对象变量与C++的引用有区别

> C++没有空引用，引用不能被赋值。
>
> Java的对象变量可以看错C++的对象指针。
>
> Date birthday ;//java
>
> Date* birthday; //c++
>
> 

堆栈的区别

> java中的对象基本都存放在堆中，由垃圾收集机制销毁。
>
> c++中的对象既有在堆中的，也有在堆栈中的，在堆栈中的，会随着作用域的结束而消亡，但在堆中的，则需要手动释放销毁。



 [Hashmap不适用于int,char](https://qa.1r1g.com/sf/ask/925142011/#)

通用参数只能绑定到引用类型,而不是基本类型,因此您需要使用相应的包装器类型.试试吧`HashMap<Character, Integer>`.

> 但是,我无法弄清楚为什么HashMap无法处理原始数据类型.

这是由于[类型擦除](http://docs.oracle.com/javase/tutorial/java/generics/erasure.html).Java从一开始就没有泛型,所以a `HashMap<Character, Integer>`真的是一个`HashMap<Object, Object>`.编译器会执行一系列额外的检查和隐式转换,以确保您不会输入错误类型的值或输出错误的类型,但在运行时只有一个`HashMap`类,它存储对象.

其他语言的"特殊化"类型在C++中,a `vector<bool>`与`vector<my_class>`内部非常不同,它们没有共同的`vector<?>`超类型.Java定义了一些东西,因此无论与向前通用代码的向后兼容性是什么,a `List<T>` [**都是一样的**](https://en.wikipedia.org/wiki/Is-a) .这种向后兼容性要求必须为泛型类型的所有参数化提供单个实现类,这防止了允许泛型参数绑定到基元的模板特化类型.`List``T`

泛型不能以关键字的形式使用原始类型.

## 第四章 对象和类

更改器方法和访问器方法

> 更改器方法：访问对象，并修改对象状态
>
> 访问器方法：访问对象，不修改对象状态
>
> 在C++当中，带有const后缀的方法是访问器方法

静态方法

