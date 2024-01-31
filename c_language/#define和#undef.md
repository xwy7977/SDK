# #define 和 #undef

## 概述

#define是C/C++语言的一个预处理指令，用来定义一个宏，编译器在预处理的时候会先替换掉所有的宏，然后再进行编译。#undef用来解除宏定义，解除后，这个宏定义就不存在了。

## #define的语法

```C
#define identifier replacement-list (optional)	        (1)	
#define identifier ( parameters ) replacement-list	    (2)	
#define identifier ( parameters, ... ) replacement-list	(3)	(since C99)
#define identifier ( ... ) replacement-list	            (4)	(since C99)
#undef identifier  	                                    (5)	
```

#define定义的宏可以分为两类：

- 类对象的宏（Object-like macros）
- 类函数的宏（Function-like macros）


### 类对象的宏（Object-like macros）
语法中的(1)就是类对象的宏的形式，比较直观，就是把代码中的所有的`identifier`都替换成`replacement-list`。

### 类函数的宏（Function-like macros）

类函数的宏在进行替换时，要把相应的参数也替换到对应的位置。

### #undef

#undef用来解除宏定义，从#undef开始，这个宏就失效了。

## 例子

### Example 1

```C
// C Program to illustrate how to use #define to declare 
// constants 
#include <stdio.h> 

// Defining macros with constant value 
#define PI 3.14159265359 

int main() 
{ 

	int radius = 21; 
	int area; 

	// Using macros to calculate area of circle 
	area = PI * radius * radius; 

	printf("Area of Circle of radius %d: %d", radius, area); 

	return 0; 
}
```

**Output**

```
Area of Circle of radius 21: 1385
```

### Example 2

```C
// C Program to define the function like macros using 
// #define 
#include <stdio.h> 

// Defining parameterized macros with expression 
#define CIRCLE_AREA(r) (3.14 * r * r) 
#define SQUARE_AREA(s) (s * s) 

int main() 
{ 

	int radius = 21; 
	int side = 5; 
	int area; 

	// Using macros to calculate areas by 
	// passing argument 
	area = CIRCLE_AREA(radius); 
	printf("Area of Circle of radius %d: %d \n", radius, 
		area); 

	area = SQUARE_AREA(side); 
	printf("Area of square of side %d: %d", side, area); 

	return 0; 
}
```

**Output**

```
Area of Circle of radius 21: 1384 
Area of square of side 5: 25
```

### Example 3

```C
#include <stdio.h>
 
// make function factory and use it
#define FUNCTION(name, a) int fun_##name(int x) { return (a) * x; }
 
FUNCTION(quadruple, 4)
FUNCTION(double, 2)
 
#undef FUNCTION
#define FUNCTION 34
#define OUTPUT(a) puts( #a )
 
int main(void)
{
    printf("quadruple(13): %d\n", fun_quadruple(13) );
    printf("double(21): %d\n", fun_double(21) );
    printf("%d\n", FUNCTION);
    OUTPUT(billion);               // note the lack of quotes
}
```

**Output**

```
quadruple(13): 52
double(21): 42
34
billion
```

## 参考

[Replacing text macros - cppreference.com](https://en.cppreference.com/w/c/preprocessor/replace#Predefined_macros)

[#define in C - GeeksforGeeks](https://www.geeksforgeeks.org/c-define-preprocessor/)

[#define directive (C/C++) | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/preprocessor/hash-define-directive-c-cpp?view=msvc-170)

[#define 指令 (C/C++) | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/preprocessor/hash-define-directive-c-cpp?view=msvc-170)