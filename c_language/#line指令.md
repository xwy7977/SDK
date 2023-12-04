# #line指令

## 概述

程序在进行编译的时候，可能会发生错误。编译器会给我们提供一些错误信息，包括错误发生在哪一个文件，发生错误的行号，以方便我们精准的定位并修正错误。

使用`#line`指令可以指示预处理器修改编译器报告给我们的行号和文件名。

## 语法

```C
#line digit-sequence ["filename"]
```

其中，文件名是可选的。

## Example 1

```C++
// C++ program to demonstrate line control
#include <iostream>
using namespace std;

// Driver Code
int main()
{
	cout << "START" << endl;

	cout << __LINE__ << " "
		<< __FILE__ << endl;

#line 67 "Binod.cpp"

	cout << __LINE__
		<< " " << __FILE__
		<< endl; // (68)

	// This will apply continuously (72)
	cout << __LINE__ << endl; // (73)
}
```

**Output**

```
START
10 test.cpp
68 Binod.cpp
73
```

## Example 2

```C
// line_directive.cpp
// Compile by using: cl /W4 /EHsc line_directive.cpp
#include <stdio.h>

int main()
{
    printf( "This code is on line %d, in file %s\n", __LINE__, __FILE__ );
#line 10
    printf( "This code is on line %d, in file %s\n", __LINE__, __FILE__ );
#line 20 "hello.cpp"
    printf( "This code is on line %d, in file %s\n", __LINE__, __FILE__ );
    printf( "This code is on line %d, in file %s\n", __LINE__, __FILE__ );
}
```

**Output**

```
This code is on line 7, in file line_directive.cpp
This code is on line 10, in file line_directive.cpp
This code is on line 20, in file hello.cpp
This code is on line 21, in file hello.cpp
```

## 解释

- 在验证`#line`指令的时候，我们使用了两个内置的宏定义：
	- __LINE__：指出源代码的行号。
	- __FILE__：指出源代码的文件名。
- `#line`指令中的行号是下一行代码的行号，而不是这个指令的行号。源代码中`#line`指令下方的代码的行号都会在此基础上递增。
- `#line __LINE__`是未定义的，不要这么使用。

## 参考

https://en.cppreference.com/w/c/preprocessor/line

https://www.geeksforgeeks.org/line-control-directive/

https://learn.microsoft.com/en-us/cpp/preprocessor/hash-line-directive-c-cpp?view=msvc-170