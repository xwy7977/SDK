# static_assert

## 概述

**什么是断言（assertion）**

在程序设计中，断言（assertion）是一种放在程序中的一阶逻辑（一个结果为真或假的逻辑判断式），目的是为了标示与验证程序开发者预期的结果，当程序执行到断言的位置时，对应的断言应该为真。若断言不为真时，程序会中止执行，并给出错误消息。

**什么是静态断言（static assertion）**

静态断言（static assertion）是在编译时（区别于运行时）进行检查的断言。static_assert就是静态断言。

## 语法

```CPP
static_assert( bool-constexpr , message )		// (since C++11)
static_assert( bool-constexpr )		            // (since C++17)
```

- `bool-constexpr`是一个可以转换为`bool`类型的常量表达式，如果表达式的值为0（false），会显示信息`message`，并且停止编译，如果表达式非0（true），那么什么也不做，继续编译。
- `message`在常量表达式为0的时候显示，这个参数是可选的。

## 例子

```CPP
// CPP code to demonstrate 
// static assertion using static_assert 
#include <iostream> 
using namespace std; 

template <class T, int Size> 
class Vector { 
	// Compile time assertion to check if 
	// the size of the vector is greater than 
	// 3 or not. If any vector is declared whose 
	// size is less than 4, the assertion will fail 
	static_assert(Size > 3, "Vector size is too small!"); 

	T m_values[Size]; 
}; 

int main() 
{ 
	Vector<int, 4> four; // This will work 
	Vector<short, 2> two; // This will fail 

	return 0; 
} 
```

**Output**

```
error: static assertion failed: Vector size is too small!
```

**解释**

在上面的代码中，我们创建了一个名叫`Vector`的模板类，我们不允许vector的大小小于4。因此，在模板内部，我们使用了`static_assert`来检查`size>3`是否满足，如果不满足就会输出错误信息。

## 注意

- 在C语言中，C23才可以使用`static_assert`。
- 在C++中，C++11以后可以使用`static_assert( bool-constexpr , message )`，C++17以后可以使用`static_assert( bool-constexpr )`。

## 参考

[static_assert declaration (since C++11) - cppreference.com](https://en.cppreference.com/w/cpp/language/static_assert)

[Understanding static_assert in C++ 11 - GeeksforGeeks](https://www.geeksforgeeks.org/understanding-static_assert-c-11/)

[static_assert | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/cpp/static-assert?view=msvc-170)

[Static assertion (since C11) - cppreference.com](https://en.cppreference.com/w/c/language/_Static_assert)

[断言 (程序) - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E6%96%B7%E8%A8%80_(%E7%A8%8B%E5%BC%8F))

[assert.h (GNU Gnulib)](https://www.gnu.org/software/gnulib/manual/html_node/assert_002eh.html)