# memset()

memset()通常为内存块填充指定值。

memset()的语法如下：

```c
// ptr ==> Starting address of memory to be filled
// x   ==> Value to be filled
// n   ==> Number of bytes to be filled starting 
//         from ptr to be filled
void *memset(void *ptr, int x, size_t n);
```

注意指针类型是void,所以我们可以向该函数传递任何类型的指针。

让我们看一看在C语言中使用memset()的简单例子：

**Example 1**

```c
// C program to demonstrate working of memset()
#include <stdio.h>
#include <string.h>

int main()
{
	char str[50] = "GeeksForGeeks is for programming geeks.";
	printf("\nBefore memset(): %s\n", str);

	// Fill 8 characters starting from str[13] with '.'
	memset(str + 13, '.', 8*sizeof(char));

	printf("After memset(): %s", str);
	return 0;
}
```

**Output**

```
Before memset(): GeeksForGeeks is for programming geeks.
After memset(): GeeksForGeeks........programming geeks.
```

**解释**

（str + 13）指向"GeeksForGeeks is for programming geeks."的第一个空格（第一个字母的下标为0），并且从该空格开始，往后数8个位置都被替换为'.'，所以看到了以上的输出。

**Example 2**

```c
// C program to demonstrate working of memset()
#include <stdio.h>
#include <string.h>

void printArray(int arr[], int n)
{
for (int i=0; i<n; i++)
	printf("%d ", arr[i]);
}

int main()
{
	int n = 10;
	int arr[n];

	// Fill whole array with 0.
	memset(arr, 0, n*sizeof(arr[0]));
	printf("Array after memset()\n");
	printArray(arr, n);

	return 0;
}
```

**Output**

```
0 0 0 0 0 0 0 0 0 0
```

但是，下面的例子稍微有点出人意料。

**Example 3**

```c
// C program to demonstrate working of memset()
#include <stdio.h>
#include <string.h>

void printArray(int arr[], int n)
{
for (int i=0; i<n; i++)
	printf("%d ", arr[i]);
}

int main()
{
	int n = 10;
	int arr[n];

	// Fill whole array with 100.
	memset(arr, 10, n*sizeof(arr[0]));
	printf("Array after memset()\n");
	printArray(arr, n);

	return 0;
}
```

**Output**

```
168430090 168430090 168430090 168430090 168430090 168430090 168430090 168430090 168430090 168430090
```

**解释**

memset赋值的时候是按字节赋值，是将参数转化成二进制之后再填入内存。比如上面的10,对应的二进制是0000 1010,一个int类型被赋值为0000 1010 0000 1010 0000 1010 0000 1010。对应的十进制就是168430090。

所以：

* 若ptr指向char型地址，x可以为任意字符值。
* 若ptr指向int型，若想要赋值正确，x可以为-1或0,因为他们的四个字节是一样的。-1=0XFFFFFFFF, 0=0X00000000。

## 参考

https://www.geeksforgeeks.org/memset-c-example/

https://blog.csdn.net/Supreme7/article/details/115431235