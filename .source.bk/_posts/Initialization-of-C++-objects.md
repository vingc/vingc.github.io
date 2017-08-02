---
title: Initialization of C++ objects
date: 2017-08-02 12:54:05
tags: technology C++
---

***

#### 类构造函数的形态

以类Stock为例，构造函数原型有以下几种。

1.  implicit default constructor，如果类声明没有提供构造函数，编译器生成一个默认的隐式构造函数，原型如下

   Stock(){}; //do noting

2. explicit default constructor without parameters，程序员可以在类声明中显示定义无参数的默认构造函数，原型如下

   Stock(){ /\*do whatever you need*/ };

3. explicit default constructor with parameters all have default values，程序员可以在类声明中显示定义有参数的默认构造函数，但所有的参数必须提供默认值，原型如下

   Stock( const char * name = "null", int val = 10 );

4. explicit constructor with parameters，程序员可以在类声明中显示定义有参数的重载构造函数，原型如下

   Stock( const char * name, int val = 10 ); //参数的默认值都是可选的，但需要遵守默认值的赋值规则



#### 类对象的初始化

类对象的初始化方式跟构造函数的原型相关，因为在创建对象时，程序必然会调用构造函数用于创建对象，根据构造函数原型的不同，初始化方式有一下几种。

1. Stock stGoogle; // use default constructor implicitly
2. Stock stGoogle = Stock(); // use default constructor explicitly
3. Stock * stGoogle = new Stock(); // use default constructor implicitly
4. Stock stGoogle = Stock( "google", 10 ); // use explicit constructor
5. Stock stGoogle( "google", 10 );  // use explicit constructor
6. Stock * stGoogle = new Stock( "google", 10 ); //use explicit constructor

以下是C++11支持的列表初始化方式

1. Stock stGoogle = Stock{ "google", 10 }; // use explicit constructor  C++11
2. Stock stGoogle{ "google", 10 };  // use explicit constructor  C++11
3. Stock * stGoogle = new Stock{ "google", 10 }; //use explicit constructor   C++11
4. Stock stGoogle{}; // use default constructor explicitly C++11



#### 类对象数组的初始化

C++设计类特性的时候，尽力满足使用对象类型像使用基本类型一样方便的初衷，因此可以在C++的类管理里，看到对象初始化，对象指针等特点都像基本类型一样维护。而类对象数组也是同样的语法，使用默认构造函数的初始化如下 

Stock array[10];

也可以显示的使用带参数的构造函数初始化数组，如

Stock array[10] = { Stock( "google",1 ), Stock( "yahoo", 2 ), Stock( "baidu", 3 ) }; //大括号围起来的逗号分隔的值列表

该次使用显示构造函数初始化数组的前三个成员，剩余的成员仍然使用默认构造函数。编译器处理这种对象数组初始化方式的流程是，首先使用默认构造函数创建数组元素，然后花括号中的构造函数将创建临时对象，然后将临时对象的内容复制到相应的元素中。因此 ，要创建类对象数组，则这个类必须有默认构造函数。因此实践中，我们可以先使用默认构造函数创建数组，然后在后续的流程里根据需要创建对象并赋值给数组成员，这也是主流的基本类型数组的使用方式。