# void指针void*

## 什么是void指针

void指针就是没有和任何数据类型关联的指针。void指针可以存放任何类型数据的地址，也可以把void指针转化为指向任何类型数据的指针。

## 一个void指针的例子

```C
// C Program to demonstrate that a void pointer
// can hold the address of any type-castable type

#include <stdio.h>
int main()
{
	int a = 10;
	char b = 'x';

	// void pointer holds address of int 'a'
	void* p = &a;
	// void pointer holds address of char 'b'
	p = &b;
}
```

## void指针的优点

void指针具有以下优点：

* malloc()和calloc()返回void指针类型，这就允许他们为任何数据类型申请内存。
* 在C语言中，void指针可以用来实现一些通用函数，比如qsort可以对各种不同类型的数据进行排序。

## 一些需要注意的点

1.void指针不能被解引用。

以下代码不能通过编译。
```C
// C Program to demonstrate that a void pointer
// cannot be dereferenced

#include <stdio.h>
int main()
{
	int a = 10;
	void* ptr = &a;
	printf("%d", *ptr);

	return 0;
}
```

**Output**
```
Compiler Error: 'void*' is not a pointer-to-object type
```

下面这个代码是使用void指针存储整型类型的数据，并且void指针被强转为整型指针，并且被解引用。

```C
// C program to dereference the void
// pointer to access the value

#include <stdio.h>

int main()
{
	int a = 10;
	void* ptr = &a;
	// The void pointer 'ptr' is cast to an integer pointer
	// using '(int*)ptr' Then, the value is dereferenced
	// with `*(int*)ptr` to get the value at that memory
	// location
	printf("%d", *(int*)ptr);
	return 0;
}
```

**Output**
```
10
```

2.ANSI C标准不允许void指针进行算术运算，但是GNU C允许void指针进行算术运算，并且认为void指针指向的数据空间大小是1。

例如，下面的C程序是一个void指针执行算术运算的例子，可以在gcc中运行，但是在其他编译器不一定可以运行。

```C
// C program to demonstrate the usage
// of a void pointer to perform pointer
// arithmetic and access a specific memory location

#include <stdio.h>

int main()
{
	// Declare and initialize an integer array 'a' with two
	// elements
	int a[2] = { 1, 2 };
	// Declare a void pointer and assign the address of
	// array 'a' to it
	void* ptr = &a;

	// Increment the pointer by the size of an integer
	ptr = ptr + sizeof(int);

	// The void pointer 'ptr' is cast to an integer
	// pointer using '(int*)ptr' Then, the value is
	// dereferenced with `*(int*)ptr` to get the value at
	// that memory location
	printf("%d", *(int*)ptr);

	return 0;
}
```

## 参考

https://www.geeksforgeeks.org/void-pointer-c-cpp/

https://www.runoob.com/w3cnote/c-void-intro.html

https://stackoverflow.com/questions/11626786/what-does-void-mean-and-how-to-use-it

