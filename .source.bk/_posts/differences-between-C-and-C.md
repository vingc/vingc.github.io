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

5. 输入和输出，C++使用”cout“和”cin“对象完成输出和输入操作。如”cout<<"Hello World"<\<endl;“和”cin>>var;“；“<<”插入运算符，“>>”提取运算符。

6. 命名规则，没有差异，以单下划线或双下划线开头的名字预留给编译器使用。

7. sizeof语言内置运算符，没有差异，参数可以为变量名或者类型名；参数为类型名时必须使用括号，如“sizeof(int)”，“int a, sizeof a;”.

8. 变量初始化，C++新增了大括号“{}”初始化方式（列表初始化，不允许缩窄转换，即不能赋值超出类型表示范围），如“int a{10};”、“int a={10};”、“int a{};”；如果大括号没有内容，默认初始化为0，变量和大括号之间的等号是可选的，也可用于字符串常量初始化字符数组、string对象、结构变量，如char date[] = { "Le Chapon Dodu" }；
   char date[] {"The E legant P la te "} ;
   string date = { "The Bread Bow l"};
   string date {"H ank's Fine E a ts "}; 。

9. 基本类型，C++新增了“char16\_t”和“char32\_t”；C++提供了bool类型，C在C99标准里才新增bool类型，且需要使用头文件"stdbool.h"。

10. 浮点常量，C++默认的浮点常量是double类型，除非通过后缀指定类型，如2.3f和1.2F为float类型，3.3和3E2为double类型，33.4l和33.4L为long double类型。

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

17. 定位new运算符，new分配数组/结构/基本类型的时候可以同时初始化，如“int* a=new int(5); int* b=new int{10};”；定位new运算符使开发人员可以指定分配内存的buffer地址，如”char buffer[50]; int * t = new (buffer) int[5];“，编译器会把t[5]放到buffer上，t的开始地址即buffer的开始地址，buffer在语义是指示地址开始的位置。

18. 动态数组，C++支持动态数组，即运行时确定数组长度和创建数组，如“Typename * pointer = new Typename[nums];”，“int * pIntArray = new int[10];”；释放使用“delete [] pointer;”语法。

19. 字符串首元素地址，在cout和C++大多数表达式中，char数组名、char指针以及双引号包围的字符串常量都被解释为字符串第一个字符的地址。

20. For-each语法，C++支持for-each的用法，如“for ( int x: {1,2,3,4} )”，“int x[10]; for ( int x: x )”；这种用法还可以用于容器。，

21. 逻辑运算符，C++支持保留字and、or、not分别代替&&、||、!运算符；因此C++不可以定义这些名字的变量；因为C不支持这三个保留字，所以为了兼容性，最好不要使用这三个单词作为逻辑运算符。

22. 函数原型，当函数定义在使用之前时，C和C++的函数原型声明都是可选的；当函数定义在使用之后时，某些C的函数原型声明是可选的（返回值是int时不需要函数原型声明，但是不建议这么使用，因为编译器无法检查参数列表），C++的函数原型声明是必须的。C++的函数原型省略参数列表时，如“int fun()”，表示参数类型为“void”；而C的函数原型省略参数列表时，表示未定义。无论是C或C++声明函数原型时，形参变量名是可选的，如“int fun( int, int b )”，而且此处的变量名可以与定义处的变量名不同。（私以为，这么灵活的设计反而使初学者难以记忆，感到混淆；工程里不用考虑这么多，所有定义的函数都需要声明原型，这样可以保证兼容性和可移植性。）

23. 左值引用&右值引用，C++增加了这两个语法特性；左值引用是定义一个变量的别名，如“int a=10; int & b = a;”，在使用中b和a一样，b的地址等于a的地址；引用必须在定义时初始化，而且定义后不能改变引用指向的变量地址。函数形参声明为左值引用，这种参数传递方式称为按引用传递；可以在被调用函数中像调用函数中一样修改变量的值（类似于指针参数的功能）。如果引用参数是const，编译器在两种情况下可能会生成临时变量存储实参的值，case1 实参的类型正确但不是左值，case2 实参的类型不正确但可以转换为正确的类型。左值一般指赋值等号的左边，可以用地址引用的值，非左值包括字面常量（不包括字符串常量）和多项表达式。右值引用的声明如“int && b = sqrt(36.0);”；左值引用的别名不占用额外的存储空间。（强调函数引用参数是const时，编译器才会生成临时变量的原因是，引用参数主要是为了提供被调用函数修改调用函数变量值的一种形式，并在传递参数时避免大块内存的copy，而临时变量的生成，会阻止该过程；当引用参数声明为const时，明确说明对引用参数的修改不能影响被调用函数内变量，因此可以使用生成临时变量的形式。）

24. 函数的默认参数，C++支持声明函数的默认参数，比如声明函数“int f( int a = 1 );”，在调用f()时因为未给出实参，因此编译器采用默认值1；对于带参数列表的函数，必须从右到左的一次添加默认值，即如果给某个参数设置默认值，则它右边的所有参数都需要设置默认值；调用函数时，从左到右依次给出实参，不能跳过某个参数，如此调用是不允许的“fun( 1, ,2 );”。

25. 函数重载，C++允许同一个函数名，定义多个具有不同参数列表的不同实现，调用函数时，编译器优选最匹配的函数。

26. 函数模板，在多个类型共用同样的算法时，C++支持函数模板功能，如“template \<typename T> T swap( T &a, T b );”，声明和定义都需要加上“template \<typename T>”，语义为使用类型名T建立模板，类型名可以为任意名字，只要符合C++命名规则。

27. 隐式实例化（implicit instantiation），函数模板本身并不是函数定义，只是编译器用来生成具体函数定义的模板。编译器使用模板为特定类型生成函数定义时，得到一个函数实例，这叫做隐式实例化。

