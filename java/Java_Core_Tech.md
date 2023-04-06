# Java核心技术

## 第三章 基本类型



> Java的数据类型分为基本数据类型和引用数据类型。
>
> int是基本数据类型，Integer是引用数据类型。

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



> 一个对象B引用另一个对象A，对A的修改会造成对B指向的对象的修改。
> 一个对象变量并没有实际包含一个对象，而仅仅引用一个对象。
> 对象变量存储的是对象的地址，实际上，对象存于堆中，通过对象变量的地址找到堆中的对象，对对象进一步操作。
>
> C++通过拷贝型构造器和复制操作符来实现对象的自动拷贝，而在Java种必须使用clone方法来获得对象的完整拷贝。



更改器方法和访问器方法

> 更改器方法：访问对象，并修改对象状态
>
> 访问器方法：访问对象，不修改对象状态
>
> 在C++当中，带有const后缀的方法是访问器方法，默认是更改器方法

> [在Java中，final关键字是一种非访问修饰符，用于表示一个变量、方法或类不能被修改或扩展](https://www.geeksforgeeks.org/final-keyword-in-java/)[1](https://www.geeksforgeeks.org/final-keyword-in-java/)[2](https://www.programiz.com/java-programming/final-keyword)[3](https://www.w3schools.com/java/ref_keyword_final.asp)。final关键字有以下特点：
>
> - [final变量：当一个变量被声明为final时，它的值不能被改变，只能被初始化一次](https://www.geeksforgeeks.org/final-keyword-in-java/)[1](https://www.geeksforgeeks.org/final-keyword-in-java/)[2](https://www.programiz.com/java-programming/final-keyword)[4](https://www.javatpoint.com/final-keyword)[。如果一个final变量没有赋值，它就是一个空白的final变量或未初始化的final变量，它只能在构造器中初始化](https://www.javatpoint.com/final-keyword)[4](https://www.javatpoint.com/final-keyword)。
> - [final方法：当一个方法被声明为final时，它不能被子类重写](https://www.geeksforgeeks.org/final-keyword-in-java/)[1](https://www.geeksforgeeks.org/final-keyword-in-java/)[2](https://www.programiz.com/java-programming/final-keyword)[3](https://www.w3schools.com/java/ref_keyword_final.asp)。这样可以防止子类改变父类的行为和逻辑。
> - [final类：当一个类被声明为final时，它不能被继承](https://www.geeksforgeeks.org/final-keyword-in-java/)[1](https://www.geeksforgeeks.org/final-keyword-in-java/)[2](https://www.programiz.com/java-programming/final-keyword)[3](https://www.w3schools.com/java/ref_keyword_final.asp)。这样可以防止类的层次结构过于复杂和混乱。
>
> 本地方法可以绕过Java语言的存取控制机制。例如可以修改final变量的值。

> ==静态方法==
>
> 静态方法不可以调用非静态方法。
>
> 非静态方法可以调用静态方法。
>
> 类的静态成员属于类本身，在类加载的时候就会被分配内存，可以通过类名直接去访问
> 类的非静态成员属于类的对象，只有在类的对象创建类的实例时，才会被分配内存，然后通过类的实例去访问。
>
> 静态方法调用非静态方法，非静态成员可能还不存在，没有this指针，无法访问实例变量和实例方法。

>==参数传递==
>
>```java
>class person{
>    private String name;
>    person(String name){
>        this.name = name;
>    }
>    public void showName(){
>        System.out.println(this.name);
>    }
>}
>public class Solution {
>	public static void swapName(person p1, person p2){
>        person t = p1;
>        p1 = p2;
>        p2 = t;
>    }
>
>    public static void main(String[] args) {
>        person p1 = new person("p1");
>        person p2 = new person("p2");
>        p1.showName(); // p1
>        p2.showName(); // p2
>        swapName(p1, p2);
>        p1.showName();// p1 
>        p2.showName();// p2
>    }
>}
>```
>
>Java对对象采用的不是引用调用，而是按值传递

### 构造器

> ==重载==
>
> 方法签名 -> 方法名+参数类型

> Java中this引用等价于C++的this指针，但在C++中，一个构造器不能调用另一个构造器。

> Java由于有自动的垃圾回收器，所以不支持析构器。可以为类添加`finalize`方法，此方法会在垃圾回收器清楚对象之前调用，但不建议用，因为不知道这个方法什么时候才会被调用。

## 第五章 继承

继承是复用，反射是在程序运行过程中发现更多的类及其属性的能力。

> 在Java中，所有的继承都是公有继承，没有C++的私有继承和保护继承。

> super不同于this，super不是一个对象的引用，不能将super赋给另一个对象变量，它只是一个指示编译器调用超类方法的特殊关键字。

> ==多态== 一个对象变量可以指示多种实际类型的现象。
>
> ==动态绑定==在运行时能够自动地选择调用哪个方法的现象。
> 	根据对象的实际类型生成方法表，虚拟机再进行查找

`is-a`规则的一种表述法：置换法则，程序中出现超类对象的任何地方都可以用子类对象置换。

==注意==，超类的引用不能赋给子类变量。

类声明为final，方法会自动成为final，域不会

> ==散列码==
>
> 字符串的散列码是由内容导出的。(String)
>
> StringBuffer没有定义hashCode方法，散列码由Object默认的hashCode方法导出的对象存储地址。
>
> 重新定义equals方法，就必须重定义hashCode方法，以便用户可以将对象插入到散列表中。
