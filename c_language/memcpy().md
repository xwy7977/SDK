# memcpy()

## 概述

C/C++ 中的`memcpy()`函数通常用来将内存块中的数据从一个地方复制到另一个地方。不同于其他的内存复制函数，`memcpy()`以字节为单位去拷贝数据而不管数据的类型，即此函数只关心需要拷贝多少个字节的数据，而不关心这些字节到底存储了什么类型的数据。

在C语言中，这个函数包含在头文件`<string.h>`中。在C++中，包含在`<cstring>`头文件中。

## 语法

```C
void* memcpy( void* dest, const void* src, std::size_t count );
```

**参数**
- dest：一个指针，指向被复制的数据将要被存储的内存地址。
- src：一个指针，指向将要被复制的数据的内存地址。
- count：被复制的字节数。

**返回值**

- dest：参数dest作为返回值。

## Example 1

```C
// C program to demonstrate working of memcpy
#include <stdio.h>
#include <string.h>

int main()
{
	char str1[] = "Geeks";
	char str2[] = "Quiz";

	puts("str1 before memcpy ");
	puts(str1);

	// Copies contents of str2 to str1
	memcpy(str1, str2, sizeof(str2));

	puts("\nstr1 after memcpy ");
	puts(str1);

	return 0;
}
```

**Output**

```
str1 before memcpy 
Geeks

str1 after memcpy 
Quiz
```

## Example 2

```C++
#include <cstdint>
#include <cstring>
#include <iostream>
 
int main()
{
    // simple usage
    char source[] = "once upon a daydream...", dest[4];
    std::memcpy(dest, source, sizeof dest);
    std::cout << "dest[4] = {";
    for (int n{}; char c : dest)
        std::cout << (n++ ? ", " : "") << '\'' << c << "'";
    std::cout << "};\n";
 
    // reinterpreting
    double d = 0.1;
//  std::int64_t n = *reinterpret_cast<std::int64_t*>(&d); // aliasing violation
    std::int64_t n;
    std::memcpy(&n, &d, sizeof d); // OK
 
    std::cout << std::hexfloat << d << " is " << std::hex << n
              << " as a std::int64_t\n" << std::dec;
 
    // object creation in destination buffer
    struct S
    {
        int x{42};
        void print() const { std::cout << '{' << x << "}\n"; }
    } s;
    alignas(S) char buf[sizeof(S)];
    S* ps = new (buf) S; // placement new
    std::memcpy(ps, &s, sizeof s);
    ps->print();
}
```

**Output**

```
dest[4] = {'o', 'n', 'c', 'e'};
0x1.999999999999ap-4 is 3fb999999999999a as a std::int64_t
{42}
```

## 解释

- `memcpy()`不检查内存溢出或者`\0`。
- 如果源地址和目的地址有重叠会导致未定义行为（undefined behaviour），比如源地址是100，目的地址是102,长度是10,就会产生重叠。

## 参考

https://en.cppreference.com/w/cpp/string/byte/memcpy

https://www.geeksforgeeks.org/memcpy-in-cc/