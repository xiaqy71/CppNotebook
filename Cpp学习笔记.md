# 笔记

## 输入输出流

+ 头文件：`<iostream> `
+ C++风格头文件不以.h结尾
+ cin 从控制台读入内容到变量
+ cout 从变量输出内容到控制台
+ std标准命名空间：C++标准库函数或对象都是在命名空间std定义

```cpp
#include <iostream>

using namespace std;

int main() {
    int a;
    cin >> a;
    cout << "a = " << a << endl;
}
```

## bool类型

bool类型是C++中的基本数据类型，一种整形类型

+ 单独占一字节，取值false(0)或true(1)
+ 任何非0值转换为true, 0转换为false
+ c语言中`<stdbool.h>`

```cpp
#include <iostream>

using namespace std;

int main() {
    bool a1 = -3; //非0即1
    bool a2 = 0;
    bool b1 = true; //true为1
    bool b2 = false; //false为0
    cout << a1 << endl;
    cout << a2 << endl;
    cout << b1 << endl;
    cout << a2 << endl;
}
```

## 文字版Q宠大乐斗

Weapon.h

```cpp
```

Hero.h

```cpp

```

main.cpp

```cpp

```

## 引用

### 基本概念

定义：引用是为已存在的变量取了一个别名，引用和引用的变量共用同一块内存空间

用法：类型&应用变量名 = 引用实体

```cpp
int b = 1;
int& a = b;
int c = 3;
a = c;
```

b为已经存在的变量,a为b的引用，引用是用指针实现的。

### 引用的特点

+ 引用实体和引用类型必须为同种类型
+ 引用在定义时必须初始化并且不能被初始化为NULL
+ 不可以改变引用关系

### 引用的用法

#### const与引用

被const修饰的变量其引用必须也要被const修饰

```cpp
#include <iostream>
using namespace std;

int main()
{
    const int a = 1;
    int& b = a; // 报错
    const int&c = a; //表示不可用通过c修改a
    return 0;
}

```

#### 参数与引用

引用作为函数参数时的原因：

  + 在函数内部会对此参数进行修改
  + 提高函数调用和运行效率

函数调用时，值的传递机制是通过“形参=实参”来对形参赋值达到传值目的，产生了一个实参的副本。而引用不用经过值的传递机制，已经有了实参值的信息。所以没有了传值和生成副本的时间和空间消耗。当程序对效率要求比较高时，这是非常必要的。

```cpp
#include <iostream>
using namespace std;

void swap(int &a, int &b)
{
    int c = a;
    a = b;
    b = c;
}

int main()
{
    int a = 1, b = 2;
    swap(a, b);
    cout << a << "  " << b << endl;
}
```

#### 返回值与引用

+ 返回值为引用的好处：在内存中不产生返回值的副本

```cpp
#include <iostream>
using namespace std;

int& fun(int a)
{
    a += 2;
    return a;
}

int main()
{
    int a = 3;
    int b = fun(a);
    cout << a << endl;
    return 0;
}
```

##### 引用和指针的区别

+ 引用在初始化时不可以初始化为NULL，指针随意
+ 引用一旦指定了引用关系就不可改变
+ 指针有多级指针而引用没有多级引用
+ ++的含义不同
+ sizeof()计算时的结果不同
+ 指针是实体需要分配内存空间；引用只是变量的别名 无需分配内存空间

### 函数重载

+ c++ 允许在同一个作用域中的某个函数（函数重载）和运算符指定多个定义
+ 在同一个作用域内可以声明几个功能类似的同名函数，但是这些同名函数的形式参数（个数、类型、顺序）必须不同。
+ 调用一个重载函数或重载运算符时，编译器通过把你所使用的参数类型与定义中的参数类型进行比较，决定选用最合适的定义。选择最合适的重载函数或重载运算符的过程，称为重载决策。

```cpp
#include <iostream>
#include <vector>
using namespace std;

void test(int a, int b)
{
    cout << "int" << " " << "int" << endl;
}

void test(int a, int b, int c = 3)
{
    cout << "int" << " " << "int" << " " << "int" << endl;
}

void test(double a, double b)
{
    cout << "double" << " " << "double" << endl;
}

void test(int a, double b)
{
    cout << "double" << " " << "int" << endl;
}

void test(double a, int b)
{
    cout << "double" << " " << "int" << endl;
}

int main() {
    //test(3, 4); 函数参数默认值导致了二义性问题，编译器不知道调用哪个函数
    test(1.1, 1.1);
    test(1, 1.1);
    test(1, 1, 1);
    test(1, 1, 1);

    return 0;
}
```

函数参数从右往左入栈

#### 函数默认参数

```cpp
#include <iostream>
#include <vector>
using namespace std;

void fun0(int t, int a = 2, int b = 3) // 可以只传前两个值，此时a不再等于默认值，会输出实参的值a=1
{
    cout << a << " " << b;
}

void fun1(int t, int a, int b = 3) // 报错，默认实参不在形参列表的结尾
{
    cout << a << b;
}

int main() {
    fun0(1, 1);
    return 0;
}
```

### vector类

#### 一维数组

```cpp
Constructors 构造函数
vector();
vector(size_type num, const TYPE &val);
vector(const vector &from);
Operators 对vector进行赋值或比较：vectors之间大小的比较是按照词典规则
v1 = v2
v1 != v2
v1 <= v1
v1 >= v2
v1 < v2
v1 > v2
v[]
back() 返回最末一个元素
capacity() 返回vector所能容纳的元素数量（在不重新分配内存的情况下）
clear() 清空所有元素
empty() 判断vector是否为空（返回true为空）
front() 返回第一个元素
pop_back() 移除最后一个元素
resize() 改变vector元素数量的大小
size() 返回vector元素数量的大小
swap() 交换两个vector
```

[ ]只能修改不能插入
