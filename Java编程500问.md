[TOC]

# JAVA问题500问

###### **[Typora 完全使用详解 ](https://sspai.com/post/54912#!)**

## 1、Java中&&和&，||和|的区别

### & &&

java当中的逻辑运算符，&&（短路与）和&表示逻辑与，||（短路或）和|表示逻辑或

不同点是&&只要是第一个条件不成立为false，就不会再去判断第二个条件，最终结果直接为false，而&判断的是所有的条件；

**测试&&：**

```java
package test;
 
public class Test{
	public static void main(String[] args){
		int i = 23;
		int j = 21;
		if ((i == j) && (100 / 0 == 0))
			System.out.println("1");
		else
			System.out.println("没有报错");
	}
}
```

输出的结果为：没有报错

正常情况下100 / 0 == 0是会报错的，而上面的示例就没有报错，就是因为&&的第一个条件不成立，后面的一个条件被短路了，所以程序没有报错

### | ||

||和|都表示逻辑或，共同点是只要两个判断条件其中有一个成立最终的结果就是true，区别是||只要满足第一个条件，后面的条件就不再判断，而|要对所有的条件进行判断。	

## 2、[java语言中数值自动转换的优先顺序](https://www.cnblogs.com/zhengfengyun/p/5091282.html)

```note
自动转换按从低到高的顺序转换。不同类型数据间的优先关系如下：
    低--------------------------------------------->高
    byte,short,char-> int -> long -> float -> double
```

## 3、Java运算符优先级

| 优先级 | 运算符                                           | 结合性   |
| ------ | ------------------------------------------------ | -------- |
| 1      | ()、[]、{}                                       | 从左向右 |
| 2      | !、+、-、~、++、--                               | 从右向左 |
| 3      | *、/、%                                          | 从左向右 |
| 4      | +、-                                             | 从左向右 |
| 5      | «、»、>>>                                        | 从左向右 |
| 6      | <、<=、>、>=、instanceof                         | 从左向右 |
| 7      | ==、!=                                           | 从左向右 |
| 8      | &                                                | 从左向右 |
| 9      | ^                                                | 从左向右 |
| 10     | \|                                               | 从左向右 |
| 11     | &&                                               | 从左向右 |
| 12     | \|\|                                             | 从左向右 |
| 13     | ?:                                               | 从右向左 |
| 14     | =、+=、-=、*=、/=、&=、\|=、^=、~=、«=、»=、>>>= | 从右向左 |

## 4、静态方法如何引用实例变量(通过对象引用？)

![image-20210924090907496](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20210924090907496.png)

```java
public class Person {
	String name = "1";
	static int age;
	int time = 1;
	
	//构造方法（无返回值）
	public Person() {
		
	}
	public void static work(int time,Person p) {//方法第一个字母小写
		time = 12;//局部变量必须初始化
		p.setTime(20);
		System.out.println("I'm working."+time);
		System.out.println("time is."+this.time);//this出现在哪个类中间，this代表这个类的对象，是对象，不是类
	}
```

## 5、Java中的静态方法、静态变量以及实例方法、实例变量

静态方法（static method）
先从一道笔试题说起

关于Java中的静态方法，下列说法哪些是正确的（）
A：静态方法是一个属于类而不属于对象(实例)的方法。（√）

    静态方法可以在没有创建对象实例的情况下调用，其是可以通过类名引用。

B：静态方法只能访问静态数据。无法访问非静态数据(实例变量)。（√）

    它这边的意思是不能直接访问非静态数据（实例变量），因为非静态数据是属于对象属性的，其只有在对象存在的时候才能引用。

C：静态方法只能调用其他静态方法，不能从中调用非静态方法。（√）

    这里也是不能直接调用非静态方法，因为非静态方法是属于某个对象的，不先实例化对象，通过对象引用，那么将无法判断具体调用哪个对象（实例）的非静态方法。

D：静态方法不能通过类名直接访问，也不需要任何对象。（×） 静态方法可以直接用类名访问。

    类名.静态方法名() 这种方式是可以的，所以静态方法可以直接通过类名进行访问。

简单总结

先总结：

    （1）静态方法中不可以直接引用实例方法（非静态方法）或实例成员变量（非静态变量）；
    
    静态方法中引用实例方法、实例变量，须先实例化对象，然后通过 对象名.实例变量名 和 对象名.实例方法名( )
    
    （2）静态方法、实例方法（非静态方法）都可以引用静态变量、静态方法；
        如果在不同类中，则是通过 类名.静态变量名 和 类名.静态方法名( ) 的方式引用；
        如果是在同一个类中，则可以省略类名；
    
    当然，要想其他类能引用其静态变量、静态方法，则其不能将这些变量、方法设置为private。
    
    （3）实例方法（非静态方法）中引用实例变量、其他实例方法；
        如果在不同类中，则需要先实例化对象，通过对象进行引用；
        如果在同一个类中，则直接引用即可；										//实例变量不可以通过类名访问
    （4）引用（调用）静态方法的方式有两种：
        类名.静态方法名( )
        先实例化一个对象，然后通过 对象名.静态方法名( )
    
    （5）静态方法中不能使用 this 和 super ，而实例方法可以；

具体案例

通过下面的案例，可以对上面所述内容有个更加清晰的认识。

##### StaticMethodTest1

```java
package com.yuan.test;

public class StaticMethodTest1 {
    private static int staticVariable;//静态成员变量
    public static int publicStaticVariable;
    protected static int protectedStaticVariable;
    private int instanceVariable;//实例成员变量（非静态成员变量）
public static void staticMethod1(){
    staticVariable = 166;//静态方法中引用静态变量
    publicStaticVariable = 101;
    protectedStaticVariable = 102;
    System.out.println("StaticMethodTest1's staticVariable ="+staticVariable);
    /*
    Non-static field 'instanceVariable' cannot be referenced from a static context
    不能从静态上下文中引用非静态变量
     */
    //instanceVariable = 555;

    /*
    Non-static method 'instanceMethod()' cannot be referenced from a static context
    不能从静态上下文中引用非静态方法（实例方法）的
     */
    //instanceMethod1();

    staticMethod2();//在当前类中的静态方法中调用当前类的其它静态方法（可省略类名）
}

public void instanceMethod1(){
    // 实例方法（非静态方法）中是可以引用非静态变量（实例成员变量）的
    instanceVariable = 100;
    // 实例方法也可以引用静态变量
    staticVariable = 177;
}

public static void staticMethod2(){
    staticVariable = 188;
}

public static void main(String[] args){
    StaticMethodTest1 staticMethodTest1 = new StaticMethodTest1();
    staticMethodTest1.instanceMethod1();
    // main方法是典型的静态方法，所以引用实例变量须通过实例对象
    System.out.println(staticMethodTest1.instanceVariable);
    System.out.println(staticVariable);

    staticMethod1();//在当前类中调用静态方法，可以省略类名
    System.out.println(staticVariable);
    System.out.println(publicStaticVariable);
    System.out.println(protectedStaticVariable);
}
}
```
###### 运行后结果为：

