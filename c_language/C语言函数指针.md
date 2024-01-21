# C语言函数指针

在C语言中，可以像定义基本数据类型的指针一样，我们可以定义指向函数的指针。下面是一个函数指针声明和定义的例子：

```C
#include <stdio.h> 
// A normal function with an int parameter 
// and void return type 
void fun(int a) 
{ 
	printf("Value of a is %d\n", a); 
} 

int main() 
{ 
	// fun_ptr is a pointer to function fun() 
	void (*fun_ptr)(int) = &fun; 

	/* The above line is equivalent of following two 
	void (*fun_ptr)(int); 
	fun_ptr = &fun; 
	*/

	// Invoking fun() using fun_ptr 
	(*fun_ptr)(10); 

	return 0; 
} 
```

**Output**

```
Value of a is 10
```

我们定义函数指针的时候要使用括号括起来，就像上面的例子这样。因为如果我们不使用括号，`void (*fun_ptr)(int)`就变成了`void *fun_ptr(int)`，就变成了定义一个返回值是void指针类型的函数。

下面介绍一些在理解函数指针时应该理解的点。

**1. 与普通指针不同，函数指针指向的是代码，而不是数据。通常，函数指针存储可执行代码的开头。**

**2. 与普通指针不同，我们不去为函数指针申请或释放内存。**

**3. 通常可以用函数名去获取函数地址，像下面的例子，我们可以在赋值运算中不写`&`符号，也可以在函数调用时不写`*`符号，程序照样正常运行。**

```C
#include <stdio.h> 
// A normal function with an int parameter 
// and void return type 
void fun(int a) 
{ 
    printf("Value of a is %d\n", a); 
} 

int main() 
{ 
    void (*fun_ptr)(int) = fun; // & removed 

    fun_ptr(10); // * removed 

    return 0; 
}
```

**Output**

```
Value of a is 10
```

**4. 像普通指针一样，我们可以有一个函数指针数组。下面第5点中的示例显示了函数指针数组的语法。**

**5. 函数指针可以用来代替switch语句。例如，在下面的程序中，用户被要求在0和2之间进行选择以执行不同的任务。**

```C
#include <stdio.h> 
void add(int a, int b) 
{ 
    printf("Addition is %d\n", a+b); 
} 
void subtract(int a, int b) 
{ 
    printf("Subtraction is %d\n", a-b); 
} 
void multiply(int a, int b) 
{ 
    printf("Multiplication is %d\n", a*b); 
} 

int main() 
{ 
    // fun_ptr_arr is an array of function pointers 
    void (*fun_ptr_arr[])(int, int) = {add, subtract, multiply}; 
    unsigned int ch, a = 15, b = 10; 

    printf("Enter Choice: 0 for add, 1 for subtract and 2 "
            "for multiply\n"); 
    scanf("%d", &ch); 

    if (ch > 2) return 0; 

    (*fun_ptr_arr[ch])(a, b); 

    return 0; 
} 
```

**Output**

```
Enter Choice: 0 for add, 1 for subtract and 2 for multiply
2
Multiplication is 150 
```

**6. 与普通数据指针一样，函数指针可以作为参数传递，也可以从函数返回。**
    
例如，下面的C程序，其中`wrapper()`接收一个`void fun()`作为参数并调用传递的函数。

```C
// A simple C program to show function pointers as parameter 
#include <stdio.h> 

// Two simple functions 
void fun1() { printf("Fun1\n"); } 
void fun2() { printf("Fun2\n"); } 

// A function that receives a simple function 
// as parameter and calls the function 
void wrapper(void (*fun)()) 
{ 
    fun(); 
} 

int main() 
{ 
    wrapper(fun1); 
    wrapper(fun2); 
    return 0; 
}
```

这个特性在C语言中非常有用，我们可以用函数指针来避免代码的冗余。比如`qsort()`函数，可以用来升序或降序排列数组，或者在结构数组的情况下按任何其他顺序进行排序。不仅如此，通过函数指针和void指针，可以对任何数据类型使用qsort。

```C
// An example for qsort and comparator 
#include <stdio.h> 
#include <stdlib.h> 

// A sample comparator function that is used 
// for sorting an integer array in ascending order. 
// To sort any array for any other data type and/or 
// criteria, all we need to do is write more compare 
// functions. And we can use the same qsort() 
int compare (const void * a, const void * b) 
{ 
    return ( *(int*)a - *(int*)b ); 
} 

int main () 
{ 
    int arr[] = {10, 5, 15, 12, 90, 80}; 
    int n = sizeof(arr)/sizeof(arr[0]), i; 

    qsort (arr, n, sizeof(int), compare); 

    for (i=0; i<n; i++) 
        printf ("%d ", arr[i]); 
    return 0; 
} 
```

**Output**

```
5 10 12 15 80 90
```

与`qsort()`类似，我们可以编写自己的函数，这些函数可以用于任何数据类型，并且可以在没有代码冗余的情况下执行不同的任务。以下是可用于任何数据类型的搜索函数示例。事实上，我们可以使用这个搜索函数，通过编写自定义的比较函数来找到接近的元素（低于阈值）。

```C
#include <stdio.h> 
#include <stdbool.h> 

// A compare function that is used for searching an integer 
// array 
bool compare (const void * a, const void * b) 
{ 
    return ( *(int*)a == *(int*)b ); 
} 

// General purpose search() function that can be used 
// for searching an element *x in an array arr[] of 
// arr_size. Note that void pointers are used so that 
// the function can be called by passing a pointer of 
// any type. ele_size is size of an array element 
int search(void *arr, int arr_size, int ele_size, void *x, 
        bool compare (const void * , const void *)) 
{ 
    // Since char takes one byte, we can use char pointer 
    // for any type/ To get pointer arithmetic correct, 
    // we need to multiply index with size of an array 
    // element ele_size 
    char *ptr = (char *)arr; 

    int i; 
    for (i=0; i<arr_size; i++) 
        if (compare(ptr + i*ele_size, x)) 
        return i; 

    // If element not found 
    return -1; 
} 

int main() 
{ 
    int arr[] = {2, 5, 7, 90, 70}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 7; 
    printf ("Returned index is %d ", search(arr, n, 
                            sizeof(int), &x, compare)); 
    return 0; 
} 
```

**Output**

```
Returned index is 2
```

通过编写单独的自定义`compare()`，上述搜索函数可以用于任何数据类型。

**7. C++中的许多面向对象特性都是使用C中的函数指针来实现的。例如，虚拟函数。类方法是使用函数指针实现的另一个示例。**



## 参考

[Function Pointer in C - GeeksforGeeks](https://www.geeksforgeeks.org/function-pointer-in-c/)