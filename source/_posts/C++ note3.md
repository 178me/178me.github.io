---
title: C++ note3
date: 2019-06-04 16:47:12
tags: note
categories: C++
---
关于面向对象编程的笔记  

<!--more-->  

# **面向对象**  
---  
> **new 动态内存分配**  
```
int* i = new int;   //类型*变量 = new 类型
int* ip = new int[5];//分配数组
int* (*ip)[5] = new int[5][4]   //分配多维数组
delete [] ip;   //数组的销毁方式
/**思考题
 *1、new如何动态分配多维数组？
    int (*ipp)[4] = new int[5][4];
 *2、分配出来的多维数组如何销毁？
    delete[] ipp;
 **/
delete i;   //销毁地址
```
>  常见错误
- 忘记销毁new出来的地址，会造成内存泄露  
- 多次销毁一段内存；建议采用如下方法判断某段内存是否被销毁过；  
```
if(ip){
    delete ip;
    ip = 0;
}
```
- 销毁一段非new分配的内存  
- 使用被delete的内存  
- 务必要记住，new和delete必须要成对使用  
- new的对象不要盲目使用自增运算符  
- 取值运算需要加上取值操作符\*  
---
>  **默认参数**  
- C++函数中可以带有默认参数  
```
double Add(int num1,int num2 = 0){
    return num1 + num2;
}
· 所有参数都可以具有默认参数
· 默认参数必须从最右边开始
· 不可以使用形参作为默认参数
· 一般来说，默认参数一般使用在函数参数很多的情况下，
它避免了函数调用者必须记住太多太长的参数
```
>  **可变参数**  
- C\++提供一种“可变参数”的机制，即允许参数的数目是可变的。  
```
/* 要定义一个支持可变参数的函数，需要用到头文件<cstd
arg>中的一些东西 */
#include <iostream>
#include <cstdarg>
using namespace std;
int Add(int first...);

int main() {
	int sum = Add(11, 22, 33, -1);
}
int Add(int first...) {
	//准备读取可变参数
	va_list nums;
	va_start(nums, first);   
	//使用<cstdarg>中的va_xxx宏函数处理可变参数
	int sum = 0;
	int num = first;
	//依次读取参数，-1表示结束
	while (num != -1) {
		cout << "+" << num << endl;
		sum += num;
		num = va_arg(nums, int);
	}
	va_end(nums);
	return sum;
}
------------
以上主要思想是使用va_xxx读取参数列表，并进行加和。遇
到-1结束，可变参数处理起来比较麻烦。
```
>  **内联函数**  
- 在进行函数调用前，会将调用函数的地址和参数列表等信息
保留在堆栈中，以便在函数执行结束后，可以返回到原先调
用的程序继续执行。因此对于某些频繁调用的小型函数来说
，这些堆栈存取动作，会降低的程序的执行效率，此时即可
使用内敛函数解决问题。  
内联函数允许函数内部的内容正在调用点直接展开，这样就
避免了传统调用函数过程带来的性能损失。
```
inline int add(int,int);
void add(int a,int b){
    cout << "接收两个数计算和" << endl;
    cout << "和值为:" << a+b << endl;
}
int main(){
    add(1,2);
    /*编译器会改写成*/
    cout << "接收两个数计算和" << endl;
    cout << "和值为:" << a+b << endl;
    ----------
    实际上，inline只是对编译器进行优化的一个建议，
    编译器完全可能会不理会该建议，所以，不要滥用inl
    ine函数
}
```
>  **函数重载**  
- 函数名相同，参数列表不同，就是函数的重载特性
```
函数重载经常出现的错误示例：
int add(int a){
    return a；
}
float add(int a){
    return a
}
//不能依赖于返回值的类型不同选定一个函数
//实参与形参类型不同
//不要认为的制造二义性冲突，例如
int add(int a){
    return a;
}
int add(int a,int b = 10){
    return a + b; 
}
```
- 安全连接和名字重组自行百度了解  
  
> **递归函数**  
- 函数自己调用自己，即递归函数
```
#include <iostream>
using namespace std;

void test(int);

int main() {
	test(10);
}
void test(int num1) {
	cout << "函数开始" << endl;
	if (num1 == 0) return;
	test(num1 / 2);
	cout << "函数结束" << endl;
}
输出结果如下:
函数开始
函数开始
函数开始
函数开始
函数开始
函数结束
函数结束--gg
函数结束
函数结束
--------------
个人是这样理解的,递归就是一个函数嵌套的过程，像上面
的程序有五个函数开始，这是在执行递归之前的语句，也
就是说算上第一次进入函数，这个函数执行了五次，但对
应的函数结束却只出现了四次，那是因为最后一次执行了 
return语句，直接跳出了函数，也就没有后面的语句的执
行。结合理解使用调试功能进行观察效果会更好。
```

> **函数指针**  
- 在C++中提供函数指针，它用以指向一个函数  

```
void (*fp)();   //声明一个类型为void，没有参数的函数指针
fp = &add;  //指向add函数的地址
fp = add    //等同与指向
//调用的方法
fp();       //相当于add()
(*fp)();    //相当于add()，一般用这种来区别这是一个函数指针的调用

```

- 理解函数指针

