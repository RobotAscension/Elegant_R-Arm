# 一、C++ 基础知识

## (一) 注释

1. 单行注释：// 描述信息
2. 多行注释：/_ 描述信息 _/

```cpp
//我是单行注释
/*
嘿嘿
我是多行注释
*/
```

## (二) 数据类型

### 1、字符串型

1. 定义：string 变量名 = "字符串值"，需要 string 头文件
2. 运算：
   - 字符串复制用赋值号 =
   - 字符串连接用 +
   - 字符串比较用 < > == !=
3. 字符串数组：每一个字符串元素只包含字符串本身而不包括'\0'

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string str1 = "hello world";
    string str2 = str1;
    string str3 = str1 + str2;

    cout << "str1 = " << str1 << endl;
    cout << "str2 = " << str2 << endl;
    cout << "str3 = " << str3 << endl;

    if(str1 == str2)
    {
        cout << "str1等于str2" << endl;
    }
    else if(str1 < str2)
    {
        cout << "str1小于str2" << endl;
    }
    else if(str1 > str2)
    {
        cout << "str1大于str2" << endl;
    }
    return 0;
}
```

注：字符串的比较还可以使用 compare 函数以及 strcmp 函数

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string str4 = "hello world";
    string str5 = "hello cpp";
    string str6 = "python is perfect";

    cout << str4.compare(str5) << endl;//20 w的ASCII值比c的ASCII值大20
    cout << str4.compare(str6) << endl;//-8 同上
    cout << str5.compare(str6) << endl;//-8 同上
    return 0;
}
```

### 2、布尔型

(1) 定义：bool 变量名 = true or false
(2) 内存大小占 1 个字节，使用 cout 会输出 1 或 0

## (三) 输入与输出

1. 输入：cin >> 变量;
2. 输出：cout << 变量或常量 << endl;
3. endl 起换行作用

## (四) 运算符

### 1、作用域运算符 ::

指定所需要的作用域

```cpp
std::cout << "hello";
```

注：注明作用域有助于理解代码，因此尽量不适用 using namespace

### 2、new 运算符

1. 定义：开辟堆区内存
2. new 类型 (初值)
3. new 在分配数组空间时不能指定初值

```cpp
//创建一个初值为10的整型指针
int* pvalue = new int(10);
//创建一个大小为10的整型数组，首元素地址存放在parr变量中
int* parr = new int[10];
```

注：指针类型的大小由系统位数决定，在 64 位系统中，所有类型的指针大小均为 8 字节

### 3、delete 运算符

1. 定义：撤销内存
2. delete 指针变量
3. 对数组空间操作时需要加[]

```cpp
//销毁指针
delete pvalue;
//销毁数组指针
delete [] parr;
```

注：new 出来的变量存放在堆区中，需要 delete 手动释放内存

## (五) 内存模型

### 1、代码区

- 定义：存放函数体的二进制代码，由操作系统进行管理

### 2、全局区

- 定义：存放全局变量和静态变量以及常量，在程序结束时由操作系统释放

### 3、栈区

- 定义：由编译器自动分配释放，存放函数的参数值、局部变量等
- 注意：不要返回局部变量的地址

### 4、堆区

- 定义：由程序员分配和释放，若程序员不释放，程序结束时由操作系统回收
- 使用 new 在堆区开辟内存 delete 撤销内存

## (六) 引用

### 1、基本语法

1. 定义：数据类型 & 别名 = 原名
2. 引用后的变量和原变量指向同一内存空间
3. 注意事项：引用必须初始化、引用在初始化后不能改变

```cpp
#include <iostream>
using namespace std;

int main()
{
    int i = 100;
    int& r = i;

    cout << "i = " << i << endl;
    cout << "i's reference = " << r << endl;
    return 0;
}
```

### 2、引用做函数参数

1. 作用：函数传参时，可以利用引用让形参修饰实参
2. 优点：可以简化指针修改实参

### 3、引用做函数返回值

1. 引用是可以作为函数返回值存在的
2. 不要返回局部函数引用
3. 函数的调用可以作为左值
   注：函数的调用作为左值时，修改得是函数的返回值

### 4、引用补充

1. 引用的本质在 C++ 实现是一个指针常量
2. 常量引用: 主要来修饰形参，加 const 修饰，防止误操作

## (七) 函数

### 1、函数的默认参数

1. 在 C++ 中，函数的形参列表中的形参是可以有默认值的。
2. 语法：返回值类型函数名（参数 = 默认值）

```cpp
void fun1(int a, int b = 20)
{
    cout << a << endl;
    cout << b << endl;
}
```

3. 若无数据传入，则函数参数值取默认值；若传入数据，则使用自己的数据。
4. 若某一位置有默认值参数，则它从左到右的参数都要有默认值
5. 若函数声明有默认参数，则函数实现就不能有默认参数；反之，函数实现有默认值，则声明不能有默认值。

```cpp
#include <iostream>
using namespace std;

void fun1(int a, int b, int c);

void fun1(int a, int b, int c = 10)
{
    cout << a << endl;
    cout << b << endl;
    cout << c << endl;
}

int main()
{
    fun1(23, 12);
    return 0;
}
```

### 2、函数的占位参数

1. C++ 中函数的形参列表可以有占位参数，调用函数时必须填补此位置。
2. 语法：返回值类型函数名（数据类型）{}
3. 占位参数可以有默认参数
   注：函数的占位参数意义不大，特殊需要再写

### 3、函数的重载

在同一作用域下，函数的名称可以相同，其参数类型或个数或顺序
不同，称为函数的重载。

1. 函数重载满足条件
   - 同一作用域下
   - 函数名称相同
   - 函数参数类型不同或个数不同或顺序不同

```cpp
#include <iostream>
using namespace std;

void fun(int a, int b)
{
    cout << a << endl;
    cout << b << endl;
}

void fun(double a, double b)
{
    cout << a << endl;
    cout << b << endl;
}

int main()
{
    fun(23, 12);
    fun(12.3, 3.14);
    return 0;
}
```

2. 函数的返回值不能作为函数重载的条件
3. 注意：引用作为重载条件、函数重载有默认参数
4. int& 和 const int& 不是同一类型，故可以进行函数重载, 传入参数分别为整型变量和整型常量
5. 当函数重载遇到默认值参数时，有可能出现二义性，即 void fun()和 void fun(int a=10), 此时 fun() 不知道会调用哪一个函数

# 二、类和对象

C++ 认为万事万物皆对象，对象有其属性和行为，具有相同性质的对象，可以抽象为类。

## (一) 封装

### 1、属性和行为作为一个整体

1. 在设计类时，属性和行为写在一起，表现事物
2. 语法:class 类名 {访问权限：属性 / 行为};

### 2、权限控制

1. 类中的访问权限共有三种，public(公共权限)、protected(保护权限)、private(私有权限)
   - 公共权限：成员类内可以访问，类外可以访问
   - 私有权限：成员类内可以访问，类外不可以访问，子类不可以访问父类
   - 保护权限：成员类内可以访问，类外不可以访问，子类可以访问父类
2. struct 和 class 区别在于默认权限不同，struct 默认公共，class 默认私有
3. 成员属性设置为私有，通过行为函数控制成员，这些函数称为类的接口

## (二) 对象特性

### 1、构造函数和析构函数

对象的初始化和清理是由构造函数和析构函数来实现的，这两个函数会被编译器自动调用，如果我们不提供该函数，则编译器会提供本身的函数来空实现。

1. 构造函数：主要作用在于创建对象时为对象的成员赋值，构造函数由编译器自动调用，无需手动调用
   - 构造函数语法：类名 (){}
   - 构造函数无返回值也不写 void
   - 函数名称与类名相同
   - 可以有参数，因此可以发送函数重载
   - 自动调用构造函数
