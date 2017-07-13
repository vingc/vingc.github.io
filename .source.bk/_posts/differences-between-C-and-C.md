---
title: Differences between C and C++
date: 2017-07-11 10:02:05
tags: technology C C++
---

***



C和C++最大的区别显然是C++增加了OOP和泛型的特性，这一部分知识是相对完整和独立的，不在本文里涉及。本文的目的是记录C和C++在语法上的细微差异，作为以后查阅和复习的资料。

***



1. 源文件命名的差异，C的源文件是“.c”结尾，头文件是“.h”结尾；C++的源文件是“.cpp"、”.cc“、”.cxx“等，而头文件没有扩展名，但支持C式头文件和转换后的C头文件，如”math.h“和”cmath“。

2. 编译器的差异，C使用gcc编译，C++使用g++编译，两个命令的编译选项大部分相同，编译过程相同。

3. 注释的差异，C99之后的版本没有差异，因为添加了对C++注释符号”//“的支持

4. main函数的差异，如果main要求返回int型时，C++可以在最后一行省略”return“语句，编译器默认为”return 0;“；C不允许省略。

5. 命名空间，C++增加了命名空间的特性，”using namespace std;“ 或”std::cout“或”using std::cout;“；”using“语句放到源文件的头部，函数定义之前，对可以本文件的所有函数生效，如果放在函数定义的头部，只会对本函数生效。

6. 输入和输出，C++使用”cout“和”cin“对象完成输出和输入操作。如”cout<<"Hello World"<\<endl;“和”cin>>var;“；“<<”插入运算符，“>>”提取运算符。

7. 命名规则，没有差异，以单下划线或双下划线开头的名字预留给编译器使用。

8. sizeof语言内置运算符，没有差异，参数可以为变量名或者类型名；参数为类型名时必须使用括号，如“sizeof(int)”，“int a, sizeof a;”.

9. 变量初始化，C++新增了大括号“{}”初始化方式（列表初始化，不允许缩窄转换，即不能赋值超出类型表示范围），如“int a{10};”、“int a={10};”、“int a{};”；如果大括号没有内容，默认初始化为0，变量和大括号之间的等号是可选的，也可用于字符串常量初始化字符数组、string对象、结构变量，如char date[] = { "Le Chapon Dodu" }；
   char date[] {"The E legant P la te "} ;
   string date = { "The Bread Bow l"};
   string date {"H ank's Fine E a ts "}; 。

10. 基本类型，C++新增了“char16\_t”和“char32\_t”；C++提供了bool类型，C在C99标准里才新增bool类型，且需要使用头文件"stdbool.h"。

11. 强制类型转换，C只支持一种格式“(TypeName)value”，C++除了支持C的这种方式之后，还支持其他转换方式，如“TypeName(value)”、“static_cast\<Type>(value)”。

12. 拼接字符串常量，C++支持该特性，如“cout<<"This is a test " "and this is another test.";”，“cout<<"This is a test and this is another test."”；前面两次输出内容是相等的，C++自动把空白分割的多个字符串常量拼接为一个，空白可以是空格、制表符、换行符；第二个字符串的首字符替代前一个字符串的空字符“\0”。

13. 字符串的表示差异，C支持字符指针char*或者字符数组char array[]，C++除了支持C式的字符串之外还支持string字符串对象。

14. 结构声明变量的差异，C使用已经定义的结构声明变量时需要带上struct关键字，如“struct inflatable balloon;”，而C++可以省略struct关键字，如“inflatable ballon;”，此处的struct关键字在C++中是可选的。假设结构inflatable定义:

    struct inflatable 

    {

    ​    int weight;

    };

15. 内存分配，C使用malloc()函数，C++另外支持了new关键字，new可以为数据对象分配内存，如"Typename * pointer = new Typename;"、“int * pInt = new int;”；Typename可以使基本类型也可以是结构类型。

16. 内存释放，C使用free()函数释放malloc()函数分配的内存，C++对于new分配的内存，需要使用delete释放，如“delete pointer;”，“delete pInt;”。

17. 动态数组，C++支持动态数组，即运行时确定数组长度和创建数组，如“Typename * pointer = new Typename[nums];”，“int * pIntArray = new int[10];”；释放使用“delete [] pointer;”语法。

18. 字符串首元素地址，在cout和C++大多数表达式中，char数组名、char指针以及双引号包围的字符串常量都被解释为字符串第一个字符的地址。

19. For-each语法，C++支持for-each的用法，如“for ( int x: {1,2,3,4} )”，“int x[10]; for ( int x: x )”；这种用法还可以用于容器。

20. （未完待续）

    ​