# C++笔记 

---
- **学习方法**  
> 学习C\++有一个捷径，那就是学会编译器的思维，了解它可能的行为，再来读C\++源程序。一旦发现了编译器的行为与预期的差异，那么再去通过学习和分析，调整自己错误的理解。这样就会编写出正确、高效的C++程序。
---
# **知识补充**  
> **条件操作符**  
-  用法 :: <表达式1>?<表达式2>:<表达式3>  
 如果表达式为true，返回表达式2的值；否则返回表达式3的值  
> **typeid操作符**  
-  用法 :: typeid(类型 || 变量).name()  
 通过name()函数获取该类型或变量的名字。  
> **安全使用数组下标**  
- 当使用数组尺寸之外的的下标访问元素时，C++编译器不会给出任何提示！这一点非常可怕。非法的赋值会改变某块内存中的值。防止使用非法的下标，以免埋下重大隐患。  
> **安全使用字符串**  
- 字符数组不是C\++的基本类型，所以字符数组的安全必须由程序员自己保证。我们看下面的例子:
```
char str1[] = "hello";
cout << str1 << endl;
str1[5] = '!';
cout << str1 << endl;
改代码输出了str1的末字符，输出如下:
hello 
hello!烫烫烫？
很显然，这不是我们想要的结果。使用'\0'作为字符串时C
++的非强制性约定，编译器不负责字符串的安全。另一方
面，由于字符串本身就是字符数组，也会带来越界访问的
隐患。
```
> **void\*指针**
- 一种特殊的指针类型，可以存放任意对象的地址   
- 注意:  
 void\*指针地址存放一个内存地址，地址指向内容不确定  
 void\*指针一般用来和别的指针比较，作为函数的输入输出 || 赋值给另外一个void\*指针  
> **引用**
```
int i;
int & ri = i;   //类型 & 变量 = 引用对象
```
> **结构常见错误**  
- 使用了未初始化的结构成员  
- 指定了太多的初始值  
> **位域**    
- 定义结构时，可以指定每个数据成员所占的比特位数。这时数据成员则可以称作位域。位域是为了节省内存。
```
struct Time{
  unsigned hour : 5;    //5 bits,0~31
  unsigned minute : 6;    //6 bits,0~63
  unsigned second : 6;    //6 bits,0~63
};
cout << sizeof(Time) <<endl;
输出结果：
4
``` 
> **联合**  
- 联合也称作共用体，多个数据类型共用一块地址，起作用的只有一个数据类型。相当于多选一。
```
union ASCII{
    char c;
    short i;
};
ASCII m;
m.i = 70;
cout << ASCII码为 << m.c << endl;
m.c = 'a';
cout << 字符a的ASCII码为: << m.i << endl;
输出结果如下:
ASCII码为F
字符a的ASCII码为：97
```
> **枚举**  
- 枚举采用关键字enum，用来定义一组常量
```
enum Arrow{
    UP,DOWN,LEFT,RIGHT
};
Arrow a1 = UP;  //ok
Arrow a2 = 100; //error
cout << a1 << endl;
输出结果为:
0
```
- 默认情况下，枚举值第一个成员对应的值为0，以此类推。当然了，也可以在定义枚举时手动指定每个枚举值。  
> **typedef**  
- typedef提供了为某种既有类型取别名的功能。 
```
typedef int zhengxing;
int t1;
zhengxing t2;   //int == zhengxing
常见用法
· 定义新的类型，以提高代码的可读性，并有效封装代码中的内部类型。
· 另外一种就是函数的指针的类型定义，如：在Windows线
程编程中，就有类似的线程函数接口定义：
    typedef void * LPVOID;
    typedef DWORD WINARI ThreadProc(LPVOID 1pParamter);
```
> **数据类型修饰符**  
- const  
    中文含义为“固定不变的”，所以const变量被称为常量或者常熟变量。const毕竟还是一个变量，它具有自己的内存地址，不过它不可以被修改。
