# 使用UNUSED宏消除unused_parameter警告

## 警告：unused parameter

在代码中常见这样一种情景：函数中定义了若干个参数，但是，其中的一个或多个参数并没有使用。对于这种情况，在编译时就会给出警告。

以下面的代码为例，还原unused parameter警告。

```C
#include <stdio.h>

int func(int a, int b)
{
    printf("hello func(). \n");
    return 0;
}

int main(void)
{
	func(1 , 2);
	return 0;
}
```

使用命令 `gcc -Wall -Wextra test.c` 进行编译时，因为参数 `a` 和参数 `b` 并没有使用，所以会有下面的警告。

```
test.c: 在函数‘func’中:
test.c:3:14: 警告：unused parameter ‘a’ [-Wunused-parameter]
    3 | int func(int a, int b)
      |          ~~~~^
test.c:3:21: 警告：unused parameter ‘b’ [-Wunused-parameter]
    3 | int func(int a, int b)
      |                 ~~~~^
```

## 警告的消除

对于上面例子中的代码，添加一个宏定义`#define UNUSED(x) (void)(x)`可以消除编译带来的警告。

```C
#include <stdio.h>

#define UNUSED(x) (void)(x)

int func(int a, int b)
{
    UNUSED(a);
    UNUSED(b);
    printf("hello func(). \n");
    return 0;
}

int main(void)
{
	func(1 , 2);
	return 0;
}
```

再次进行编译时，就不会提示上面的警告信息。

## 参考

https://stackoverflow.com/questions/3599160/how-can-i-suppress-unused-parameter-warnings-in-c

https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html

https://blog.csdn.net/weiqifa0/article/details/106678290

https://linux.cn/article-8032-1.html