2. 析构函数：主要在于对象销毁前自动调用构造，无需手动调用，而且只调用一次
   - 析构函数： 类名 (){}
   - 析构函数无返回值也不写 void
   - 函数名称和类名一致，并在前面加上
   - 祈构函数无参数
   - 自动调用析构函数

### 2、构造函数的分类及调用

构造函数按参数可以分成有参构造和无参构造 (默认构造函数)，按类型分为普通构造和拷贝构造

1. 拷贝构造函数需要传入同一个类的属性的参数实现拷贝构造
   - 拷贝构造函数语法：类名 (const 同一类名 & 参数名)
2. 调用方式有括号法、显示法、隐式转换法
   - 括号法：类名 对象名 (参数)
   - 显示法：类名 对象名 = 类名 (参数)
   - 隐式转换法：类名 对象名 = 参数

```cpp
Person p1;
Person p2(p1);
Person p3 = Person(p1);//Person(10)为匿名对象
Person p4 = p1;
```

3. 匿名对象特点：当前行执行结束后，系统会立即回收该匿名对象
4. 不要利用拷贝构造函数初始化匿名对象，会出现重定义现象

```cpp
// Person(p2);//错误
```

5. 调用默认构造函数时，不要加 ()，不然可能会认为函数的声明

### 3、拷贝构造函数调用时机

C++调用拷贝构造函数有三种情况：

- 使用一个已经创建完毕的对象来初始化一个新对象
- 值传递的方式给函数参数传值
- 以值方式返回局部对象

### 4、构造函数调用规则

默认情况下，C++ 编译器至少给一个类添加 3 个函数:

- 默认构造函数 (无参、函数体为空)
- 默认析构函数 (空实现)
- 默认拷贝构造函数 (值拷贝)

注意：

1. 如果用户定义有参构造函数，C++ 不再提供默认无参构造，但是会提供其他构造函数
2. 如果用户定义拷贝构造函数,C++ 不再提供其他构造函数

### 5、深拷贝和浅拷贝

1. 浅拷贝：简单的赋值拷贝操作，使用系统默认提供的拷贝构造函数，会进行浅拷贝操作

```cpp
Person p1(18, 170);
Person p2(p1);//浅拷贝

//若使用下面的析构函数，对于指针变量height_，由于浅拷贝，p2未给height_开辟新的内存，即p1和p2指向同一块内存，导致该区域内存释放两次(p1一次，p2一次)
~Person()
{
    if(height_ != NULL)
    {
        delete height_;
        height_ = NULL;
    }

    cout << "析构函数的调用" << endl;
}
```

解决方法：深拷贝

2. 深拷贝：在堆区重新申请空间，进行拷贝操作
3. 析构函数：将开辟在堆区的内存空间释放
4. 编译器提供的拷贝构造函数会做浅拷贝操作，浅拷贝会使堆区内存重复释放
5. 如果有在堆区开辟的内存，需要自己写拷贝构造函数，防止浅拷贝操作带来问题

### 6、初始化列表

C++ 提供了初始化列表语法，用来初始化类的属性

语法：构造函数 (参数): 属性 1(值 1)，属性 2(值 2)

```cpp
Person(string name, int age, int height) : name_(name), age_(age), height_(height) {}
```

另外，对于继承某基类的子类，其构造函数也可以使用初始化列表的方式，通过调用基类的构造函数来完成对基类属性的初始化

```cpp
#include <iostream>
using namespace std;

class Base
{
public:
    Base(string name): name_(name) {}

protected:
    string name_;
};

class Son: public Base
{
public:
    Son(string name): Base(name)
    {
        cout << "我的名字叫做" << this->name_ << endl;
    }
};

int main()
{
    Son s("Tessy");
    return 0;
}
```

### 7、类对象作为类成员

1. 创建的其他某一个类的对象可以作为类的成员

```cpp
class A
{

};

class B
{
private:
    A a;
};

```

2. 当其他类的对象作为本类的成员时，构造函数先构造其他类的对象，析构函数后析构其他类的对象，即其他类的对象的构造和析构包含着本类,即 A 构造、B 构造、B 析构、A 析构

### 8、静态成员

静态成员就是在成员变量和成员函数前加上关键字 static

1. 静态成员变量：

   - 所有对象共享同一份数据
   - 在编译阶段分配内存、存储到全局区
   - 类内声明、类外初始化
   - 有访问权限

2. 静态成员函数：
   - 所有对象共享同一份数据
   - 静态成员函数只能访问静态成员变量
   - 类外访问不到私有的静态成员函数

静态成员变量与函数都可以通过对象和类名两种方式进行访问

```cpp
#include <string>
#include <iostream>
using namespace std;

class Person
{
//有访问权限
public:
    //类内声明
    static string name_;
    int age_;

    static void function()
    {
        cout << "静态成员函数的调用" << endl;
    }
};

//类外初始化
string Person::name_ = "Tom";

int main()
{
    //所有对象共享同一份数据
    //既可以通过对象访问
    Person p1;

    cout << p1.name_ << endl;

    Person p2;
    p2.name_ = "Jetson";

    cout << p2.name_ << endl;

    //也可以通过类名访问
    cout << Person::name_ << endl;

    //对象调用
    p1.function();

    //类名调用
    Person::function();
    return 0;
}
```

### 9、成员函数和成员变量分开存储

1. 在 C++ 中，类内的成员变量和成员函数分开存储

- 静态成员变量和成员函数均不占对象空间
- 所有函数共享一个函数实例
- 只有非静态成员变量才属于类的对象上

2. C++ 编译器会给每个空对象分配一个字节空间，为了区分空对象占内存的位置

```cpp
#include <iostream>
using namespace std;

class Person
{

};

class Phone
{
public:
    int Memory_;//非静态成员变量属于类的对象
    static int CPU_;//静态成员变量不属于类的对象

    void Software()//非静态成员函数不属于类的对象
    {

    }

    static void Hardware()//静态成员函数不属于类的对象
    {

    }
};

void test01()
{
    Person p1;

    cout << "p1的大小为: " << sizeof(p1) << endl;//一个空类的对象所占内存大小为1字节
}

void test02()
{
    Phone p1;

    cout << "p1的大小为: " << sizeof(p1) << endl;
}

int main()
{
    test01();
    test02();

    return 0;
}
```

### 10、this 指针

因为每一个非静态成员函数只会产生一份函数实例，为了区分不同对象，C++ 通过 this 指针指向被调用的成员函数所属的对象，this 指针是隐含在每一个非静态成员函数内的一种指针，是指针常量

this 指针的用途：

- 当形参和成员变量同名时，可用 this 指针来区分
- 在类的非静态成员函数中返回对象本身，可使用 return \*this，返回值类型必须使用类的引用

### 11、空指针访问成员函数

1. 空指针可以访问类中的成员函数，但 this 指针指向为空
2. 为了提高代码的健壮性，需要加入判断 this 指针是否为空

```cpp
class Person
{
public:
    void ShowName()
    {
        if(this == NULL)
        {
            return;
        }

        cout << name_ << endl;
    }

    string name_;
};
```

### 12、const 修饰成员函数

常函数：

- 成员函数加上 const，称为常函数
- const 关键字修饰的是 this 指针，使得成员属性不可以修改
- 成员函数属性加关键字 mutable 后，在常函数中依然可以修改

常对象：

- 声明对象前加 const 称该对象为常对象
- 常对象只能调用常函数

## (三) 友元

### 1、全局函数作友元

在程序中，有些私有属性也想让类外特殊的一些函数或类进行访问，就需要用到友元的技术，友元的目的就是让一个函数或类访问另一个类中私有成员

- 友元的关键字为 friend
- 语法：friend 访问私有成员的全局函数声明;