```
#include <iostream>
using namespace std;

int add(int a ,int b) {
	return a + b;
}
int min(int a, int b);
int main() {
	void (*fp1)(int);
	int (*fp2)(int, int);
	cout << typeid(fp1).name() << endl;
	cout << typeid(fp2).name() << endl;
	cout << typeid(add).name() << endl;
	cout << typeid(min).name() << endl;
}
int min(int a, int b) {
	return a - b;
}
------------
利用typeid输出函数指针类型来理解它
根据这样的特性，我们可以定义函数指针数字组
int (*fp[])(int ,int ) = {&add,&min}
函数指针的定义有点繁琐，建议用typedef来改善可读性。
typedef int (*fp)(int,int);
fp fp1 = add;
fp fp2 = &min;
fp fp3[] = {&add,&min};
```

- 函数与值传递  

```
·值传递有三种方式：传值方式，引用方式，传址方式

·向函数传递参数的时候，除了引用方式外，其他方式都是
在函数内部将参数内容复制一份使用。
```
> **类的设计**
- 类是对象的类型，对象是类的实例  
- 类的设计  

```
· 类的语法定义：
class 类名{
访问控制符:
    成员列表
};
· 类也可以先声明后定义，声明方式如下
class 类名;
· 对象的定义
类名 对象名;
类名 * 对象名 = new 类名();
//类的两种实例化方法
还可以定义类对象的指针和引用
类名 * 指针名 = &对象名;
类名 & 引用名 = 对象名;
· 数据成员的访问
可以使用"."来访问数据成员
对象指针用"->"来访问
还支持用"::"域名操作符访问成员，但常用以上两种
· 成员访问控制
访问控制符一般包括两种
public:共有的，可以在任意地方访问成员
private:私有的，只能在类的内部访问成员
有一种不成文的规矩，就是把私有的数据成员加上下划线
· 成员函数
成员函数其实与普通的函数没有太大的差别，它可以被内
联，也可以被重载，也可以使用默认参数，唯一的区别就
是定义是要加上类域的帽子，但声明不需要，如
class A{
    void a();
};
void A :: a(){  //数据类型 所属类名 :: 函数名
    cout << "我属于A类" << endl;
}
· this指针
在成员函数体内，有一种特殊的指针，this指针。this指
针指向当前类对象本身，可以用this调用对象的成员：
this -> a();
注意:this不能被改变，也不能在类作用域以外的地方使用
· 内存中的类
类包括数据成员和成员函数，但内存中的类只包括其数据
成员，成员函数其实并不属于对象，它只是一个特殊的全
局函数。
· 类的长度等于所有数据成员的长度之和，但是考虑如下情况：
#include <iostream>
using namespace std;
class A {
public:
	int a;
	int b;
	char c;
	char d;
};
class B {
public:
	int a;
	char c;
	int b;
	char d;
};
int main() {
	cout << sizeof(A) << endl;
	cout << sizeof(B) << endl;
}
输出如下：
12
16
为了程序运行的效率，编译器在一定的设置下可能对成员
排放位置做一些调整，使得整个结构体为一个字节长的整
数倍，这就是所谓的“字节对齐”，上面演示了这种布局的
差异，可以看出来，，不同的排列方式会引起类字节长度
的差别，大家写代码一定要考虑这一点。
```

- UML类图可以表示一个类，便于理解，如  
- 私有是"-"前缀，共有则是"+"前缀  

|类名|  
|:-:|
|数据成员|
|函数成员|





>  **类的讨论**  

```
· 类与结构
C++中提供结构和类。在数据成员上，它们唯一的差别在于
：结构成员的默认访问控制为public，类的默认访问控制
为private。
class是一个全新的概念，所以人们更愿意接受class是真
正的面向对象概念。而对于struct，人们更愿意用来描述
那些没有行为或者行为能力很弱的数据结构体。
· 抽象性
在软件开发的分析、设计时对具体问题进行归纳、概括，
并将这一类对象的公共特性加以条理化和严格描述，它主
张集中思想和精力，考虑关键、主要、实质性的问题，去
掉非主要的部分，便于开发人员对整个问题准确地认识。
为具体的对象定义一个类的过程就是抽象。
· 封装性
保证程序员用正确的方式操作对象，并将一些操作细节隐
藏起来。主要体现如下方面:
--- 保护私有数据:不允许外部程序直接访问私有的数据
--- 隐藏了操作细节:提供公用成员函数提供外部调用
根据这两个方面,我们可以举一个例子来说明:
#include <iostream>
using namespace std;
class A {
	/**
	 *声明一个A类，包含两个数据成员并封装成4个成员函数
	 *这里使用this指针加深印象
	 **/
	string _name;
	string _sex;
public:
	void setname(string name) { 
		this ->_name = name; 
	}
	void setsex(string sex) { 
		this->_sex = sex;
	}
	string getname() { return this ->_name; }
	string getsex() { return this ->_sex; }
};
int main() {
	/**
	 *使用指针的方法实例化A的一个对象
	 *定义两个string临时变量
	 *调用公共的数据成员封装函数进行赋值和输出
	 **/
	A * a1 = new A();
	string temp1,temp2;
	cout << "请输入你的姓名";
	cin >> temp1;
	a1->setname(temp1);
	cout << "请输入你的性别";
	cin >> temp2;
	a1->setsex(temp2);
	cout << "姓名:" << a1->getname() << endl;
	cout << "性别:" << a1->getsex() << endl;
}
程序员的责任就是封装复杂的数据和操作，以简单明了的
共有函数的方式为外部程序提供对象操作接口
```
    