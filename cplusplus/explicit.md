# c++ Explicit 关键字

`explicit`关键字有两个用途：

1. 指定构造函数或转换函数 (C++11起)为显式, 即它不能用于隐式转换和复制初始化。
2. 可以与常量表达式一同使用. 当该常量表达式为 true 才为显式转换(C++20起)。

下面分别记录这两个用途。

### 1. 将构造函数标记为显式

C++中的`explicit`关键字通常用来将构造函数标记为显式类型转换，即在创建对象的时候不能进行隐式类型转换。

可以通过一个例子来理解：

```c++
// CPP Program to illustrate default
// constructor without 'explicit'
// keyword
#include <iostream>
using namespace std;
  
class Complex {
private:
    double real;
    double imag;
  
public:
    // Default constructor
    Complex(double r = 0.0, double i = 0.0)
        : real(r)
        , imag(i)
    {
    }
  
    // A method to compare two Complex numbers
    bool operator==(Complex rhs)
    {
        return (real == rhs.real && imag == rhs.imag)
                   ? true
                   : false;
    }
};
  
// Driver Code
int main()
{
    // a Complex object
    Complex com1(3.0, 0.0);
  
    if (com1 == 3.0)
        cout << "Same";
    else
        cout << "Not Same";
    return 0;
}
```

**Output**

```
Same
```

在上面的例子中，只传给构造函数一个参数，然后，这个构造函数就变成转换构造函数，因为转换构造函数允许将单个参数转换为正在构造的类。

我们可以避免这种隐式转换，因为它们可能会导致意外的结果。我们可以通过`explicit`关键字使构造函数变成显式。例如，如果我们尝试使用以下带有`explicit`关键字的构造函数，就会出现编译错误。

```c++
// CPP Program to illustrate default
// constructor with
// 'explicit' keyword
#include <iostream>
using namespace std;
  
class Complex {
private:
    double real;
    double imag;
  
public:
    // Default constructor
    explicit Complex(double r = 0.0, double i = 0.0)
        : real(r)
        , imag(i)
    {
    }
  
    // A method to compare two Complex numbers
    bool operator==(Complex rhs)
    {
        return (real == rhs.real && imag == rhs.imag)
                   ? true
                   : false;
    }
};
  
// Driver Code
int main()
{
    // a Complex object
    Complex com1(3.0, 0.0);
  
    if (com1 == 3.0)
        cout << "Same";
    else
        cout << "Not Same";
    return 0;
}
```

**Output**

```
Compiler Error : no match for 'operator==' in 'com1 == 3.0e+0'
```

我们仍然可以将`double`类型转换为复数，但现在我们必须显式地进行类型转换。例如，以下程序运行良好。

```c++
// CPP Program to illustrate 
// default constructor with
// 'explicit' keyword
#include <iostream>
using namespace std;
  
class Complex {
private:
    double real;
    double imag;
  
public:
    // Default constructor
    explicit Complex(double r = 0.0, double i = 0.0)
        : real(r)
        , imag(i)
    {
    }
  
    // A method to compare two Complex numbers
    bool operator==(Complex rhs)
    {
        return (real == rhs.real && imag == rhs.imag)
                   ? true
                   : false;
    }
};
  
// Driver Code
int main()
{
    // a Complex object
    Complex com1(3.0, 0.0);
  
    if (com1 == (Complex)3.0)
        cout << "Same";
    else
        cout << "Not Same";
    return 0;
}
```

**Output**

```
Same
```

### 2. 与常量表达式一同使用

`explicit`关键字可以与常量表达式一起使用。但是，如果该常量表达式的计算结果为`true`，此时构造函数是显式的。举个例子：

```c++
constexpr bool ENABLE_EXPLICIT = false;

struct Foo {
    explicit(ENABLE_EXPLICIT)
    Foo(int) {}
};

Foo a = 1;
```

以上代码可以正常编译。但是如果把变量`ENABLE_EXPLICIT`改为`true`。在`clang-10.0.0`就会得到以下错误：

```
error: no viable conversion from 'int' to 'Foo'
note: explicit constructor is not a candidate (explicit specifier evaluates to true)
```

所以与常量表达式一起使用时，会根据常量表达式的值而出现不同的结果。

### 参考

[C++ explicit 关键字 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/52152355)

[C++ explicit的作用 - 原来... - 博客园 (cnblogs.com)](https://www.cnblogs.com/this-543273659/archive/2011/08/02/2124596.html)

[C++ explicit 关键字 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/52152355)

[Use of explicit keyword in C++ - GeeksforGeeks](https://www.geeksforgeeks.org/use-of-explicit-keyword-in-cpp/)

[Let's try C++20 | explicit(bool) - DEV Community](https://dev.to/pgradot/let-s-try-c-20-explicit-bool-7a)