### 2、友元类

- friend 也可以修饰类，用于访问类中的私有属性
- 类外定义成员函数，需要先在类内声明，再指明成员函数的作用域，即属于哪个类

### 3、成员函数作友元

- 语法：friend 成员函数
- 其中，成员函数必须指明作用域
- friend 修饰的成员函数声明必须在成员函数所属类定义之后定义

```cpp
#include <iostream>
using namespace std;

class Person;

class Man
{
public:
    void showAge(Person &p);
};

class Person
{
    friend void showAge(Person& p);//全局函数做友元
    friend class Man;//类做友元,与下面效果一致
    friend void Man::showAge(Person &p);//成员函数做友元

public:
    Person(int age): age_(age) {}

private:
    int age_;
};

//类外定义成员函数需指明属于哪个类，在类内声明
void Man::showAge(Person& p)
{
    cout << "年龄为：" << p.age_ << endl;
}

void showAge(Person& p)
{
    cout << "年龄为：" << p.age_ << endl;
}

void test01()
{
    Person p1(18);
    Man m1;

    showAge(p1);
    m1.showAge(p1);
}

int main()
{
    test01();

    return 0;
}
```

## (四) 运算符重载

### 1、加法运算符重载

通过全局函数或成员函数重载 + 号，使得两个自定义的数据类型可以直接相加

- 语法：类名 operator+ (类名 & 参数名)
- 函数内容为将类中的属性各自相加

成员函数重载本质调用 p1.operator+(p2)
全局函数重载本质调用 operator+(p1, p2)

```cpp
//通过成员函数重载
Person operator+(Person& p)
{
    return Person(this->name_ + p.name_, this->age_ + p.age_);
}

//通过全局函数重载
Person operator+(Person& p1, Person& p2)
{
    return Person(p1.name_ + p2.name_, p1.age_ + p2.age_);
}
```

### 2、左移运算符重载

作用：直接输出自定义数据类型中的多个数据, << 无法通过成员函数重载,只能通过全局函数重载

- 语法：ostream& operator<<(ostream& cout, 类名 参数名)
- 重载左移运算符配合友元可以输出自定义数据类型

```cpp
//通过全局函数重载左移运算符
ostream& operator<<(ostream& cout, Person& p)
{
    cout << "姓名为" << p.name_ << " 年龄为" << p.age_;
    return cout;
}
```

### 3、递增运算符重载

作用：通过重载递增运算符，实现自己的整型数据，后置递增无法使用全局函数重载

- 前置递增：类名& operator++()
- 后置递增: 类名 & operator++(int)
- int 区分前置和后置
- 返回类的引用是为了对同一个数据一直进行递增

```cpp
//通过成员函数重载前置递增运算符
Person& operator++(void)
{
    this->age_++;
    return *this;
}

//通过全局函数重载前置递增运算符
Person& operator++(Person& p)
{
    p.age_++;
    return p;
}

//通过成员函数重载后置递增运算符
Person& operator++(int)
{
    this->age_++;
    return *this;
}
```

### 4、赋值运算符重载

如果使用未重载的赋值运算符，会对数据进行浅拷贝，从而带来堆区内存重复释放的问题

- 赋值运算符重载达到深拷贝的作用
- 重载之前需要判断是否有属性在堆区，如果有先释放干净，然后再深拷贝
- 语法：类名 & operator=(类名 & 参数名)
- 返回值为类名是为了连续赋值操作
- 赋值运算符无法通过全局函数进行重载

```cpp
//通过成员函数重载赋值运算符
Person& operator=(Person& p)
{
    if(this->age_ != nullptr & this->name_ != nullptr)
    {
        delete this->age_;
        delete this->name_;
        this->age_ = nullptr;
        this->name_ = nullptr;
    }

    this->name_ = new string(*p.name_);
    this->age_ = new int(*p.age_);

    return *this;
}

p3 = p2 = p1;
```

### 5、关系运算符重载

语法：bool operator==(类名 & 参数名)

```cpp
//通过成员函数重载等号运算符
bool operator==(Person& p)
{
    if(*this->name_ == *p.name_ & *this->age_ == *p.age_)
    {
        return true;
    }
    return false;
}

//通过全局函数重载等号运算符
bool operator==(Person& p1, Person& p2)
{
    if(*p1.name_ == *p2.name_ & *p1.age_ == *p2.age_)
    {
        return true;
    }
    return false;
}
```

### 6、函数调用运算符重载

由于重载后使用的方式很像函数调用，因此称为仿函数

```cpp
class MyPrint
{
public:
    void operator()(string str)
    {
        cout << str << endl;
    }
};

void test02()
{
    MyPrint Myfunc;
    Myfunc("hello world!");
}
```

## (五) 继承

### 1、基本语法

- 继承是指子类可以拥有父类的某些属性
- 基本语法：class 子类: 继承方式 父类
- 子类也称为派生类，父类也称为基类

```cpp
class Node01: public Node
```

### 2、继承方式

- 公共继承、私有继承、保护继承都只能继承父类中的保护成员和公有成员
  - 公有继承不会改变父类中成员的权限
  - 保护继承会将公有成员和保护成员都转变成保护权限
  - 私有继承会将公有成员和保护成员都转变成私有权限

### 3、继承中的对象模型

子类会继承父类所有的成员，只是私有成员会被隐藏，计算大小时会被算入

### 4、继承中构造和祈构顺序

子类继承父类后，当创建子类对象，也会调用父类的构造函数;父类的构造函数在子类的构造函数的前面调用，父类的析构函数在子类的析构函数的后面调用，即父类包含着子类。

### 5、继承同名成员的处理方式

- 当父类和子类中出现同名成员变量时，访问子类同名成员变量，直接访问即可；访问父类同名成员变量，需要加作用域
- 当父类与子类中出现同名成员函数时，访问子类同名成员函数，直接访问即可；父类中的所有成员函数隐藏，访问父类同名成员函数，需要加作用域
- 同名静态成员变量与同名成员变量处理方式一样

### 6、多继承语法

C++ 允许一个类继承多个类:

- class 子类：继承方式父类 1，继承方式父类 2...
- 多继承可能会引发父类中有同名成员出现，需要加作用域区分

### 7、菱形继承方法

- 菱形继承：两个派生类继承同一个基类，又有某一个类同时继承两个派生类，这种继承称为菱形继承，或者钻石继承
- 最后的类继承了两个派生类中的继承于基类的成员，调用这些成员导致出现了二义性，需要指明是哪一个的派生类
- 菱形继承导致出现了两份数据，利用虚继承可以解决菱形继承的问题，即在继承方式前面加 virtual 关键字，virtual 继承的类叫做虚基类，此时相当于只有一个数据

```cpp
class Animal { public: int age_; };
class Sheep: virtual public Animal {};
class Tuo: virtual public Animal {};
class SheepTuo: public Sheep, public Tuo {};

void test01()
{
    SheepTuo ST;

    ST.age_ = 18;

    cout << ST.age_ << endl;
}
```

## (六) 多态

### 1、多态的基本概念

1. 多态分为静态多态和动态多态:

   - 静态多态：函数重载和运算符重载属于静态多态，复用函数名
   - 动态多态：派生类和虚函数实现运行时多态

2. 静态多态与动态多态的区别为：

   - 静态多态函数的地址早绑定 - 编译阶段确定函数地址
   - 动态多态的函数地址晚绑定 - 运行阶段确定函数地址
   - 静态多态函数 +virtual 变成动态多态函数，实现地址晚绑定
   - 动态多态满足条件有必须有继承关系，子类重写父类的虚函数

3. 动态多态的调用：父类的指针或引用执行子类对象

