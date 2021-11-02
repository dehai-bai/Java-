# Java语言概述
## 1.1 Java的起源与发展
### 1.1.1 Java的起源
> 大概知道这几个点就可以了
- Java之父：James Gosling
- 公司：美国Sun Microsystems
- Java语言于1995年5月23日正式发布
### 1.1.2 Java发展历程
各个版本的发布时间和工程，这个自己到网上或书籍查找
## 1.2 Java平台与开发环境
### 1.2.1Java平台与应用领域
#### Java 标准版（Java Standard Edition，Java SE）：客户端
#### Java 企业版（Java Enterprise Edition，Java EE）：服务器端
#### Java 微型版（Java Micro Edition，Java ME）：移动设备（手机等）
### 1.2.2 JDK,JRE,JVM
java源程序必须经过编译才能运行。

什么是**编译器**：就是将程序源代码转换成可执行格式（如字节码，本机代码等）的程序。

那么，Java的编译器是一个叫**javac**的程序

除了上述这些，还差一步，因为javac只是将Java源代码编译成字节码，要运行字节码，还需要一个**Java虚拟机（Java Virtual Machine，JVM）**。此外，当写代码时还需要用到很多Java核心类库中的类，所以，也需要下载这些类库。所以**JVM和Java类库构成了Java的运行环境JRE(Java runtime environment)**。

JDK（Java Development Toolkit）：称为Java开发工具包，他是编译和运行Java程序的必备软件

总结：
- JVM就是一种运行字节码的应用程序
- JRE就是一种包含JVM和Java类库的环境
- JDK就是包含JRE和一个Java编译器和其他程序的工具集
> 注意：操作系统不同，他们的JRE也不同。

### 1.2.3 JDK的下载安装
### 1.2.4 Java API文档
Application Program Interface：Java应用编程接口，也叫库。
自己没事一定要多翻一翻API文档。

## 1.3 Java程序基本结构
### 1.3.1 Java程序开发步骤
1.编辑源程序（写代码）
2.编译源程序
3.执行或调试程序
> 其实，难的在于调试程序，等以后进入公司便会深有体会