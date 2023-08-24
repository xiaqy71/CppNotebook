# 课堂笔记

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

## 引用

### 基本概念

定义：引用是为已存在的变量取了一个别名，引用和引用的变量共用同一块内存空间

用法：类型&引用变量名 = 引用实体

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
+ 不可以改变引用关系：因为其底层是const指针实现的

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
+ 调用一个重载函数或重载运算符时，编译器在编译阶段通过把你所使用的参数类型与定义中的参数类型进行比较，决定选用最合适的定义。选择最合适的重载函数或重载运算符的过程，称为重载决策。

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

需要包含头文件`<vector>`

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

> 插入元素，容量会被扩大为1.5倍或2倍（msvc中是1.5倍）
#### 二维数组

##### 二维数组创建

```cpp
vector<vector<int>> vec;
```

##### 初始化

```cpp
vector<vector<int>> vec = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
```

##### 追加元素

行尾追加元素

```cpp
vec[1].push_back(111);
```

追加一维数组

```cpp
vec.push_back({7,8,9});
```

##### 遍历二维数组

增强for循环

```cpp
for(auto it:vec){
    for(auto its:it){
        cout << its << " ";
    }
    cout << endl;
}
```


### 类

访问权限：

+ protected 类内和子类可以访问
+ public 类外也可访问
+ private 类内访问

#### 类和结构体的区别

类的默认访问权限是private，结构体是public
#### 对象

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

class people
{
public:
    // 属性
    string name = "刘";
    int age = 10;

    // 行为

    void eat()
    {
        cout << "吃饭" << endl;
    }

    // 成员函数在类内声明，类外实现
    void study();
};

void people::study()
{
    cout << "学习" << endl;
}

int main()
{
    people p;
    cout << p.name << endl;
    cout << p.age << endl;
    p.eat();
    p.study();
}
```

#### 构造函数

```c++
#include <iostream>

#include <vector>

#include <string>

using namespace std;
class A

{

private:

    int val;
    int *p = nullptr;

public:
	//无参构造
    A(){};
    A(int val);
    ~A();
};

  
//构造函数
A::A(int val)

{
    this->val = val;
}
```

#### 析构函数

```c++
A::~A()

{
    delete p;
}
```

#### this指针

一个对象的this指针并不是对象本身的一部分，不会影响sizeof(对象)的结果。this作用域是在类内部，当在类的非静态成员函数中访问类的非静态成员的时候，编译器会自动将对象本身的地址作为一个隐含参数传递给函数。

> this指针一般存在栈区或寄存器（由编译器决定）

```c++
A::A(int val)
{
    this->val = val;
}
```

#### new和malloc的区别

+ new是运算符 malloc是库函数
+ new无需强制转换
+ new可以对所得的内存进行初始化
+ delete会调用析构函数，free不会调用析构函数
+ new/delete可以重载
+ new分配内存失败时会抛出异常，malloc分配失败会返回null
#### new malloc 和 free delete 可以混合使用吗

+ 对于基本类型而言，没有区别。根据需要new和malloc可以混用，new[]和malloc可以混用，delete、delete[]和free可以混用
+ 对于构造函数没有作用的类，new和malloc可以混用
+ 对于没有显式定义析构函数的类，delete[]和new[]必须配套使用，delete和free如果想混用，free需要显式调用析构函数

#### 优先队列

```cpp
priority_queue<int, vector<int>,greater<int>> q1;//默认为最大堆结构 greater为最小堆
/*
int：表示优先级队列中存放int类型的元素
vector<int>表示优先级队列由数组模拟
greater<int>表示优先级队列为最小堆
less<int>表示优先级队列为最大堆
*/
q1.pop();//弹出队首元素
q1.top();//返回队首元素
q1.push(3);//向队尾追加元素
```

#### 比较器

```cpp
#include <iostream>
#include <vector>

using namespace std;

class A
{
public:
    int a;
    A(int a);
};

//函数比较器
bool cmp(cosnt A&a, const A&b)
{
	return a.a < b.a;
}

//结构体对象比较器
struct CMP
{
    bool operator() (vector<int>& a, vector<int>& b)
    {
        return a[0] < b[0];
    }
};

int main()
{
    vector<A>vec = { A(3),A(2),A(1) };
    //sort(vec.begin(), vec.end(), cmp);
    sort(vec.begin(),vec.end(),CMP());
    for (auto it : vec)
    {
        cout << it.a << " ";
    }
}
```

#### 继承

##### 继承语法

```cpp
#include <iostream>
#include <string>
using namespace std;

class father
{
    private:
        int pri;
    protected:
        int pro;
    public:
        int pub;
        void fun() {cout << "fun()" << endl;};
        void eat() {cout << "eat()" << endl;};
};

class son:public father
{
    void work()
    {
        //pri = 1;//父类私有成员不能在子类中访问
        pro = 1;
        pub = 1;
    }
}

int main()
{
    son s;
    s.pub();
    s.fun();
    s.eat();
    s.work();
}

```

##### 继承方式

+ 凡是基类中私有的，派生类都不可以访问
+ 基类中除了私有的成员，其他成员在派生类中的访问属性总是以（继承方式，基类的访问属性）中安全性高的方式呈现。（安全性级别：私有>保护>公有）

```cpp
#include<iostream>
#include<string>
using namespace std;

class father
{
    public:
        int pub;
    protected:
        int pro;
    private:
        int pri;
};

class son:private father{
    void fun()
    {
        pri = 1;
        pro = 1;
        pub = 1;
    }
}

class grandson:public son
{
    void fun(){
        pub = 1;
        pro = 1;
    }
}

int main()
{
    son s;
    s.pub = 1;
    return 0;
}
````