```cpp
class Animal
{
public:
    int age_;

    virtual void Speak()//virtual实现地址晚绑定
    {
        cout << "动物在说话" << endl;
    }
};
class Cat: public Animal//有继承关系
{
public:
    void Speak()//子类方法重写
    {
        cout << "小猫在说话" << endl;
    }
};

class Dog: public Animal
{
public:
    void Speak()
    {
        cout << "小狗在说话" << endl;
    }
};

void doSpeak(Animal& animal)//父类的指针或引用执行子类对象
{
    animal.Speak();
}

void test02()
{
    Animal animal;
    Cat cat;
    Dog dog;

    doSpeak(animal);
    doSpeak(cat);
    doSpeak(dog);
}
```

### 2、多态的原理剖析

1. 当建立一个动态多态时，会在基类中出现一个 vfptr，即虚函数 (表)指针
2. 虚函数指针会指向一个虚函数表 vftable，表内记录虚函数的地址
3. 当子类重写父类的虚函数，子类的虚函数表内部会替换成子类的虚函数地址
4. 当父类的指针或者引用指向子类对象时，发生多态

### 3、纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容,因此可以将父类的虚函数改为纯虚函数

```cpp
// virtual 返回值类型 函数名 (参数列表) = 0;
virtual void Speak() = 0;
```

当类中有了纯虚函数，该类称为抽象类，抽象类特点：

- 无法实例化对象
- 子类必须重写类中的纯虚函数，否则也属于抽象类
- 当类是具有纯虚函数的基类时，谁分配给他空间，就调用谁的函数

```cpp
class Animal
{
public:
    int age_;

    virtual void Speak() = 0;
};

class Cat: public Animal
{
public:
    virtual void Speak()//重写纯虚函数时必须带上virtual关键字
    {
        cout << "小猫在说话" << endl;
    }
};

class Dog: public Animal
{
public:
    virtual void Speak()
    {
        cout << "小狗在说话" << endl;
    }
};

void doSpeak(Animal& animal)
{
    animal.Speak();
}

void test01()
{
    Cat cat;
    Dog dog;

    doSpeak(cat);
    doSpeak(dog);
}
```

### 4、虚析构和纯虚析构

多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用子类的析构代码，解决方式是将父类中的析构函数改为虚析构或纯虚析构

虚析构和纯虚析构共性：

- 可以解决父类指针释放子类对象
- 都需要有具体的函数实现

```cpp
class Animal
{
public:
    Animal()
    {
        cout << "Animal构造函数的调用" << endl;
    }

    virtual void Speak() = 0;//纯虚函数

    virtual ~Animal()//虚析构函数
    {
        cout << "Animal虚析构函数的调用" << endl;
    }

    string *name_;
};

class Cat: public Animal
{
public:
    Cat(string name)
    {
        name_ = new string(name);
        cout << "Cat构造函数的调用" << endl;
    }

    virtual void Speak()
    {
        cout << *this->name_ << "小猫在说话" << endl;
    }

    ~Cat()
    {
        if(name_ != nullptr)
        {
            delete name_;
            name_ = nullptr;
            cout << "Cat析构函数的调用" << endl;
        }
    }
};

void test01()
{
    Animal *animal = new Cat("Tom");
    animal->Speak();
    delete animal;
}
```

注：父类中的纯虚析构函数也需要内容，在类外写函数内容 类名:: 类名 ()

## (七) 文件操作

### 1、C++文件

1. C++ 中对文件操作需要包含头文件 \<fstream>
2. 文本文件：文件以文本的 ASCII 码形式存储在计算机中
3. 二进制文件：文件以文本的二进制形式存储在计算机中，用户一般不能直接读懂

### 2、文本文件

1. 写文本文件：

   1. 创建流对象 ofstream ofs;
   2. 打开文件 ofs.open("文件路径", 打开方式);
   3. 写数据 ofs << "写入的数据"
   4. 关闭文件 ofs.close();

2. 打开方式：

   - ios::in 为读文件而打开文件
   - ios::out 为写文件而打开文件
   - ios::ate 初始位置为文件尾
   - ios::app 追加方式写文件
   - ios::trunc 如果文件存在先删除，再创建
   - ios::binary 二进制方式
   - 打开方式可以配合使用，使用 | 操作符

3. 读文本文件:

   1. 创建流对象 ifstream ifs;
   2. 打开文件 ifs.open("文件路径", 打开方式);
   3. 判断文件是否打开成功 ifs.is_open()，返回值为布尔类型
   4. 读数据
   5. 关闭文件 ifs.close();

4. 读取方式：

   - while(ifs >> buffer) buffer 为 char \*类型
   - while(ifs.getline(buffer, sizeof(buffer)))
   - while(getline(ifs, buffer)) buffer 为 string 类型(好用)
   - while((c = ifs.get()) != EOF) c 为 char 类型

### 3、二进制文件

以二进制文件方式对文件进行读写操作需要指定打开方式为 ios::binary

1. 写文件：

   - 利用流对象调用成员函数 write
   - 函数原型:ostream& write(const char\* buffer, int len);

2. 读文件：

   - 利用流对象调用成员函数 read
   - 函数原型：istream& read(const char\* buffer, int len);

字符指针指向内存中一段存储空间，len 是读写的字节数

```cpp
//二进制文件
#include <fstream>
#include <iostream>
using namespace std;

class Person
{
public:
    string name_;
    int age_;
};

void test01()
{
    ofstream ofs;
    ofs.open("test02.txt", ios::out | ios::binary);
    Person p = {"张三", 18};
    ofs.write((const char*)&p, sizeof(p));
    ofs.close();
}

void test02()
{
    ifstream ifs;
    ifs.open("test02.txt", ios::in | ios::binary);
    Person p;
    if(ifs.is_open())
    {
        ifs.read((char *)&p, sizeof(p));
    }
    ifs.close();

    cout << "姓名：" << p.name_ << " 年龄：" << p.age_ << endl;
}

int main()
{
    test01();
    test02();

    return 0;
}
```

# 三、泛型编程

## (一) 模版

### 1、函数模版基本语法

C++ 提供两种模版机制，即函数模版和类模版

函数模版作用：建立一个通用函数，其函数返回值和形参类型可以不具体制定，用虚拟的类型来代表。

> 语法：template \<typename T>
> 函数声明或定义

- template 声明创建模版 typename 表示数据类型 T 通用的数据类型
- typename 可以换成 class

有两种方式来使用函数模版

- 自动类型推导: 直接调用模版函数
- 显示指定类型: 函数名 < 指定类型 >(参数)

### 2、函数模版注意事项

1. 自动类型推导，必须推导出一致的数据类型
2. 无论函数模版中通用数据类型 T 是否被调用，模版必须确定 T 的数据类型，才可以使用

### 3、函数模版与普通函数区别

1. 普通函数可以发生隐式类型转换
2. 函数模版使用自动类型推导不可以发生隐式类型转换
3. 函数模版使用显示指定类型可以发生隐式类型转换

### 4、函数模版与普通函数的调用规则

1. 如果函数模版和普通函数都可以实现，优先调用普通函数
2. 可以通过空模版参数列表来强制调用函数模版
3. 函数模版也可以发生重载
4. 如果函数模版可以产生更好的匹配，优先调用函数模版
5. 模版不是万能的，某些情况下需要模版重载来具体实现模版
6. 语法:template<> 函数（具体参数类型列表）
7. 开发中不要普通函数与函数模板一起使用，容易出现二义性

### 5、类模版

类模版创建语法:

- template<class T1, class T2, ...>

类模版使用:

- 在创建一个类的对象时，在类名后面加上模版的参数列表
- Person<string, int>

