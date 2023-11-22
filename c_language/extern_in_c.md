# extern关键字

## 概述

在C语言中，关键字extern可以作用于变量和函数，以扩展变量和函数的可见性。

为了更好的介绍关键字extern,先介绍声明和定义的区别。
* 变量或函数的声明就只是说这个变量或函数在程序的其他地方存在，但是并没有为他们申请内存。变量或函数的声明主要就是为了告诉程序他们是什么类型，函数的声明还让程序知道函数的参数类型、参数顺序、以及返回值。
* 函数或变量的定义，除了具有声明所具有的全部作用外，定义还为变量或函数申请内存。因此，我们可以认为定义是声明的超集。

extern是external的缩写，如果某个代码文件需要的变量存在于其他的文件中，一般就会使用extern.

## C语言中extern的语法

在变量声明前加入extern即可。

```
extern data_type variable_name;
```

## 一个使用extern的例子

```C
#include <stdio.h> 

extern int a;	 // int var; -> declaration and definition 
				// extern int var; -> declaration 

int main() 
{ 
	printf("%d", a); 

	return 0; 
}

```

上面只是一个使用的例子，可以编译，但是链接会出错，因为还没有定义。

## C语言使用extern的一些注意点

* 使用该关键字进行变量声明的时候，并没有申请内存，只是告诉程序，可以使用这个变量啦。
* 可以在文件中多次使用extern关键字来声明一个变量。
* extern关键字告诉编译器，这个变量是在别的地方定义的，跳出这个范围去找。
* 编译器是无条件的相信extern关键字的，在编译的时候不会报错，但是如果变量没有在其他地方进行定义的话，链接器会报错的。
* 如果使用extern修饰的变量被初始化，那么将会申请内存，并且被认为是定义。

一个变量或函数可以被多次声明，但是只能被定义一次，因为你不能在两个地方存放相同的变量或函数。

## extern在函数中的使用

当我们声明函数时，extern属性是隐式添加的。比如，我们像如下去声明函数：

```C
int foo(int arg1, char arg2);
```

在编译器眼里是这样的：

```C
extern int foo(int arg1, char arg2);
```

所以只要在代码文件里进行了函数的声明，就算不加extern,编译器也认为这个函数已经在其他地方定义了，会继续进行编译而不报错。

## extern在声明变量时的使用

如果我们只是想声明一个变量，可以这样去做：

```C
extern int var;
```

这样一个整数类型的变量就声明好了，但是并没有申请内存，我们可以声明多次。

如果你想定义这个变量，可以像这样去做：

```C
int var = 10;
```

上面这行代码同时进行了变量的声明和定义，也申请了内存。编译器不会自动为变量添加extern属性，因为如果添加的话，就不会为变量申请内存了。extern关键字必须显式写出以扩展变量的可见性。通过为变量使用extern关键字，我们可以在程序的任何地方使用这个变量（如果该变量已经被定义的话）。

**Example 1**

```C
int var; 
int main(void) 
{ 
	var = 10; 
	return 0; 
} 
```

这个程序可以成功编译，变量var是一个全局变量。

**Example 2**

```C
extern int var; 
int main(void) 
{ 
	return 0; 
} 
```

这个程序可以成功编译，因为变量var只是被声明，并且没有在程序中使用。

**Example 3**

```C
extern int var; 
int main(void) 
{ 
	var = 10; 
	return 0; 
} 
```

这个程序在编译（此处的编译指的是编译和链接）的时候会出错，因为var被声明，但是没有在其他地方定义。本质上，var没有申请内存，当去把var的值变为10的时候发现这个变量根本不存在。

**Example 4**

```C
// As we are importing the file and henceforth the 
// defination 
#include "somefile.h" 

// Declaring the same variable 
extern int var; 
	// int var; 
	// It will throw compiler error as compiler will get 
	// confused where the variable is defined 

int main(void) 
{ 
	var = 10; 
	return 0; 
} 

// Now it will compile and run successfully
```

如果在somefile.h文件中定义了var,这个程序可以编译成功。

**Example 5**

```C
extern int var = 0; 
int main(void) 
{ 
	var = 10; 
	return 0; 
} 
```

上面这个程序也可编译成功，在声明的时候进行初始化相当于进行了定义。

## 总结一下

1. 声明可以有多次，但是定义只能有一次。
2. extern关键字被用来扩展变量或函数的可见性。
3. 函数声明时默认添加extern关键字，所以在函数定义或声明时extern关键字不是必须的，隐式添加。
4. extern用于变量时，只在声明时使用，不再定义时使用。
5. 有一个例外，如果一个变量在声明时被初始化并且被extern修饰，此时也视为定义。

## 参考

https://www.geeksforgeeks.org/understanding-extern-keyword-in-c/