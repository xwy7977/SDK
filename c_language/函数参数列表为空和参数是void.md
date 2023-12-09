# 函数参数列表为空和参数是void

## 概述

如果想要定义一个不带参数的函数，可能会看见以下两种不同的写法。

```C
void foo() { }

void foo(void) { }
```

其实他们之间是有区别的：

> In C:
>    - `void foo()` means "a function `foo` taking an unspecified number of arguments of unspecified type"
>    - `void foo(void)` means "a function `foo` taking no arguments"
>
> In C++:
>    - `void foo()` means "a function `foo` taking no arguments"
>    - `void foo(void)` means "a function `foo` taking no arguments"

就是说：

- 对于C语言：如果参数列表为空，表示可以接受任何参数；如果参数是void,表示不可以接受任何参数。
- 对于C++：参数列表为空和参数是void都表示不可以接受任何参数。

## Example

下面的例子中，`foo_a`参数列表为空，可以接受任何参数。`foo_b`参数是void,不可以接受任何参数，如果不注释掉，程序是不能编译运行的。

```C
#include <stdio.h>

void foo_a()
{
	printf("hello foo_a()\n");
}

void foo_b(void)
{
	printf("hello foo_b()\n");
}

int main(void)
{
	foo_a(1, "abc");
	// foo_b( 1, "abc" );
	return 0;
}
```

## 参考

https://www.zhihu.com/question/476345907/answer/2048368398

https://en.cppreference.com/w/c/language/function_declaration

https://stackoverflow.com/questions/51032/is-there-a-difference-between-foovoid-and-foo-in-c-or-c