```cpp
template <class T1, class T2>
class Person
{
public:
    Person(T1 name, T2 age): name_(name), age_(age) {}

    void showPerson()
    {
        cout << this->name_ << this->age_ << endl;
    }

private:
    T1 name_;
    T2 age_;
};

void test01()
{
    Person<string, int> p("张三", 18);

    p.showPerson();
}
```

### 5、类模版与函数模版区别

类模版没有自动类型推导，但是在模版参数列表中可以有默认参数，默认参数只能放在在后面

### 6、类模版中成员函数的创建时机

- 普通类中的成员函数一开始就可以创建
- 类模版中的成员函数在调用时才会创建

### 7、类模版对象做函数参数

- 指定传入类型
- 参数模版化
- 整个类模版化

### 8、类模版与继承

- 当子类继承的父类是一个类模版时，子类在声明时要指定父类的类型
- 如果不指定，编译器会无法给子类分配内存
- 如果想灵活指定出父类类型。则子类也许变成类模版

### 9、类模版成员函数类外实现

- 无论是成员函数还是构造函数，在类外实现时，都需要先声明模版，然后再指定模版参数列表
- 语法: 作用域 < 模版参数列表 >:: 函数名 (函数参数列表)

```cpp
template <class T1, class T2>
void Person<T1, T2>::showPerson()
{
    cout << this->name_ << this->age_ << endl;
}
```

### 10、类模版分文件编写

- 类模版编写类外成员函数的声明和实现时，如果分文件编写，调用.h 文件编译器是无法获得成员函数的
- 为了获得成员函数，需要包含.cpp 文件，但不常用
- 另一种解决方式是将函数声明和实现写到.hpp 文件中，然后包含.hpp 文件

### 11、类模版友元

全局函数类内实现做友元函数，只需加关键字 friend
全局函数类外实现做友元函数，需要再次定义一个模版参数

```cpp
template <class T1, class T2>
class Person
{
    // //全局函数类内实现
    // friend void showPerson(Person<T1, T2>& p)
    // {
    //     cout << p.name_ << p.age_ << endl;
    // }

    //全局函数类外实现
    template <class U1, class U2>
    friend void showPerson(Person<U1, U2>& p);

public:
    Person(T1 name, T2 age): name_(name), age_(age) {}

private:
    T1 name_;
    T2 age_;
};

template <class U1, class U2>
void showPerson(Person<U1, U2>& p)
{
    cout << p.name_ << p.age_ << endl;
}

void test01()
{
    Person<string, int> p("张三", 18);

    showPerson(p);
}
```

## (二)STL

STL, 即标准模板库，从广义长可以分为容器、算法和迭代器三类

1. 容器分成序列式容器和关联式容器，容器的分类对应着数据结构中的线性表、栈列树等

2. 算法分成质变算法和非质变算法，区分是运算过程中是否更改区间内元素的内容

3. 迭代器：输入迭代器、输出迭代器、前向迭代器、双向迭代器、随机访问迭代器

> STL 六大组件：容器、算法、迭代器、仿函数、适配器和空间配置器
>
> - 容器：各种数据结构、如 vector、list、deque、set、map 等
> - 算法：各种算法，如 sort、find、copy、for_each 等
> - 迭代器：容器和算法之间通过迭代器进行无缝连接
> - 仿函数：行为类似函数，可作为算法的某种策略
> - 适配器：一种用来修饰容器或者仿函数或迭代器接口的东西
> - 空间配置器：负责空间的配置与管理

## (三) 容器

### 1、string 容器

#### 1.1 string 介绍

string 是一个类，类内部封装了 char* 管理该字符串，是一个 char* 型的容器

#### 1.2 string 构造函数

构造函数原型：

```cpp
string str1;//创建空字符串

string str2("hello world");//使用const char*类型的字符指针常量进行初始化

string str3(str2);//使用另一个string对象初始化string对象

string str4(3, 's');//使用n个字符进行初始化
```

#### 1.3 string 赋值

```cpp
str1 = "hello";
str2 = str1;//等号赋值

str3.assign("hello world");//字符指针常量赋值
str4.assign("hello world", 5);//把字符串前n个字符赋值给str
str5.assign(str4);//字符串赋值
str6.assign(4, 's');//n个字符赋值
```

#### 1.4 string 拼接

```cpp
str += "world";//字符串追加操作

str.append(const char* s);//参数为字符指针常量
```

#### 1.5 string 查找和替换

查找:

- find 从左至右 rfind 从右至左
- find(str, pos)
- 找到输出首元素下标，否则输出-1

替换：

- repalce(pos, n, str)
- 从 pos 开始 n 个字符替换为 str

#### 1.6 string 比较

```cpp
str1.compare(str2) //相等返回 0，大于返回 1，小于返回-1
```

#### 1.7 string 存取

使用 size 函数获取字符串长度

```cpp
string str = "hello world";

cout << str[1] << endl;
cout << str.at(1) << endl;
cout << str.size() << endl;
```

#### 1.8 string 插入和删除

```cpp
string str("hello world!");
cout << str[2] << endl;
cout << str.at(2) << endl;
cout << str.size() << endl;

str.insert(6, "python ");
cout << str << endl;

str.erase(6, 6);//(pos, n)从第pos开始删除n个字符
cout << str << endl;

string substr = str.substr(0, 5);//(pos, n)从第pos开始取出5个字符作为子字符串
cout << substr << endl;
```

### 2、vector 容器

#### 2.1 vector 介绍

使用 vector 容器需要包含 vector 的头文件

- vector<int>::iterator 迭代器类型
- v.begin(): 起始迭代器，指向容器中第一个元素的地址
- v.end(): 结束迭代器，指向容器中最后一个元素的下一个位置的地址

```cpp
void test01()
{
    vector<int> v;

    //尾插法向vector容器中插入元素
    v.push_back(10);
    v.push_back(20);
    v.push_back(30);
    v.push_back(40);
    v.push_back(50);

    //vector<int>::iterator vector容器的迭代器类型
    for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout << *it << ' ';
    }
    cout << endl;
}
```

#### 2.2 vector 遍历

遍历 vector 容器的三种方法

```cpp
void PrintNum(int num)
{
    cout << num << ' ';
}

//while遍历
vector<int>::iterator it = v.begin();
while (it != v.end())
{
    cout << *it << ' ';
    it++;
}
cout << endl;

//for遍历
for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
{
    cout << *it << ' ';
}
cout << endl;

//for_each遍历
for_each(v.begin(), v.end(), PrintNum);
```

注意：容器可以嵌套容器，如果需要输出小容器中的元素，需要两层 for 循环

#### 2.3 vector 构造函数

- vector<T> v1; //默认构造函数
- vector<T> v2(v1.begin(), v2.end()); //区间的方式构造容器，左闭右开
- vector<T> v3(v2); //拷贝构造函数
- vector<T> v4(10, 100); //向容器中添加 10 个 100

```cpp
vector<int> v1;
vector<int> v2(v1.begin(), v1.end());
vector<int> v3(v2);
vector<int> v4(10, 100);
```

#### 2.4 vector 赋值

```cpp
vector<int> v5;
v5 = v1;

vector<int> v6;
v6.assign(v1.begin(), v1.end());
```

#### 2.5 vector 大小

- empty() 判断容器是否为空,返回值为布尔类型
- capacity() 容器的容量
- size() 返回容器中元素的个数
- resize(int num); 重新指定容器的长度为 num，若容器变长，则以默认值填充新位置，如果容器变短，则超出部分删除
- resize(int num, T elem) 默认值为 elem

```cpp
vector<int> v7;
if(v7.empty())
{
    cout << "vector容器为空" << endl;
}
else
{
    cout << "vector容器不为空" << endl;
}

v7.resize(5);
v7.assign(v1.begin(), v1.end());

cout << "vector容器容量为" << v7.capacity() << endl;
cout << "vector容器大小为" << v7.size() << endl;
```

