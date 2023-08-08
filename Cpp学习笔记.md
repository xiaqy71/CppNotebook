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