```
int i = 100;
int m = 200;
int* ip0 = &i;  //非const
int* const ip1 = &i;    //const 修饰int*
int const * ip2 = &i;   //const 修饰int
const int* ip3 = &i;    //const 修饰int
const int* const ip4 = &i;  //const 同时修饰ip4和*ip4

ip0 = &m;
*ip0 = 101;

//ip1 = &m;
*ip1 = 101;

ip2 = &m;
//*ip2 = 101;

ip3 = &m;
//*ip3 = 101;

//ip4 = &m;
//*ip4 = 101;

注意到ip1、ip2、ip3之间的差别。ip1时指针常量，而ip2
和ip3都是常量指针。ip1指针不能被指来指去，而ip2和ip
3恰恰相反。它们本身可以被指来指去，但是它们指向的内
容只读，不能被修改。ip4综合了两种特点，提供一个最安全的指针。

·常见用法
取代宏，定义一些不可更改的值
```  
- volatile  
- 不多见，一般情况下，只有底层才会有到，有兴趣可以百度。  
> **定义带参数的main()函数**  
- main()函数支持另外一种原型  
```
int main(int argc,char * argv[]) {
	cout << "参数数目:\t" << argc << endl;
	for (int i = 0; i < argc; i++) {
		cout << "参数" << i << ":\t\t" << argv[i] << endl;
	}
	return 0;
}
输出结果为exe文件所在目录
可以打开命令窗口进入到程序所在目录输入命令
程序名+空格+bluejoe+vcer.net
会输出程序的参数列表
```
> **预处理指令**  
```
预处理器一般完成如下操作：
· 格式化代码，去多余的空格和注释；
· 进行一些宏替换
· 包含另外一段代码
· 通过一些条件的判断，动态决定是否编译某段代码
预处理指令
#define     //定义宏
#undef      //取消宏的定义
#if         //判断
#else       
#elif
#endif
#error      //输出错误信息
#include    //包含文件
```
- 宏指令   
```
· 一般的，定义宏的时候可以为其指定替换的文本
· 也可以把宏定义成某个表达式
· rand()函数可以返回一个0~RAND_MAX之间的随机整数，R
AND_MAX是由标准库函数定义的宏。如果需要取指定范围的
随机数可以用到RAND_MAX,如
int i = rand * 10 / RAND_MAX;   //0~10之间的数
· 宏可以包含参数，这样的宏也可以叫做宏函数，如：
#define S(x) x * x
int main(){
    cout << "9的平方是:"     << S(9) << endl;
}
· 宏函数具有一个很明显的优点，那就是避免了C++的强类
型检测，如
#define S(a,b) a+b
int main() {
	string s1 = "Hello";
	string s2 = "World";
	cout << S(s1, s2) << endl;
}
· 宏与常量很相似，所以不能引用和指向宏定义的常量
· 宏函数也是会有副作用的，如
#define S(x) ((x) * (x))
int i = 100;
cout << "S(101);" << S(i++) << endl;
输出如下: 
S(101): 10000
结果并不是我们期待的101*101，避免副作用的方法，那就
是正确运用宏，把宏看成一种预编译时期的文本替换，而
这，也正是宏原本的含义。

· #操作符
如果宏定义中出现了‘#’，预处理器会将#后面的参数括成
一个字符串进行替换，如
#define S(i) cout << "S("#i")" << ((i) * (i)) << endl;
S(90);//等同于cout << "S("90")" << ((90) * (90)) << endl;
· ##操作符
“##”用于将两侧的参数合并成一个。如
#define RGB(rr,gg,bb) 0x##rr##gg##bb
int red = RGB(FF,00,00);
//会被替换成
int red = 0xFF0000;
· 取消宏
“#undef”用于取消指定名字的宏，然后修改宏的值
吐槽一下：个人不知道为什么不能直接删除然后修改
· C++预定义宏
_LINE_      //整数，代表代号所在行号  
_FILE_      //字符串，代表当前代码所在的文件路径
_DATe_      //字符串代表当前文件的编译日期
_TIME_      //字符串代表当前文件的编译时间
_STDC_      //代表是否为标准C
_cplusplus_ //当前当前的C++版本
· 可以使用这些宏实现特定的功能
bool ok = false;
if(!ok){
    cout << "发生错误:" << _FILE_ << "(" << _LINK_ << ")" << endl;
    cout << "该软件最后发布时间：" << _DATE_ << " " << _TIME_ << endl;
}
```
> **条件编译指令**  
- 预处理通过某些条件的判断有选择的进行处理  
```
· #if···#endif(条件编译的结尾) 
· #else 和 #elif  
与if语句相似
分别与if语句中的else和else if相似
#define IS 9
int main(){
#if IS < 10
    cout << "TEST" << endl;
#elif Is < 5
    cout << "TEST2" << endl;
#else 
    cout << "error" << endl;
#endif
    return 0;
}
· #if define 和 #if !define
前者用于检测指定的宏是否定义
#if define IS
    cout << "已定义" << endl;
#else 
    cout << "未定义" << endl;
#endif
这这种情况可以使用#undef取消对IS的定义（解决了前面不知道它的用法）
还可以使用"!"操作符，指定某个宏没有被定义的情形，
也就是#if !define.(个人感觉等同于#undef)
#if !define IS
    cout << "未定义" << endl;
#endif
· #ifdef 和 #ifndef
前者等价于#if define,后者等价于#if !define：相当于缩写
```
> 文件包含指令  
```
· #include
用于包含一个源文件
文件名用<>时，它指示预处理器从预设的标准路径中搜索
指定的头文件。预设路径一般是编译器自带的include目
录，当前也可以自己添加其他的目录
文件名用双引号括起来的时，预处理器会从当前文件所在的目录中查找文件。
在一些编译器中，还可以使用相对路径查找头文件
· C标准库头文件
<cassert>   //assert宏的定义   
<cctype>    //字符操作函数的操作
<cerrno>    //错误码的定义
<cmath>     //数学函数库
<setjmp>    //错误处理库
<cstdarg>   //可变参数处理宏的定义
<stdio>     //标准输入输出的声明
<stdlib>    //数字函数、内存管理函数、系统函数、随
              机函数等的声明
<cstring>   //C类型的字符串的操作函数的声明
<ctime>     //日期、时间操作函数的声明
· C++标准库的头文件
<string>        //字符串
<iostream>      //流操作
<fstream>       //文件流
<complex>       //复数
<stdexcept>     //标准异常
STL             //标准模板库
· 合理的使用头文件
考虑如下情况：
a.h 包含 point.h    b.h 包含 point.h
c.h 包含 a.h 和 b.h
这种情况下，当编译器处理c.h时，重复定义就出现了
解决办法是，类似如下的办法，重新设计point.h的内容
#ifndef _HEADER_POINt_H_
#define _HEADER_POINt_H_
头文件内容
#endif
以上定义一个宏：_HEADER_POINt_H_(可以自定义)，并通
过它来 判断当前文件是否已经被包含。这样一来，即使po
in.h被包含多次，由#ifndef...#endif定义的point.h文件
的内容也不会被包含多次
· #error
当编译器遇到#error指令时，会停止下来，并在编译窗口
输出#error后面的信息
· #line
用于改变当前行的行号和文件名
· #pragma
属于自定义指令，每个编译器可以自己定义自己的功能
```

---