#### 2.6 vector 插入和删除

- push_back() 尾部插入元素
- pop_back() 删除最后一个元素
- insert(const_iterator pos, T ele) 迭代器指向位置插入元素 ele
- insert(const_iterator pos, int count, T ele) 迭代器指向位置 pos 插入 count 个元素 elem
- erase(const_iterator pos) 删除迭代器指向的元素
- erase(const_iterator start, const_iterator end) 删除迭代器从 start 到 end 的元素
- clear() 删除容器中所有元素

```cpp
vector<int> v1;

v1.push_back(10);
v1.push_back(20);
PrintVector(v1);

v1.pop_back();
PrintVector(v1);
v1.insert(v1.begin() + 1, 20);
PrintVector(v1);

v1.insert(v1.end(), 10, 30);
PrintVector(v1);

v1.erase(v1.begin() + 1);
PrintVector(v1);

v1.erase(v1.begin() + 1, v1.end());
PrintVector(v1);

v1.clear();
PrintVector(v1);

if(v1.empty())
{
    cout << "容器为空";
}
```

#### 2.7 vector 数据存取

- at(int index) 取出索引 Index 的元素
- operator[index]返回索引 Index 的元素
- front() 和 back() 返回第一个和最后一个元素

```cpp
cout << v1.at(7) << endl;
cout << v1[4] << endl;
cout << v1.front() << endl;
cout << v1.back() << endl;
```

#### 2.8 vector 互换容器

- v1.swap(v2) 将容器 v1 和 v2 本身的元素互换

#### 2.9 vector 预留空间

- reserve(int len) 容器预留 len 个元素长度，预留位置不初始化, 元素不可访问

```cpp
v.reverse(10);//预留10个元素位
```

### 3、deque 容器

deque 容器：双端数组，可以对头部进行插入和删除操作

```cpp
deque<int> d;
d.push_front(20);
d.push_front(10);//插入头部元素
d.push_back(30);
d.push_back(40);
d.push_back(50);

for (deque<int>::iterator it = d.begin(); it != d.end(); it++)
{
    cout << *it << ' ';
}


d.pop_front();//删除头部元素
cout << endl;

for (deque<int>::iterator it = d.begin(); it != d.end(); it++)
{
    cout << *it << ' ';
}
cout << endl;

cout << d.front() << ' ' << d.back() << endl;//取出头尾元素

sort(d.begin(), d.end(), [](int a, int b) { return a > b; });
for (deque<int>::iterator it = d.begin(); it != d.end(); it++)
{
    cout << *it << ' ';
}
cout << endl;
```

### 4、stack 容器

stack 是一种先进后出的数据结构，他只有一个出口，栈中只有顶端的元素才能被外界使用，因此栈不允许有遍历行为

栈的常见操作：

- top() 返回栈顶元素
- pop() 出栈
- push() 入栈

```cpp
stack<int> s;

s.push(10);
s.push(20);
s.push(30);
s.push(40);

if(s.empty())
{
    cout << "栈为空" << endl;
}
else
{
    cout << "栈不为空" << endl;
}
cout << "栈的大小为" << s.size() << endl;
cout << "栈顶元素为" << s.top() << endl;

s.pop();

stack<int> s2;
s2.push(10);

s.swap(s2);
cout << s.size() << " " << s2.size() << endl;
```

### 5、queue 容器

queue 是一种先进先出的数据结构

queue 常见操作：

- pop() 队头元素出队列
- push() 队尾元素入队列
- back() 返回队尾元素
- front() 返回队头元素
- empty() 判断是否为空
- size() 计算队列大小
- swap() 交换两个队列

```cpp
queue<int> q;
q.push(10);
q.push(20);
q.push(30);
q.push(40);

if(q.empty())
{
    cout << "队列为空" << endl;
}
else
{
    cout << "队列不为空" << endl;
}
cout << "队列的大小为" << q.size() << endl;
cout << "队头元素为" << q.front() << endl;
cout << "队尾元素为" << q.back() << endl;

q.pop();
```

### 6、list 容器

STL 中的链表是一个双向循环链表,常见操作有

```cpp
//list有swap、sort、erase、insert等操作
list<int> l;

l.push_back(20);
l.push_front(10);
l.push_back(30);
PrintList(l);

l.pop_front();
PrintList(l);

l.reverse();
PrintList(l);
```

### 7、set 容器

#### 7.1 set 简介

set 容器：所有元素都会在插入时自动被排序

set/multiset 属于关联式容器，底层结构是用二叉树实现

set 和 multiset 区别：

- set 不允许容器中出现重复的元素，类似集合，
- multiset 可以出现重复

#### 7.2 set 操作

```cpp
set<int> s;

s.insert(20);
s.insert(10);
s.insert(90);
s.insert(70);
PrintSet(s);

s.erase(70);
PrintSet(s);

//查找元素，若存在，则返回对应迭代器；若不存在，则返回元素个数
cout << *s.find(20) << endl;
cout << *s.find(70) << endl;

//由于set不能重复，故返回结果只能为0或1
cout << s.count(90) << endl;

//insert返回值为pair<set<T>::iterator, bool>,第一个为元素迭代器，第二个为元素是否插入成功的布尔值
if(s.insert(10).second)
{
    cout << "插入成功" << endl;
}
else
{
    cout << "插入失败" << endl;
}

s.clear();
PrintSet(s);

if(s.empty())
{
    cout << "集合为空" << endl;
}
else
{
    cout << "集合不为空" << endl;
}
```

注：multiset 不会检测数据，因此可以重复插入

#### 7.3 pair 对组数据

pair 对组创建: 成对出现的数据, 利用对组可以返回两个数据

pair 构造函数：

- pair<type, type> p(value1, value2);
- pair<type, type> p = make_pair(value, value);

```cpp
pair<int, bool> p1(10, true);
pair<int, bool> p2 = make_pair(10, false);
```

#### 7.4 set 排序

内置类型自定义 set 排序方式, 即创建一个比较的类，类内重载函数调用运算符()，然后将类名传入 set 创建时的尖括号中

```cpp
class Compare
{
public:
    bool operator()(int a, int b) const { return a > b; }
};

set<int, Compare> reverse_s;
reverse_s.insert(23);
reverse_s.insert(567);
reverse_s.insert(44);
reverse_s.insert(9);
PrintSet(reverse_s);
```

set 中存放自定义数据类型都需要指定自定义排序类型

```cpp
set<Person, Person_compare> s;
```

### 8、map 容器

map 中所有的元素都是 pair，其中第一个元素为 key，即键值，起到索引的作用；第二个元素为 value，即值

- map/multimap 属于关联式容器, 底层结构是用二叉树实现的。
- 所有元素都会根据元素的键值自动排序
- map 不可以含有重复 key 元素;multimap 可以

```cpp
#include <iostream>
#include <string>
#include <map>
using namespace std;

void PrintMap(map<int, string>& m)
{
    for (map<int, string>::iterator it = m.begin(); it != m.end(); it++)
    {
        cout << "key is " << (*it).first << " value is " << it->second << endl;
    }
    cout << endl;
}

void test01()
{
    map<int, string> m;

    m.insert(pair<int, string>(10, "cat"));
    m.insert(pair<int, string>(20, "dog"));
    m.insert(pair<int, string>(40, "pig"));
    m.insert(pair<int, string>(30, "person"));//auto sort with key

    PrintMap(m);

    cout << "The value whose key is 20 is " << m.find(20)->second << endl;
    cout << "The couter for 30 is " << m.count(30) << endl;

}

int main()
{
    test01();

    return 0;
}
```

使用仿函数进指定排序规则