**100**
**177**
**StaticMethodTest1's staticVariable =166**
**188**
**101**
**102**

##### StaticMethodTest2

```java
package com.yuan.test;

public class StaticMethodTest2 {
    private static int staticVariable;
    public static int publicStaticVariable;
public static void staticMethod1(){
    // 通过类名直接引用StaticMethodTest1类的静态方法staticMethod1
    // 引用其他类的静态方法（类名.静态方法名()）
    StaticMethodTest1.staticMethod1();
    // 修改当前类中的静态变量，可以省略类名
    staticVariable = 222;
    publicStaticVariable = 221;
    // 修改其它类中的静态变量（类名.静态变量名），注意：其它类的静态变量不能是private的
    StaticMethodTest1.publicStaticVariable = 201;
    StaticMethodTest1.protectedStaticVariable = 202;
    // 除了可以使用类名直接调用静态方法，还可以通过实例对象调用静态方法
    StaticMethodTest1 staticMethodTest1 = new StaticMethodTest1();
    staticMethodTest1.staticMethod1();//会将其publicStaticVariable、protectedStaticVariable 的值又改回101、102 
}

public static void main(String[] args){
    staticMethod1();
    // 引用其他类的静态变量（类名.静态变量名）
    System.out.println(StaticMethodTest1.publicStaticVariable);
    System.out.println(StaticMethodTest1.protectedStaticVariable);
    // 引用当前类的静态变量
    System.out.println(publicStaticVariable);
}
}
```

###### 运行结果为：

**StaticMethodTest1's staticVariable =166**
**StaticMethodTest1's staticVariable =166**
**101**
**102**
**221**

## 6、[eclipse源码中文注释乱码问题解决方法](https://blog.csdn.net/xiongyouqiang/article/details/80334608)

## 7、[Java 中 Comparable 接口的意义和用法](https://blog.csdn.net/nvd11/article/details/27393445)

在之前的博文中已经介绍了Java中Collection 接口和 Collections类.

http://blog.csdn.net/nvd11/article/details/21516075


一, 为何需要实现Comparable接口

我们知道Collections类中包含很多对实现Collection接口的容器各种操作的静态方法.