28. 显示实例化（explicit instantiation），C++支持显示实例化，即让编译器直接生成特定类型的函数定义。如“template swap<int>(int a,int b);”，语义为“使用swap()模板生成int类型的函数定义”。显示实例化不需要另外定义函数实现，只需要给出声明。

29. 显示具体化（explicit specialization），如“template<> swap<int>(int a, int b);”，或者“template<> swap(int a,int b);”，语义为“不要使用swap()模板来生成int类型的函数定义，而是使用专门为int类型显示的定义的函数定义”。具体化除了要给出函数声明，还需要专门提供具体的函数实现。具体化函数优先级高于模版函数，而非模板函数优先于具体化和模板函数。~~如果在同一个文件中同时声明了同一个模板的同一个类型的显示具体化函数和显示实例化函数，则会出错。（测试发现，编译和运行并不会出错，使用该类型的实参调用函数时，调用了具体化函数。）~~

30. decltype关键字，C++11新增特性，在泛型函数中可能遇到无法确定变量类型的情况，如“T a, T b, ?type? x=a+b;”，但是可以用decltype声明“decltype(a+b) x;”，语义是，变量x的类型为a+b表达式的类型。一般声明格式为“decltype(expression) var;”，编译器依次应用如下规则，得出var的类型：

    * 如果expression是未用括号围起来的标识符，则var的类型与该标识符的类型相同，包括const/指针等限定符，如“int & a=1; decltype(a) var;”，var类型为int &。

    * 如果expression是函数调用，则var的类型与函数返回值类型一样，如“int f(int a); decltype(f(2)) var;”，var的类型为int，但是该声明并不会真的调用函数，编译器只需要check该函数的返回值类型。

    * 如果expression是一个左值，则var是指向该类型的引用，如“int a=1;decltype((a)) var = a;”，var的类型是int &；

    * 如果前面的条件都不满足，则var的类型是expression的类型，如“char a = 1,short b=2;decltype(a+b) var;”，var的类型是int (因为char+short在表达式中会导致整形提升，编译器把char和short提升为int后计算，因此表达式结果的类型是int)。

      decltype可以配合typedef使用，如“typedef decltype(x+y) xy; xy var;”。

31. 后置返回类型，语法“auto fun( int a, int b ) ->double {/*func body\*/}”，->double被称为后置返回类型，auto是占位符，用于表示后置返回类型提供的类型，在这里是double。这个特性通常结合模板和delctype使用，如

    ~~~C++
    template <typename T1, typename T2>

    auto fun( T1 x, T2 y )->decltype(x+y) 

    {/*func body*/}
    ~~~

    decltype在参数声明后面，位于x和y的作用于内。

32. 全局变量，C和C++都支持使用extern关键字引用声明其他文件中定义的全局变量，如“extern int g_lab;”；C++还支持使用作用域解析运算符修饰全局变量，可以在不使用extern引用声明的情况下直接使用其他文件定义的全局变量，如“cout<<::g_lab<<endl; int a = ::g_lab;”。

33. auto和register，在C++11之前，auto指示修饰的变量为自动变量（即临时变量），register指示修饰的变量为寄存器变量；C++11发布后，auto用于自动类型推断，register只是指示修饰的变量为自动变量。

34. mutable关键字，C不支持，而C++支持的特性，主要是配合const使用，mutable可以修饰类的成员或者结构的成员，在使用const修饰类或者结构变量之后，mutable修饰的成员仍然可以被修改。

35. const关键字修饰全局变量，如”const int g_lab=10;“，C中const不影响全局变量的作用域，但在C++中，const修饰全局变量时，等同于static，该变量的作用域变成本文件；C++之所以支持该特性，是为了可以把常量定义放到头文件中，当多个源文件包含头文件时，对该常量的定义不违法唯一定义规则(ODR);”extern const“同时使用时，extern覆盖const的作用域特性，使该常量可以被其他源文件引用声明然后使用，但该常量同时具备const的常量特性，引用声明可以有多处，但定义只可以有一处（ODR）。

36. 语言链接性，C++因为支持同名函数，因此编译器执行名称修饰，把同名不同参数列表的函数翻译成不同的名字，这和C语言编译器不同，所以在C++源文件中调用C编译的库文件里的函数时，要使用extern "C" 修饰函数原型声明，如” extern "C" void fun(int);“，该语义告诉编译器使用C语言的协议用于函数名字查询。相应的extern "C++"修饰函数原型声明时，告诉编译器使用C++语言的协议用于函数名字查询（这在C++源代码里是默认行为）。

37. namespace名称空间，除了C传统的全局声明区域和代码块声明区域之外，C++支持另外一种名称声明区域即名称空间。不同声明区域之间的名称可以相同，名称空间可以起到名称隔离的作用，给名称的使用提供更多选择。使用语法”namespace test { int a; struct bff{}; void fun(); void real(){} }“，可以使用作用域解析运算符::使用名称空间中的名称，如”std::cin>>test::a;“。也可以使用using 编译指令或者using声明，把名称空间中的全部名称或者某些名称导入当前声明区域，using编译指令”using namespace test;“，using声明”using test::a;“。名称空间可以嵌套，using指令也可以传递，如果把A导入B，则把B导入C的时候相当于同时A导入C。在代码块中使用using声明时，导入的名称可能与本地变量相同名称冲突；但使用using编译指令导入所有名称时，本地变量相同名称会覆盖名称空间的名称。未命名的名称空间使内部的名称相当于作用域为本文件的静态变量，如”namespace {int a=10;}“相当于定义了”static int a=10;“。名称空间可以定义别名，如namespace MFF = merge:file:first;

38. （未完待续）

39. ​

    ​