```cpp
class MySort
{
public:
    bool operator()(const int& v1, const int& v2) const
    {
        return v1 > v2;
    }
};
//注意仿函数类型为常函数
```

### 9、函数对象

#### 9.1 概念

重载函数调用运算符的类，其对象称为函数对象

- 函数对象在使用时，可以像普通函数那样调用，可以有参数，可以有返回值
- 函数对象超出普通函数的概念，函数对象可以有自己的状态
- 函数对象可以作为参数传递

#### 9.2 谓词

谓词概念: 返回 bool 类型的仿函数称为谓词

- 如果 operator() 接受一个参数，那么叫做一元谓词
- 如果 operator() 接受两个参数，那么叫做二元谓词

```cpp
class Condition
{
public:
    bool operator()(int val) const { return val > 5; }
};
```

#### 9.3 内置函数对象

内置函数对象: 算术仿函数、关系仿函数、逻辑仿函数

1. 算术仿函数

- plus<T> p;\\加法仿函数,为二元谓词
- negate<T> n;\\取反仿函数,为一元谓词

2. 关系仿函数

- 关系仿函数：等于、不等于、大于、大于等于、小于、小于等于
- 若作为参数传递，则写为 greater<int>()
- 用于指定排序规则

3. 逻辑仿函数

- logical_and
- logical_or
- logical_not

# 四、算法

## (一) 常见遍历算法

### 1、for_each

- 参数为迭代器 begin、迭代器 end、函数
- 函数为普通函数或仿函数
- 普通函数传入函数名
- 仿函数传入函数名加括号

```cpp
//普通函数
void Print01(int val)
{
    cout << val << ' ';
}

//仿函数
class Print02
{
public:
    void operator()(int val) { cout << val << ' '; }
};
```

### 2、transform

transform(iterator begin1, iterator end1, iterator begin2, func)：

- begin1 源容器开始迭代器
- end1 源容器结束迭代器
- begin2 目标容器开始迭代器
- func 函数或函数对象

注：使用之前需要开辟空间

## (二) 常见查找算法

### 1、find

find(iterator begin, iterator end, value):

- begin 开始迭代器
- end 结束迭代器
- value 查找的元素

> 查找指定元素，返回指定元素的迭代器，找不到返回结束迭代器,且只支持查找与值相等的元素，而无法进行条件判断

### 2、find_if

find_if(iterator begin, iterator end, Pred):

- begin 开始迭代器
- end 结束迭代器
- Pred 函数或者谓词

> 按值查找元素，找到返回指定位置迭代器、找不到返回结束迭代器位置

### 3、adjacent_find

adjacent_find(iterator begin, iterator end):

- begin 开始迭代器
- end 结束迭代器

> 查找相邻重复元素，返回相邻元素的第一个位置的迭代器，找不到返回结束迭代器

### 4、binary_search

binary_search(iterator begin, iterator end, value):

- begin 开始迭代器
- end 结束迭代器
- value 要查找的元素
- 查找指定元素是否存在
- 返回类型为布尔值
- 在无序序列不可用

### 5、count

count(iterator begin, iterator end, value)：

- begin 开始迭代器
- end 结束迭代器
- 统计元素个数

### 6、count_if

count_if(iterator begin, iterator end, func):

- begin 开始迭代器
- end 结束迭代器
- func 函数对象
- 统计符合条件函数的元素个数

## (三) 常见排序算法

### 1、sort

sort(iterator begin, iterator end, Pred):

- begin 开始迭代器
- end 结束迭代器
- Pred 仿函数或普通函数
- 按指定条件排序

### 2、random_shuffle

random_shuffle(iterator begin, iterator end):

- begin 开始迭代器
- end 结束迭代器
- 指定范围内元素随机调整次序

### 3、merge

merge(iterator begin1, iterator end1, iterator begin2, iterator end2, iterator destination.begin)

- 合并两个容器并排序, 放在目标容器中
- 其中两个容器必须有序且排序类型一致

### 4、reverse

reverse(iterator begin, iterator end)

- 反转指定范围内的元素

## (四) 常见拷贝和替换算法

### 1、copy

copy(iterator begin, iterator end, iterator destination.begin):

- 拷贝某一容器到 destination 容器中
- 新容器需要提前开辟空间

### 2、replace

replace(iterator begin, iterator end, oldvalue, newvalue):

- 将 oldvalue 替换成 newvalue

### 3、replace_if

replace_if(iterator begin, iterator end, Pred, newvalue):

- begin 开始迭代器
- end 结束迭代器
- Pred 一元谓词
- 按条件替换元素，满足条件的替换成指定元素

### 4、swap

swap(container c1, container c2):

- container 容器
- 互换两个容器的元素

## (五) 常见算术生成算法

### 1、accumulate

accumulate(iterator begin, iterator end, value):

- 计算区间内容器元素累计总和
- value 累加的起始值
- 需要包含头文件 numeric

### 2、fill

fill(iterator begin, iterator end, value)

- 向容器中填充元素

## (六) 常见集合算法

### 1、set_intersection

set_intersection(iterator begin1, iterator end1, iterator begin2, iterator end2, iterator destination):

- 求两个容器的交集，原容器必须为有序的序列
- 结果存放到目标容器中
- 目标容器需要提前开辟空间
- 返回值为交集的结束迭代器

### 2、set_union

set_union(iterator begin1, iterator end1, iterator begin2, iterator end2, iterator destination):

- 求两个容器的并集，原容器必须为有序的序列
- 结果存放到目标容器中
- 目标容器需要提前开辟空间
- 返回值为并集的结束迭代器

### 3、set_difference

set_difference(iterator begin1, iterator end1, iterator begin2, iterator end2, iterator destination):

- 求两个容器的差集，原容器必须为有序的序列
- 结果存放到目标容器中
- 目标容器需要提前开辟空间
- 返回值为差集的结束迭代器

# 五、C++常用库

## （一）Eigen

### 1、Eigen 库介绍

Eigen 是用于线性代数计算的高效 C++模板库，广用于科学计算、机器人学、计算机视觉等领域。Eigen 提供了矩阵和向量的表示和运算，并支持相关操作，如矩阵分解、特征值计算以及奇异值分解等

#### 1.1 矩阵的创建

# 六、扩展知识

## （一）gcc 和 g++的区别

gcc 和 g++都是 GNU Compiler Collection 的缩写，是 GNU 开发的编译器套件，主要用于 C、C++、Objective-C、Java 等语言的编译。

### 1、文件后缀名处理

> gcc: 如果文件扩展名是.c, gcc 会将其视为 C 代码。如果文件扩展名是.cpp 等, gcc 会尝试按照 C++代码进行编译，但必须手动链接 C++库
> g++: 无论文件扩展名是.c、.cpp 等都视为 C++代码

### 2、编译选项

> gcc: 默认情况下, gcc 不会自动链接 C++库
> g++: 默认会处理所有文件为 C++

## （二）智能指针

### 1、基本介绍

在 C++中，智能指针是一种管理动态内存的工具，通过 RALL 机制，实现自动管理堆内存的分配和释放，避免内存泄漏和悬空指针等问题，头文件为\<memory>

C++11 标准中引入了三种常用的智能指针：

- std::unique_ptr
- std::shared_ptr
- std::weak_ptr

### 2、std::unique_ptr

特点：某一时刻只能有一个智能指针指向该对象，具有独占式的所有权，但可使用 move 函数转移所有权

#### 2.1 声明和初始化

可以使用 std::make_unique 或直接使用 new 进行初始化

