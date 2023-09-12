# typedef in c

关键字typedef通常用来为已经存在的数据类型提供一个新的名字。

在程序中，数据类型的名字可能比较晦涩难懂，这时候就可以使用typedef来进行用户自定义数据类型，就类似于给命令起一个别名。

## C中typedef的语法

```C
typedef existing_name alias_name;
```

在上面定义以后，就可以使用`alias_name`来表示`existing_name`。

## 在C中使用typedef的例子

```C
typedef long long ll;
```

下面是一个例子

```C
// C program to implement typedef
#include <stdio.h>

// defining an alias using typedef
typedef long long ll;

// Driver code
int main()
{
	// using typedef name to declare variable
	ll var = 20;
	printf("%ld", var);

	return 0;
}
```

**Output**

```
20
```

## 在C语言中使用typedef

以下是在C语言中使用typedef的常见情形

* 给现存的数据类型起一个有意义的名字，这样可以让其他的用户更简单的理解程序。
* 经常用于结构体，这样可以增加代码的可读性，而且不需要重复的写struct这个关键字。
* 用于指针，这样就可以使用一个简单的语句定义多个指针。
* 用于数组，这样就可以定义含有多个成员的变量。

下面会对以上的用法进行举例。

### 1. typedef用于结构体

在C语言中，typedef用于结构体时，一个新的类型被创建并且可以用于结构体变量的声明。

**Example 1: Using typedef to define a name for a structure**

```C
// C program to implement
// typedef with structures
#include <stdio.h>
#include <string.h>

// using typedef to define an alias for structure
typedef struct students {
	char name[50];
	char branch[50];
	int ID_no;
} stu;

// Driver code
int main()
{
	stu st;
	strcpy(st.name, "Kamlesh Joshi");
	strcpy(st.branch, "Computer Science And Engineering");
	st.ID_no = 108;

	printf("Name: %s\n", st.name);
	printf("Branch: %s\n", st.branch);
	printf("ID_no: %d\n", st.ID_no);
	return 0;
}
```

**Output**

```
Name: Kamlesh Joshi
Branch: Computer Science And Engineering
ID_no: 108
```

### 2. typedef 用于指针

typedef也可以用于给指针起一个别名，在定义多个指针类型的变量时使用typedef是非常有效的，因为定义指针变量的`*`是和右边的变量结合在一起的。

例如：

```C
int *var1, var2;
```

上面定义了一个指针变量var1和int型变量var2.

但是：

```C
typedef int* Int_ptr;
Int_ptr var, var1, var2;
```

定义了三个执行int型的指针变量var,var1和var2.

**Example 2: Using typedef to define a name for pointer type.**

```C
// C program to implement
// typedef with pointers
#include <stdio.h>

typedef int* ptr;

// Driver code
int main()
{
	ptr var;
	*var = 20;

	printf("Value of var is %d", *var);
	return 0;
}
```

**Output**

```
Value of var is 20
```

### 3. 使用typedef给数组起一个别名

```C
// C program to implement typedef with array
#include <stdio.h>

typedef int Arr[4];

// Driver code
int main()
{
	Arr temp = { 10, 20, 30, 40 };
	printf("typedef using an array\n");

	for (int i = 0; i < 4; i++) {
		printf("%d ", temp[i]);
	}
	return 0;
}
```

**Output**

```
typedef using an array
10 20 30 40 
```

### 4. 使用typedef定义函数指针

```C
typedef char (*PTRFUN)(int); 
PTRFUN pFun; 
char glFun(int a){ return;} 
void main() 
{ 
    pFun = glFun; 
    (*pFun)(2); 
} 
```

## typedef vs #define

typedef和#define的主要区别：
1. #define也可以为值定义别名，例如把1定义为ONE,3.14定义为PI,typedef只是为类型定义别名。
2. #define由预处理器进行解释，typedef由编译器进行解释。
3. #define语句后面没有分号，typedf语句后面有分号。
4. typedef其实是声明了一个新的类型。

下面是一个使用`#define`的例子

```C
// C program to implement #define
#include <stdio.h>

// macro definition
#define LIMIT 3

// Driver code
int main()
{
	for (int i = 0; i < LIMIT; i++) {
		printf("%d \n", i);
	}
	return 0;
}
```

**Output**

```
0 
1 
2 
```

## 参考

https://www.geeksforgeeks.org/typedef-in-c/

https://blog.csdn.net/qll125596718/article/details/6891881

https://en.cppreference.com/w/c/language/typedef