当然, 其中最长用的莫过于排序了(Collections.sort(List l).


下面是1个简单例子:

    public class Compare1{
        public static void f(){
            ArrayList arr = new ArrayList();
            arr.add(10);
            arr.add(23);
            arr.add(7);
     
            System.out.println(arr);
     
            Collections.sort(arr);
            
            System.out.println(arr);
        } 
    }


逻辑很简单, 就是在1个list容器中添加3个int数值(注意实际被自动装箱成Interger对象).

正常输出容器元素一次, 利用Collections.sort()方法排序后, 再输出1次.


输出:

       [java] [10, 23, 7]
       [java] [7, 10, 23]



但是当List容器添加的元素对象是属于自己写的类时, 就可能出问题了.

例子:

    import java.util.ArrayList;
    import java.util.Collections;
     
    class Student{
        private String name;
        private int ranking;
     
        public Student(String name, int ranking){
            this.name = name;
            this.ranking = ranking;
        } 
     
        public String toString(){
            return this.name + ":" + this.ranking;
        }
    }
     
    public class Compare2{
        public static void f(){
            ArrayList arr = new ArrayList();
            arr.add(new Student("Jack",10));
            arr.add(new Student("Bill",23));
            arr.add(new Student("Rudy",7));
     
            System.out.println(arr);
        } 
    }


上面定义了1个Student类, 它只有两个成员, 名字和排名.

在f()方法内, 添加3个Student的对象到1个list容器中, 然后输出(必须重写String方法, 这里不解释了):

[java] [Jack:10, Bill:23, Rudy:7]


到此为止, 是没有问题的.  但是当我对这个容器进行排序时就有问题了.

例如将上面的f()方法改成:

    public class Compare2{
        public static void f(){
            ArrayList arr = new ArrayList();
            arr.add(new Student("Jack",10));
            arr.add(new Student("Bill",23));
            arr.add(new Student("Rudy",7));
     
            System.out.println(arr);
            Collections.sort(arr);
            System.out.println(arr);
        } 
    }


编译时就会出错:

 [java] Caused by: java.lang.ClassCastException: Collection_kng.Comparable_kng.Student cannot be cast to java.lang.Comparable


提示这个类Student没有实现Comparable接口.

原因也很简单, 因为Java不知道应该怎样为Student对象排序, 是应该按名字排序? 还是按ranking来排序?


为什么本文第1个例子就排序成功? 是因为Java本身提供的类Integer已经实现了Comparable接口. 也表明Integer这个类的对象是可以比较的.


而Student类的对象默认是不可以比较的.  除非它实现了Comparable接口.


总而言之,  如果你想1个类的对象支持比较(排序), 就必须实现Comparable接口.


二, Comparable接口简介.

Comparable 接口内部只有1个要重写的关键的方法.

就是

int compareTo(T o)

这个方法返回1个Int数值,  

例如 i = x.compareTo(y)

如果i=0, 也表明对象x与y排位上是相等的(并非意味x.equals(y) = true, 但是jdk api上强烈建议这样处理)

如果返回数值i>0 则意味者, x > y啦，　

反之若i<0则　意味x < y


三, Comparable接口的实现及用法.
用回上面的例子，　我们修改Student类, 令其实现Comparable接口并重写compareTo方法.

    import java.util.ArrayList;
    import java.util.Collections;
     
    class Student implements Comparable{
        private String name;
        private int ranking;
     
        public Student(String name, int ranking){
            this.name = name;
            this.ranking = ranking;
        } 
     
        public String toString(){
            return this.name + ":" + this.ranking;
        }
     
        public int compareTo(Object o){
            Student s = (Student)(o);
            return this.ranking - s.ranking;
        }
    }
     
    public class Compare2{
        public static void f(){
            ArrayList arr = new ArrayList();
            arr.add(new Student("Jack",10));
            arr.add(new Student("Bill",23));
            arr.add(new Student("Rudy",7));
     
            System.out.println(arr);
            Collections.sort(arr);
            System.out.println(arr);
        } 
    }

注意重写的compareTo(Object o)方法内.  根据Student的ranking成员来比较的, 也就是说跟姓名无关了.


这时再编译执行, 就能见到List容器内的Student对象已经根据ranking来排序了. 

输出:

    [java] [Jack:10, Bill:23, Rudy:7]
    [java] [Rudy:7, Jack:10, Bill:23]

## 8、java中什么叫引用

首先，你要明白什么是变量。变量的实质是一小块内存单元。这一小块内存里存储着变量的值

比如int a = 1;

a就是变量的名名，1就是变量的值。

而当变量指向一个对象时，这个变量就被称为引用变量

比如A a =new A();

**a就是引用变量，它指向了一个A对象，也可以说它引用了一个A对象。我们通过操纵这个a来操作A对象。 此时，变量a的值为它所引用对象的地址**

1. 引用数据类型为java两大数据类型之一
2. 引用数据型在被床架时，首先要在栈上给其引用（句柄）分配一块内存，而对象的具体信息都存储在堆内存上，然后由栈上面的引用指向堆中对象的地址。
3. 引用数据类型包括：类、接口类型、数组类型、[枚举类型](https://www.baidu.com/s?wd=枚举类型&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y4nAfYPHKBnWbznycLnjRY0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EnW04rjmLnHDv)、注解类型，字符串型；

- java另一大数据类型为基本数据类型，其包括包括数值型，字符型和布尔型。
- 基本数据类型在被创建时，在栈上给其划分一块内存，将数值直接存储在栈上；

就是这个数据的别名，就像一个人的外号一样，你处理这个外号，就是对个人本身的处理相当于C里面的引用，即&，存有某个类的实例地址

## 9、Java中float类型值后为什么要加F

double类型为64位,而float为32位，并且小数的二进制与整数二进制不同，列如值3.4首先会被看作double类型，64位转成32位会有精度损失。因此float类型要在值后加F.

**3.14是double型。因为3.14在计算机中小数的表示基本上无法准确的描述出来，一般是只是一个近似值，所以“3.14f”才能表示成float型，而3.14只能表示成double型。**

![img](https://img.php.cn/upload/article/202007/06/2020070615463466883.jpg)

## 10、Java中构造方法与普通方法的区别

###### 普通方法

定义：**简单的说方法就是完成特定功能的代码块。**

###### 构造方法

定义：**简单的来说是给对象的数据进行初始化的**。

## 11、jar包的一些事儿



## 12、Java Regex（正则表达式）



## 13、Java中的哈希码

在Java中，哈希码代表了**对象的一种特征**，例如我们**判断某两个字符串是否==，如果其哈希码相等，则这两个字符串是相等的**。其次，哈希码**是一种数据结构的算法**。常见的哈希码的算法有：

1：Object类的hashCode.返回对象的内存地址经过处理后的结构，由于每个对象的内存地址都不一样，所以哈希码也不一样。

2：String类的hashCode.根据String类包含的字符串的内容，根据一种特殊算法返回哈希码，只要字符串内容相同，返回的哈希码也相同。
3：Integer类，返回的哈希码就是Integer对象里所包含的那个整数的数值，例如Integer i1=new Integer(100),i1.hashCode的值就是100 。由此可见，2个一样大小的Integer对象，返回的哈希码也一样。

## 14、Java中的implements

 *JAVA中extends 与implements有啥区别？*

1. 在类的声明中，通过关键字**extends来创建一个类的子类**。一个类通过关键字**implements声明自己使用一个或者多个接口。**
    extends 是继承某个类, 继承之后可以使用父类的方法, 也可以重写父类的方法; **implements 是实现多个接口, 接口的方法一般为空的, 必须重写才能使用**。

2. extends是继承父类，只要那个类不是声明为final或者那个类定义为abstract的就能继承，**JAVA中不支持多继承，但支持多重继承，但是可以用接口来实现，这样就要用到implements，继承只能继承一个类，但implements可以实现多个接口，**用逗号分开就行了
    比如

   ```java
    class A extends B implements C,D,E
   ```

*implements 也是实现父类和子类之间继承关系的关键字，如类 A 继承 类 B 写成 class A implements B{}.*

​	implements是一个类实现一个接口用的关键字，他是用来实现接口中定义的抽象方法。比如：people是一个接口，他里面有say这个方法。public interface people(){ public  say();}但是接口没有方法体。只能通过一个具体的类去实现其中的方法体。比如chinese这个类，就实现了people这个接口。 public class chinese implements people{ public say()  {System.out.println("你好！");}}

## 15、Java throws和throw：声明和抛出异常

[Java](http://c.biancheng.net/java/) 中的异常处理除了捕获异常和处理异常之外，还包括声明异常和拋出异常。实现声明和抛出异常的关键字非常相似，它们是 throws 和 throw。可以通过 **throws 关键字在方法上声明**该方法要拋出的异常，然后在方法内部通过 **throw 拋出异常对象**。

##### throws 声明异常

当一个方法产生一个它不处理的异常时，（调用别人的，不知道会有什么问题），那么就需要在该方法的头部声明这个异常，以便将该异常传递到方法的外部进行处理。使用 throws 声明的方法表示此方法不处理异常。throws 具体格式如下：

```java
returnType method_name(paramList) throws Exception 1,Exception2,…{…}
```


其中，returnType 表示返回值类型；method_name 表示方法名；paramList 表示参数列表；Exception 1，Exception2，… 表示异常类。

**如果有多个异常类，它们之间用逗号分隔。**这些异常类可以是方法中调用了可能拋出异常的方法而产生的异常，也可以是方法体中生成并拋出的异常。

使用 throws 声明抛出异常的思路是，当前方法不知道如何处理这种类型的异常，该异常应该由向上一级的调用者处理；如果 main 方法也不知道如何处理这种类型的异常，也可以使用 throws 声明抛出异常，该异常将交给 JVM 处理。JVM 对异常的处理方法是，打印异常的跟踪栈信息，并中止程序运行，这就是前面程序在遇到异常后自动结束的原因。

## 16、Java 抽象类、抽象方法（abstract）

### 抽象方法：

- 在所有的普通方法上面都会有一个“{}”，这个表示方法体，有方法体的方法一定可以被对象直接使用。
- **而抽象方法，是指没有方法体的方法，同时抽象方法还必须使用关键字abstract做修饰。**
- **抽象方法必须为public或者protected**（因为如果为private，则不能被子类继承，子类便无法实现该方法），缺省情况下默认为public。

抽象方法示例：

```csharp
//没有方法体，有abstract关键字做修饰
public abstract void xxx();
```

### 抽象类的基本概念：

- 众所周知，父类是将子类所共同拥有的属性和方法进行抽取，这些属性和方法中，有的是已经明确实现了的，有的还无法确定，那么我们就可以将其定义成抽象，在后日子类进行重用，进行具体化。
- 所以，**抽象类是为了把相同的但不确定的东西的提取出来，为了以后的重用。定义成抽象类的目的，就是为了在子类中实现抽象方法。**
- 简单说，拥有抽象方法的类就是抽象类（但抽象类中也可以不包含抽象方法），**抽象类要使用abstract关键字声明。**

抽象类示例：

```kotlin
//定义一个抽象类
abstract class A{

    //普通方法
    public void fun(){
        System.out.println("存在方法体的方法");
    }

    //抽象方法，没有方法体，有abstract关键字做修饰
    public abstract void print();
}
```

### 抽象类的特性和使用：

- **抽象类不能被实例化。因为抽象类中方法未具体化，这是一种不完整的类，所以直接实例化也就没有意义了。**
- 抽象类的使用必须有子类，使用extends继承，一个子类只能继承一个抽象类。
- **子类（如果不是抽象类）则必须覆写抽象类之中的全部抽象方法（如果子类没有实现父类的抽象方法，则必须将子类也定义为为abstract类。）。**
- 抽象类可以不包含抽象方法，但如果类中包含抽象方法，就必须将该类声明为抽象类。

抽象类的基本使用示例：

```java
//定义一个抽象类
abstract class A{

    //普通方法
    public void fun(){
        System.out.println("存在方法体的方法");
    }

    //抽象方法，没有方法体，有abstract关键字做修饰
    public abstract void print();
}

//单继承
//B类是抽象类的子类，是一个普通类
class B extends A{

    //强制要求覆写
    @Override
    public void print() {
        System.out.println("Hello World !");
    }

}
public class TestDemo {

    public static void main(String[] args) {
        //向上转型
        A a = new B();

        //被子类所覆写的过的方法
        a.print();
    }
}
```

运行结果：

```undefined
Hello World !
```

### 抽象类的使用限制：

- 抽象类可以有构造方法。

> 由于抽象类里会存在一些属性，那么抽象类中一定存在构造方法，其存在目的是为了属性的初始化。
>  并且子类对象实例化的时候，依然满足先执行父类构造，再执行子类构造的顺序。

示例如下：

```csharp
abstract class A{
    public A(){
        System.out.println("*****A类构造方法*****");
    }

    public abstract void print();
}

class B extends A{
    public B(){
        System.out.println("*****B类构造方法*****");
    }

    @Override
    public void print() {
        System.out.println("Hello World !");
    }
}

public class TestDemo {
    public static void main(String[] args) {
        A a = new B();
    }
}
```

执行结果：

```undefined
*****A类构造方法*****
*****B类构造方法*****
```

- **抽象类不能使用final声明，因为抽象类必须有子类，而final定义的类不能有子类。**
- 抽象类能否使用static声明吗？

> **外部抽象类不允许使用static声明，而内部的抽象类可以使用static声明。**
>  使用static声明的内部抽象类相当于一个外部抽象类，继承的时候使用“外部类.内部类”的形式表示类名称。

内部抽象类使用示例：

```java
abstract class A{
    //static定义的内部类属于外部类
    static abstract class B{
        public abstract void print();
    }
}

class C extends A.B{
    public void print(){
        System.out.println("**********");
    }
}

public class TestDemo {
    public static void main(String[] args) {
        //向上转型
        A.B ab = new C();
        ab.print();
    }
}
```

执行结果：

```undefined
**********
```

- **抽象类中的static方法可以直接调用。**

示例代码：

```csharp
abstract class A{
    public static void print(){
        System.out.println("Hello World !");
    }
}

public class TestDemo {
    public static void main(String[] args) {
        A.print();
    }
}
```

执行结果：

```undefined
Hello World !
```

- 有时候由于抽象类中只需要一个特定的系统子类操作，所以可以忽略掉外部子类。这样的设计在系统类库中会比较常见，目的是对用户隐藏不需要知道的子类。

示例如下：

```java
abstract class A{
    public abstract void print();

    //内部抽象类子类
    private static class B extends A{
        //覆写抽象类的方法
        public void print(){
            System.out.println("Hello World !");
        }
    }

    //这个方法不受实例化对象的控制
    public static A getInstance(){
        return new B();
    }
}

public class TestDemo {
    public static void main(String[] args) {
        //此时取得抽象类对象的时候完全不需要知道B类这个子类的存在
        A a = A.getInstance();
        a.print();
    }
}
```

执行结果：

```undefined
Hello World !
```

## 17. 打破砂锅问到底（泛型）

> 泛型存在的意义？
>  泛型类，泛型接口，泛型方法如何定义？
>  如何限定类型变量？
>  泛型中使用的约束和局限性有哪些？
>  泛型类型的继承规则是什么？
>  泛型中的通配符类型是什么？
>  如何获取泛型的参数类型？
>  虚拟机是如何实现泛型的？
>  在日常开发中是如何运用泛型的？

![image-20211016215620517](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20211016215620517.png)

Java泛型详解.png

### 晓之以理动之以码

### 泛型的定义以及存在意义

泛型，即“参数化类型”。就是将类型由原来的具体的类型参数化，类似于方法中的变量参数，此时类型也定义成参数形式（可以称之为类型形参），然后在使用/调用时传入具体的类型（类型实参）。
 例如：GenericClass**<T>**{}

> 一些常用的泛型类型变量：
>  E：元素（Element），多用于java集合框架
>  K：关键字（Key）
>  N：数字（Number）
>  T：类型（Type）
>  V：值（Value）

如果要实现不同类型的加法，每种类型都需要重载一个add方法



```csharp
package com.jay.java.泛型.needGeneric;

/**
 * Author：Jay On 2019/5/9 16:06
 * <p>
 * Description: 为什么使用泛型
 */
public class NeedGeneric1 {

    private static int add(int a, int b) {
        System.out.println(a + "+" + b + "=" + (a + b));
        return a + b;
    }

    private static float add(float a, float b) {
        System.out.println(a + "+" + b + "=" + (a + b));
        return a + b;
    }

    private static double add(double a, double b) {
        System.out.println(a + "+" + b + "=" + (a + b));
        return a + b;
    }

    private static <T extends Number> double add(T a, T b) {
        System.out.println(a + "+" + b + "=" + (a.doubleValue() + b.doubleValue()));
        return a.doubleValue() + b.doubleValue();
    }

    public static void main(String[] args) {
        NeedGeneric1.add(1, 2);
        NeedGeneric1.add(1f, 2f);
        NeedGeneric1.add(1d, 2d);
        NeedGeneric1.add(Integer.valueOf(1), Integer.valueOf(2));
        NeedGeneric1.add(Float.valueOf(1), Float.valueOf(2));
        NeedGeneric1.add(Double.valueOf(1), Double.valueOf(2));
    }
}

```

取出集合元素时需要人为的强制类型转化到具体的目标类型，且很容易现“java.lang. ClassCast Exception”异常。



```cpp
package com.jay.java.泛型.needGeneric;

import java.util.ArrayList;
import java.util.List;

/**
 * Author：Jay On 2019/5/9 16:23
 * <p>
 * Description: 为什么要使用泛型
 */
public class NeedGeneric2 {
    static class C{

    }
    public static void main(String[] args) {
        List list=new ArrayList();
        list.add("A");
        list.add("B");
        list.add(new C());
        list.add(100);
        //1.当我们将一个对象放入集合中，集合不会记住此对象的类型，当再次从集合中取出此对象时，改对象的编译类型变成了Object类型，但其运行时类型任然为其本身类型。
        //2.因此，//1处取出集合元素时需要人为的强制类型转化到具体的目标类型，且很容易出现“java.lang.ClassCastException”异常。
        for (int i = 0; i < list.size(); i++) {
//            System.out.println(list.get(i));
            String value= (String) list.get(i);
            System.out.println(value);
        }
    }
}
```

所以使用泛型的意义在于
 **1,适用于多种数据类型执行相同的代码（代码复用）
 2, 泛型中的类型在使用时指定，不需要强制类型转换（类型安全，编译器会检查类型）**

### 泛型类的使用

定义一个泛型类：public class `GenericClass<T>`{}



```cpp
package com.jay.java.泛型.DefineGeneric;

/**
 * Author：Jay On 2019/5/9 16:49
 * <p>
 * Description: 泛型类
 */
public class GenericClass<T> {
    private T data;

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }

    public static void main(String[] args) {
        GenericClass<String> genericClass=new GenericClass<>();
        genericClass.setData("Generic Class");
        System.out.println(genericClass.getData());
    }
}
```

### 泛型接口的使用

定义一个泛型接口：public interface `GenericIntercace<T>`{}



```dart
/**
 * Author：Jay On 2019/5/9 16:57
 * <p>
 * Description: 泛型接口
 */
public interface GenericIntercace<T> {
     T getData();
}
```

实现泛型接口方式一：public class `ImplGenericInterface1<T>` implements `GenericIntercace<T>`



```cpp
/**
 * Author：Jay On 2019/5/9 16:59
 * <p>
 * Description: 泛型接口实现类-泛型类实现方式
 */
public class ImplGenericInterface1<T> implements GenericIntercace<T> {
    private T data;

    private void setData(T data) {
        this.data = data;
    }

    @Override
    public T getData() {
        return data;
    }

    public static void main(String[] args) {
        ImplGenericInterface1<String> implGenericInterface1 = new ImplGenericInterface1<>();
        implGenericInterface1.setData("Generic Interface1");
        System.out.println(implGenericInterface1.getData());
    }
}
```

实现泛型接口方式二：public class ImplGenericInterface2 implements `GenericIntercace<String>` {}



```dart
/**
 * Author：Jay On 2019/5/9 17:01
 * <p>
 * Description: 泛型接口实现类-指定具体类型实现方式
 */
public class ImplGenericInterface2 implements GenericIntercace<String> {
    @Override
    public String getData() {
        return "Generic Interface2";
    }

    public static void main(String[] args) {
        ImplGenericInterface2 implGenericInterface2 = new ImplGenericInterface2();
        System.out.println(implGenericInterface2.getData());
    }
}
```

### 泛型方法的使用

定义一个泛型方法： private static`<T> T`genericAdd(T a, T b) {}



```csharp
/**
 * Author：Jay On 2019/5/10 10:46
 * <p>
 * Description: 泛型方法
 */
public class GenericMethod1 {
    private static int add(int a, int b) {
        System.out.println(a + "+" + b + "=" + (a + b));
        return a + b;
    }

    private static <T> T genericAdd(T a, T b) {
        System.out.println(a + "+" + b + "="+a+b);
        return a;
    }

    public static void main(String[] args) {
        GenericMethod1.add(1, 2);
        GenericMethod1.<String>genericAdd("a", "b");
    }
}
```



```java
/**
 * Author：Jay On 2019/5/10 16:22
 * <p>
 * Description: 泛型方法
 */
public class GenericMethod3 {

    static class Animal {
        @Override
        public String toString() {
            return "Animal";
        }
    }

    static class Dog extends Animal {
        @Override
        public String toString() {
            return "Dog";
        }
    }

    static class Fruit {
        @Override
        public String toString() {
            return "Fruit";
        }
    }

    static class GenericClass<T> {

        public void show01(T t) {
            System.out.println(t.toString());
        }

        public <T> void show02(T t) {
            System.out.println(t.toString());
        }

        public <K> void show03(K k) {
            System.out.println(k.toString());
        }
    }

    public static void main(String[] args) {
        Animal animal = new Animal();
        Dog dog = new Dog();
        Fruit fruit = new Fruit();
        GenericClass<Animal> genericClass = new GenericClass<>();
        //泛型类在初始化时限制了参数类型
        genericClass.show01(dog);
//        genericClass.show01(fruit);

        //泛型方法的参数类型在使用时指定
        genericClass.show02(dog);
        genericClass.show02(fruit);

        genericClass.<Animal>show03(animal);
        genericClass.<Animal>show03(dog);
        genericClass.show03(fruit);
//        genericClass.<Dog>show03(animal);
    }
}
```

### 限定泛型类型变量

1,对类的限定：public class `TypeLimitForClass<T extends List & Serializable>{}`
 2,对方法的限定：public static`<T extends Comparable<T>>`T getMin(T a, T b) {}



```dart
/**
 * Author：Jay On 2019/5/10 16:38
 * <p>
 * Description: 类型变量的限定-方法
 */
public class TypeLimitForMethod {

    /**
     * 计算最小值
     * 如果要实现这样的功能就需要对泛型方法的类型做出限定
     */
//    private static <T> T getMin(T a, T b) {
//        return (a.compareTo(b) > 0) ? a : b;
//    }

    /**
     * 限定类型使用extends关键字指定
     * 可以使类，接口，类放在前面接口放在后面用&符号分割
     * 例如：<T extends ArrayList & Comparable<T> & Serializable>
     */
    public static <T extends Comparable<T>> T getMin(T a, T b) {
        return (a.compareTo(b) < 0) ? a : b;
    }

    public static void main(String[] args) {
        System.out.println(TypeLimitForMethod.getMin(2, 4));
        System.out.println(TypeLimitForMethod.getMin("a", "r"));
    }
}
```



```java
/**
 * Author：Jay On 2019/5/10 17:02
 * <p>
 * Description: 类型变量的限定-类
 */
public class TypeLimitForClass<T extends List & Serializable> {
    private T data;

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }

    public static void main(String[] args) {
        ArrayList<String> stringArrayList = new ArrayList<>();
        stringArrayList.add("A");
        stringArrayList.add("B");
        ArrayList<Integer> integerArrayList = new ArrayList<>();
        integerArrayList.add(1);
        integerArrayList.add(2);
        integerArrayList.add(3);
        TypeLimitForClass<ArrayList> typeLimitForClass01 = new TypeLimitForClass<>();
        typeLimitForClass01.setData(stringArrayList);
        TypeLimitForClass<ArrayList> typeLimitForClass02 = new TypeLimitForClass<>();
        typeLimitForClass02.setData(integerArrayList);

        System.out.println(getMinListSize(typeLimitForClass01.getData().size(), typeLimitForClass02.getData().size()));

    }

    public static <T extends Comparable<T>> T getMinListSize(T a, T b) {
        return (a.compareTo(b) < 0) ? a : b;
    }
```

### 泛型中的约束和局限性

1,不能实例化泛型类
 2,静态变量或方法不能引用泛型类型变量，但是静态泛型方法是可以的
 3,基本类型无法作为泛型类型
 4,无法使用instanceof关键字或==判断泛型类的类型
 5,泛型类的原生类型与所传递的泛型无关，无论传递什么类型，原生类是一样的
 6,泛型数组可以声明但无法实例化
 7,泛型类不能继承Exception或者Throwable
 8,不能捕获泛型类型限定的异常但可以将泛型限定的异常抛出



```Java
/**
 * Author：Jay On 2019/5/10 17:41
 * <p>
 * Description: 泛型的约束和局限性
 */
public class GenericRestrict1<T> {
    static class NormalClass {

    }

    private T data;

    /**
     * 不能实例化泛型类
     * Type parameter 'T' cannot be instantiated directly
     */
    public void setData() {
        //this.data = new T();
    }

    /**
     * 静态变量或方法不能引用泛型类型变量
     * 'com.jay.java.泛型.restrict.GenericRestrict1.this' cannot be referenced from a static context
     */
//    private static T result;

//    private static T getResult() {
//        return result;
//    }

    /**
     * 静态泛型方法是可以的
     */
    private static <K> K getKey(K k) {
        return k;
    }

    public static void main(String[] args) {
        NormalClass normalClassA = new NormalClass();
        NormalClass normalClassB = new NormalClass();
        /**
         * 基本类型无法作为泛型类型
         */
//        GenericRestrict1<int> genericRestrictInt = new GenericRestrict1<>();
        GenericRestrict1<Integer> genericRestrictInteger = new GenericRestrict1<>();
        GenericRestrict1<String> genericRestrictString = new GenericRestrict1<>();
        /**
         * 无法使用instanceof关键字判断泛型类的类型
         * Illegal generic type for instanceof
         */
//        if(genericRestrictInteger instanceof GenericRestrict1<Integer>){
//            return;
//        }

        /**
         * 无法使用“==”判断两个泛型类的实例
         * Operator '==' cannot be applied to this two instance
         */
//        if (genericRestrictInteger == genericRestrictString) {
//            return;
//        }

        /**
         * 泛型类的原生类型与所传递的泛型无关，无论传递什么类型，原生类是一样的
         */
        System.out.println(normalClassA == normalClassB);//false
        System.out.println(genericRestrictInteger == genericRestrictInteger);//
        System.out.println(genericRestrictInteger.getClass() == genericRestrictString.getClass()); //true
        System.out.println(genericRestrictInteger.getClass());//com.jay.java.泛型.restrict.GenericRestrict1
        System.out.println(genericRestrictString.getClass());//com.jay.java.泛型.restrict.GenericRestrict1

        /**
         * 泛型数组可以声明但无法实例化
         * Generic array creation
         */
        GenericRestrict1<String>[] genericRestrict1s;
//        genericRestrict1s = new GenericRestrict1<String>[10];
        genericRestrict1s = new GenericRestrict1[10];
        genericRestrict1s[0]=genericRestrictString;
    }

}
```



```Java
/**
 * Author：Jay On 2019/5/10 18:45
 * <p>
 * Description: 泛型和异常
 */
public class GenericRestrict2 {

    private class MyException extends Exception {
    }

    /**
     * 泛型类不能继承Exception或者Throwable
     * Generic class may not extend 'java.lang.Throwable'
     */
//    private class MyGenericException<T> extends Exception {
//    }
//
//    private class MyGenericThrowable<T> extends Throwable {
//    }

    /**
     * 不能捕获泛型类型限定的异常
     * Cannot catch type parameters
     */
    public <T extends Exception> void getException(T t) {
//        try {
//
//        } catch (T e) {
//
//        }
    }

    /**
     *可以将泛型限定的异常抛出
     */
    public <T extends Throwable> void getException(T t) throws T {
        try {

        } catch (Exception e) {
            throw t;
        }
    }
}
```

### 泛型类型继承规则

1,对于泛型参数是继承关系的泛型类之间是没有继承关系的
 2,泛型类可以继承其它泛型类，例如: public class ArrayList<E> extends AbstractList<E>
 3,泛型类的继承关系在使用中同样会受到泛型类型的影响



```java
/**
 * Author：Jay On 2019/5/10 19:13
 * <p>
 * Description: 泛型继承规则测试类
 */
public class GenericInherit<T> {
    private T data1;
    private T data2;

    public T getData1() {
        return data1;
    }

    public void setData1(T data1) {
        this.data1 = data1;
    }

    public T getData2() {
        return data2;
    }

    public void setData2(T data2) {
        this.data2 = data2;
    }

    public static <V> void setData2(GenericInherit<Father> data2) {

    }

    public static void main(String[] args) {
//        Son 继承自 Father
        Father father = new Father();
        Son son = new Son();
        GenericInherit<Father> fatherGenericInherit = new GenericInherit<>();
        GenericInherit<Son> sonGenericInherit = new GenericInherit<>();
        SubGenericInherit<Father> fatherSubGenericInherit = new SubGenericInherit<>();
        SubGenericInherit<Son> sonSubGenericInherit = new SubGenericInherit<>();

        /**
         * 对于传递的泛型类型是继承关系的泛型类之间是没有继承关系的
         * GenericInherit<Father> 与GenericInherit<Son> 没有继承关系
         * Incompatible types.
         */
        father = new Son();
//        fatherGenericInherit=new GenericInherit<Son>();

        /**
         * 泛型类可以继承其它泛型类，例如: public class ArrayList<E> extends AbstractList<E>
         */
        fatherGenericInherit=new SubGenericInherit<Father>();

        /**
         *泛型类的继承关系在使用中同样会受到泛型类型的影响
         */
        setData2(fatherGenericInherit);
//        setData2(sonGenericInherit);
        setData2(fatherSubGenericInherit);
//        setData2(sonSubGenericInherit);

    }

    private static class SubGenericInherit<T> extends GenericInherit<T> {

    }
```

### 通配符类型

1,`<? extends Parent>` 指定了泛型类型的上届
 2,`<? super Child>` 指定了泛型类型的下届
 3, `<?>` 指定了没有限制的泛型类型

![img](https:////upload-images.jianshu.io/upload_images/2516326-c36715daf91572cf.png?imageMogr2/auto-orient/strip|imageView2/2/w/487/format/webp)

通配符测试类结构.png



```csharp
/**
 * Author：Jay On 2019/5/10 19:51
 * <p>
 * Description: 泛型通配符测试类
 */
public class GenericByWildcard {
    private static void print(GenericClass<Fruit> fruitGenericClass) {
        System.out.println(fruitGenericClass.getData().getColor());
    }

    private static void use() {
        GenericClass<Fruit> fruitGenericClass = new GenericClass<>();
        print(fruitGenericClass);
        GenericClass<Orange> orangeGenericClass = new GenericClass<>();
        //类型不匹配,可以使用<? extends Parent> 来解决
//        print(orangeGenericClass);
    }

    /**
     * <? extends Parent> 指定了泛型类型的上届
     */
    private static void printExtends(GenericClass<? extends Fruit> genericClass) {
        System.out.println(genericClass.getData().getColor());
    }

    public static void useExtend() {
        GenericClass<Fruit> fruitGenericClass = new GenericClass<>();
        printExtends(fruitGenericClass);
        GenericClass<Orange> orangeGenericClass = new GenericClass<>();
        printExtends(orangeGenericClass);

        GenericClass<Food> foodGenericClass = new GenericClass<>();
        //Food是Fruit的父类，超过了泛型上届范围，类型不匹配
//        printExtends(foodGenericClass);

        //表示GenericClass的类型参数的上届是Fruit
        GenericClass<? extends Fruit> extendFruitGenericClass = new GenericClass<>();
        Apple apple = new Apple();
        Fruit fruit = new Fruit();
        /*
         * 道理很简单，？ extends X  表示类型的上界，类型参数是X的子类，那么可以肯定的说，
         * get方法返回的一定是个X（不管是X或者X的子类）编译器是可以确定知道的。
         * 但是set方法只知道传入的是个X，至于具体是X的那个子类，不知道。
         * 总结：主要用于安全地访问数据，可以访问X及其子类型，并且不能写入非null的数据。
         */
//        extendFruitGenericClass.setData(apple);
//        extendFruitGenericClass.setData(fruit);

        fruit = extendFruitGenericClass.getData();

    }

    /**
     * <? super Child> 指定了泛型类型的下届
     */
    public static void printSuper(GenericClass<? super Apple> genericClass) {
        System.out.println(genericClass.getData());
    }

    public static void useSuper() {
        GenericClass<Food> foodGenericClass = new GenericClass<>();
        printSuper(foodGenericClass);

        GenericClass<Fruit> fruitGenericClass = new GenericClass<>();
        printSuper(fruitGenericClass);

        GenericClass<Apple> appleGenericClass = new GenericClass<>();
        printSuper(appleGenericClass);

        GenericClass<HongFuShiApple> hongFuShiAppleGenericClass = new GenericClass<>();
        // HongFuShiApple 是Apple的子类，达不到泛型下届，类型不匹配
//        printSuper(hongFuShiAppleGenericClass);

        GenericClass<Orange> orangeGenericClass = new GenericClass<>();
        // Orange和Apple是兄弟关系，没有继承关系，类型不匹配
//        printSuper(orangeGenericClass);

        //表示GenericClass的类型参数的下界是Apple
        GenericClass<? super Apple> supperAppleGenericClass = new GenericClass<>();
        supperAppleGenericClass.setData(new Apple());
        supperAppleGenericClass.setData(new HongFuShiApple());
        /*
         * ？ super  X  表示类型的下界，类型参数是X的超类（包括X本身），
         * 那么可以肯定的说，get方法返回的一定是个X的超类，那么到底是哪个超类？不知道，
         * 但是可以肯定的说，Object一定是它的超类，所以get方法返回Object。
         * 编译器是可以确定知道的。对于set方法来说，编译器不知道它需要的确切类型，但是X和X的子类可以安全的转型为X。
         * 总结：主要用于安全地写入数据，可以写入X及其子类型。
         */
//        supperAppleGenericClass.setData(new Fruit());

        //get方法只会返回一个Object类型的值。
        Object data = supperAppleGenericClass.getData();
    }

    /**
     * <?> 指定了没有限定的通配符
     */
    public static void printNonLimit(GenericClass<?> genericClass) {
        System.out.println(genericClass.getData());
    }

    public static void useNonLimit() {
        GenericClass<Food> foodGenericClass = new GenericClass<>();
        printNonLimit(foodGenericClass);
        GenericClass<Fruit> fruitGenericClass = new GenericClass<>();
        printNonLimit(fruitGenericClass);
        GenericClass<Apple> appleGenericClass = new GenericClass<>();
        printNonLimit(appleGenericClass);

        GenericClass<?> genericClass = new GenericClass<>();
        //setData 方法不能被调用， 甚至不能用 Object 调用；
//        genericClass.setData(foodGenericClass);
//        genericClass.setData(new Object());
        //返回值只能赋给 Object
        Object object = genericClass.getData();

    }

}
```

### 获取泛型的参数类型

[Type是什么](https://www.jianshu.com/p/c820e55d9f27)
 这里的Type指java.lang.reflect.Type, 是Java中所有类型的公共高级接口, 代表了Java中的所有类型. Type体系中类型的包括：数组类型(GenericArrayType)、参数化类型(ParameterizedType)、类型变量(TypeVariable)、通配符类型(WildcardType)、原始类型(Class)、基本类型(Class), 以上这些类型都实现Type接口.

> 参数化类型,就是我们平常所用到的泛型List、Map；
>  数组类型,并不是我们工作中所使用的数组String[] 、byte[]，而是带有泛型的数组，即T[] ；
>  通配符类型, 指的是<?>, <? extends T>等等
>  原始类型, 不仅仅包含我们平常所指的类，还包括枚举、数组、注解等；
>  基本类型, 也就是我们所说的java的基本类型，即int,float,double等



```dart
public interface ParameterizedType extends Type {
    // 返回确切的泛型参数, 如Map<String, Integer>返回[String, Integer]
    Type[] getActualTypeArguments();
    
    //返回当前class或interface声明的类型, 如List<?>返回List
    Type getRawType();
    
    //返回所属类型. 如,当前类型为O<T>.I<S>, 则返回O<T>. 顶级类型将返回null 
    Type getOwnerType();
}
```



```cpp
/**
 * Author：Jay On 2019/5/11 22:41
 * <p>
 * Description: 获取泛型类型测试类
 */
public class GenericType<T> {
    private T data;

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }

    public static void main(String[] args) {
        GenericType<String> genericType = new GenericType<String>() {};
        Type superclass = genericType.getClass().getGenericSuperclass();
        //getActualTypeArguments 返回确切的泛型参数, 如Map<String, Integer>返回[String, Integer]
        Type type = ((ParameterizedType) superclass).getActualTypeArguments()[0]; 
        System.out.println(type);//class java.lang.String
    }
}
```

### 虚拟机是如何实现泛型的

Java泛型是Java1.5之后才引入的，为了向下兼容。Java采用了C++完全不同的实现思想。Java中的泛型更多的看起来像是编译期用的
 Java中泛型在运行期是不可见的，会被擦除为它的上级类型。如果是没有限定的泛型参数类型，就会被替换为Object.



```xml
GenericClass<String> stringGenericClass=new GenericClass<>();
GenericClass<Integer> integerGenericClass=new GenericClass<>();
```

C++中GenericClass<String>和GenericClass<Integer>是两个不同的类型
 Java进行了类型擦除之后统一改为GenericClass<Object>



```cpp
/**
 * Author：Jay On 2019/5/11 16:11
 * <p>
 * Description:泛型原理测试类
 */
public class GenericTheory {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();
        map.put("Key", "Value");
        System.out.println(map.get("Key"));
        GenericClass<String, String> genericClass = new GenericClass<>();
        genericClass.put("Key", "Value");
        System.out.println(genericClass.get("Key"));
    }

    public static class GenericClass<K, V> {
        private K key;
        private V value;

        public void put(K key, V value) {
            this.key = key;
            this.value = value;
        }

        public V get(V key) {
            return value;
        }
    }

    /**
     * 类型擦除后GenericClass2<Object>
     * @param <T>
     */
    private class GenericClass2<T> {

    }

    /**
     * 类型擦除后GenericClass3<ArrayList>
     * 当使用到Serializable时会将相应代码强制转换为Serializable
     * @param <T>
     */
    private class GenericClass3<T extends ArrayList & Serializable> {

    }
}
```

对应的字节码文件



```dart
 public static void main(String[] args) {
        Map<String, String> map = new HashMap();
        map.put("Key", "Value");
        System.out.println((String)map.get("Key"));
        GenericTheory.GenericClass<String, String> genericClass = new GenericTheory.GenericClass();
        genericClass.put("Key", "Value");
        System.out.println((String)genericClass.get("Key"));
    }
```

### 学以致用

##### 泛型解析JSON数据封装

api返回的json数据



```json
{
    "code":200,
    "msg":"成功",
    "data":{
        "name":"Jay",
        "email":"10086"
    }
}
BaseResponse .java
```



```cpp
/**
 * Author：Jay On 2019/5/11 20:48
 * <p>
 * Description: 接口数据接收基类
 */
public class BaseResponse {

    private int code;
    private String msg;

    public int getCode() {
        return code;
    }

    public void setCode(int code) {
        this.code = code;
    }

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }
}
UserResponse.java
```



```kotlin
/**
 * Author：Jay On 2019/5/11 20:49
 * <p>
 * Description: 用户信息接口实体类
 */
public class UserResponse<T> extends BaseResponse {
    private T data;

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }
}
```

##### 泛型+反射实现巧复用工具类



```java
/**
 * Author：Jay On 2019/5/11 21:05
 * <p>
 * Description: 泛型相关的工具类
 */
public class GenericUtils {

    public static class Movie {
        private String name;
        private Date time;

        public String getName() {
            return name;
        }

        public Date getTime() {
            return time;
        }

        public Movie(String name, Date time) {
            this.name = name;
            this.time = time;
        }

        @Override
        public String toString() {
            return "Movie{" + "name='" + name + '\'' + ", time=" + time + '}';
        }
    }

    public static void main(String[] args) {
        List<Movie> movieList = new ArrayList<>();
        for (int i = 0; i < 5; i++) {
            movieList.add(new Movie("movie" + i, new Date()));
        }
        System.out.println("排序前:" + movieList.toString());

        GenericUtils.sortAnyList(movieList, "name", true);
        System.out.println("按name正序排：" + movieList.toString());

        GenericUtils.sortAnyList(movieList, "name", false);
        System.out.println("按name逆序排：" + movieList.toString());
    }

    /**
     * 对任意集合的排序方法
     * @param targetList 要排序的实体类List集合
     * @param sortField  排序字段
     * @param sortMode   true正序，false逆序
     */
    public static <T> void sortAnyList(List<T> targetList, final String sortField, final boolean sortMode) {
        if (targetList == null || targetList.size() < 2 || sortField == null || sortField.length() == 0) {
            return;
        }
        Collections.sort(targetList, new Comparator<Object>() {
            @Override
            public int compare(Object obj1, Object obj2) {
                int retVal = 0;
                try {
                    // 获取getXxx()方法名称
                    String methodStr = "get" + sortField.substring(0, 1).toUpperCase() + sortField.substring(1);
                    Method method1 = ((T) obj1).getClass().getMethod(methodStr, null);
                    Method method2 = ((T) obj2).getClass().getMethod(methodStr, null);
                    if (sortMode) {
                        retVal = method1.invoke(((T) obj1), null).toString().compareTo(method2.invoke(((T) obj2), null).toString());
                    } else {
                        retVal = method2.invoke(((T) obj2), null).toString().compareTo(method1.invoke(((T) obj1), null).toString());
                    }
                } catch (Exception e) {
                    System.out.println("List<" + ((T) obj1).getClass().getName() + ">排序异常！");
                    e.printStackTrace();
                }
                return retVal;
            }
        });
    }
}
```

##### Gson库中的泛型的使用-TypeToken



```csharp
/**
 * Author：Jay On 2019/5/11 22:11
 * <p>
 * Description: Gson库中的泛型使用
 */
public class GsonGeneric {
    public static class Person {
        private String name;
        private int age;

        public Person(String name, int age) {
            this.name = name;
            this.age = age;
        }

        @Override
        public String toString() {
            return "Person{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    '}';
        }
    }

    public static void main(String[] args) {
        Gson gson = new Gson();
        List<Person> personList = new ArrayList<>();
        for (int i = 0; i < 5; i++) {
            personList.add(new Person("name" + i, 18 + i));
        }
        // Serialization
        String json = gson.toJson(personList);
        System.out.println(json);
        // Deserialization
        Type personType = new TypeToken<List<Person>>() {}.getType();
        List<Person> personList2 = gson.fromJson(json, personType);
        System.out.println(personList2);
    }
}
```