```cpp
#include <iostream>
#include <memory>

class MyClass
{
public:
    MyClass() { std::cout << "MyClass构造函数的调用" << std::endl; }
    ~MyClass() { std::cout << "MyClass析构函数的调用" << std::endl; }
    void doSomething() { std::cout << "Doing something" << std::endl; }
};

int main()
{
    //使用make_unique创建MyClass类型的unique_ptr对象
    std::unique_ptr<MyClass> ptr1 = std::make_unique<MyClass>();

    //使用new创建MyClass类型的unique_ptr对象
    std::unique_ptr<MyClass> ptr2(new MyClass());

    //调用类的成员函数
    ptr1->doSomething();
    ptr2->doSomething();

    //不需要手动delete，unique_ptr会自动释放内存

    return 0;
}
```

输出：

```
MyClass构造函数的调用
MyClass构造函数的调用
Doing something
Doing something
MyClass析构函数的调用
MyClass析构函数的调用
```

#### 2.2 转移所有权

由于 unique_ptr 的独占性，它不能被拷贝，但可以转移所有权

```cpp
#include <iostream>
#include <memory>

class MyClass
{
public:
    MyClass() { std::cout << "MyClass构造函数的调用" << std::endl; }
    ~MyClass() { std::cout << "MyClass析构函数的调用" << std::endl; }
};

int main()
{
    //使用std::make_unique创建MyClass类型的std::unique_ptr对象
    std::unique_ptr<MyClass> ptr1 = std::make_unique<MyClass>();

    //使用std::move转移所有权
    std::unique_ptr<MyClass> ptr2 = std::move(ptr1);

    //ptr1现在为空
    if(ptr1 == nullptr)
    {
        std::cout << "ptr1 is null\n";
    }

    //不需要手动delete，unique_ptr会自动释放内存

    return 0;
}
```

输出：

```
MyClass构造函数的调用
ptr1 is null
MyClass析构函数的调用
```

#### 2.3 释放内存

- release: 放弃 unique_ptr 对象的所有权，并返回原始指针
- reset: 销毁当前管理的对象并可以重新管理新的 unique_ptr 对象

```cpp
#include <iostream>
#include <memory>

class MyClass
{
public:
    MyClass() { std::cout << "MyClass构造函数的调用" << std::endl; }
    ~MyClass() { std::cout << "MyClass析构函数的调用" << std::endl; }
};

int main()
{
    std::unique_ptr<MyClass> ptr = std::make_unique<MyClass>();

    //释放所有权，ptr不再管理该对象
    MyClass* new_ptr = ptr.release();
    std::cout << "ptr所有权被释放, 成为原始指针\n";

    //必须手动delete原始指针
    delete new_ptr;

    //重置unique_ptr，指向一个新的对象
    ptr.reset(new MyClass());

    // 自动释放新的对象

    return 0;
}
```

输出：

```
MyClass构造函数的调用
ptr所有权被释放, 成为原始指针
MyClass析构函数的调用
MyClass构造函数的调用
MyClass析构函数的调用
```

### 3、std::shared_ptr

shared_ptr 可以同时指向同一个对象，该对象会在最后一个 shared_ptr 对象销毁时自动释放内存，避免手动释放管理内存。

- 共享所有权：同一对象可以被多个 shared_ptr 拥有，shared_ptr 拥有一个引用次数，当引用次数变为 0 时，所管理的对象会被销毁
- 线程安全的引用次数：不同线程可以安全地共享同一对象的 shared_ptr

#### 3.1 声明和初始化

可以使用 std::make_shared 或 new 初始化对象

```cpp
#include <iostream>
#include <memory>

class MyClass
{
public:
    MyClass() { std::cout << "MyClass构造函数的调用" << std::endl; }
    ~MyClass() { std::cout << "MyClass析构函数的调用" << std::endl; }
    void doSomething() { std::cout << "Doing something!" << std::endl; }
};

int main()
{
    //使用make_shared初始化shared_ptr对象
    std::shared_ptr<MyClass> ptr1 = std::make_shared<MyClass>();

    //调用成员函数
    ptr1->doSomething();

    //输出引用次数
    std::cout << "引用次数为" << ptr1.use_count() << std::endl;

    //将ptr1赋值拷贝给ptr2
    std::shared_ptr<MyClass> ptr2 = ptr1;

    //输出引用次数
    std::cout << "引用次数为" << ptr1.use_count() << std::endl;

    //使用new初始化shared_ptr对象
    std::shared_ptr<MyClass> ptr3(new MyClass());

    //调用成员函数
    ptr3->doSomething();

    return 0;
}
```

注：use_count 函数的返回值为指向同一个对象的不同 shared_ptr 对象的个数

#### 3.2 转移所有权

虽然 shared_ptr 具有共享所有权的特点，但它仍然可以使用 move 转移所有权

#### 3.3 std::shared_ptr 和 std::weak_ptr

当 shared_ptr 的引用次数增加时，管理的对象会一直存在，有时可能需要一种不影响引用次数的方式来观察对象，即 std::weak_ptr 的用法

```cpp
#include <iostream>
#include <memory>

class MyClass
{
public:
    MyClass() { std::cout << "MyClass构造函数的调用" << std::endl; }
    ~MyClass() { std::cout << "MyClass析构函数的调用" << std::endl; }
    void doSomething() { std::cout << "Doing something!" << std::endl; }
};

int main()
{
    //使用make_shared初始化shared_ptr对象
    std::shared_ptr<MyClass> ptr1 = std::make_shared<MyClass>();
    std::weak_ptr<MyClass> weakptr = ptr1;

    //输出引用次数
    std::cout << "引用次数为" << ptr1.use_count() << std::endl;

    //检查std::weak_ptr是否有效
    if(auto sharedptr = weakptr.lock())
    {
        std::cout << "共享指针对象存在\n";
    }

    //手动释放shared_ptr对象
    ptr1.reset();

    //共享指针已释放，weak_ptr无法锁定对象
    if(auto sharedptr = weakptr.lock())
    {
        std::cout << "共享指针对象存在\n";
    }
    else
    {
        std::cout << "共享指针对象不存在\n";
    }

    return 0;
}
```

#### 3.4 自定义删除器

std::shared_ptr 可以自定义删除器

```cpp
#include <iostream>
#include <memory>

class MyClass
{
public:
    MyClass() { std::cout << "MyClass构造函数的调用" << std::endl; }
    ~MyClass() { std::cout << "MyClass析构函数的调用" << std::endl; }
    void doSomething() { std::cout << "Doing something!" << std::endl; }
};

//自定义删除器
void customDeleter(MyClass* p)
{
    std::cout << "自定义删除器的调用\n";
    delete p;
}

int main()
{
    std::shared_ptr<MyClass> ptr1(new MyClass(), customDeleter);

    return 0;
}
```

#### 3.5 循环引用问题

若两个 shared_ptr 对象互相持有对方, 会造成循环引用, 导致内存无法释放, weak_ptr 可以打破这种循环引用

```cpp
//该C++文件内存并未释放
#include <iostream>
#include <memory>

class B;  //前向声明

class A {
public:
    std::shared_ptr<B> ptrB;

    ~A() { std::cout << "A的析构函数调用\n"; }
};

class B {
public:
    std::shared_ptr<A> ptrA;

    ~B() { std::cout << "B的析构函数调用\n"; }
};

int main()
{
    std::shared_ptr<A> a = std::make_shared<A>();
    std::shared_ptr<B> b = std::make_shared<B>();

    //循环引用，A和B永远不会被析构
    a->ptrB = b;
    b->ptrA = a;

    //a和b的引用次数均为2
    std::cout << "a的引用次数为" << a.use_count() << std::endl;
    std::cout << "b的引用次数为" << b.use_count() << std::endl;

    //输出未自动调用析构函数
    std::cout << "Exiting main\n";

    return 0;
}
```

解决方法是将 A 或 B 内的共享指针对象改为 weak_ptr 类型，使得引用次数不得增加
