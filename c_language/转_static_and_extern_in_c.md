[原文地址：https://leimao.github.io/blog/Static-Extern-C/](https://leimao.github.io/blog/Static-Extern-C/)

# Static and Extern in C

## 概述

在C语言中，关键字 static 和 extern 一般用来对变量和函数的存储周期和链接（linkage）作用范围进行修饰。在这篇文章中，将使用一个比较简明的例子对这两个关键字进行介绍。

## static 和 extern 关键字

* static - 静态存储周期和内部链接。
* extern - 静态存储周期和外部链接。

静态存储周期指的是存在于程序运行的整个生命周期，在 main 函数执行之前，只被初始化一次并且被储存在对象中。

内部链接指的是标识符只能被同一个翻译单元（translation unit）引用。被 static 修饰的、具有文件作用域的就是内部链接。

外部链接指的是可以被程序中的其他翻译单元引用，非 static 修饰的函数、extern 修饰的变量，以及非 static 修饰的具有文件作用域的变量都是外部链接。

    什么是文件作用域：是从变量名字声明之处直至该编译单元结束之处。

## Example

下面是使用 static 和 extern 的简单例子。

**lib.c**

```c
#include <stdio.h>

/* Static variable is local to this file. */
/* other files can also have a variable of the same name. */
static int i = 0;

/* External variable j from other files. */
extern int j;

/* Static function local to this file. */
static void hello_heaven()
{
    printf("-----------------------------------------------\n");
    printf("hello_heaven called from lib\n");
}

/* extern void hello_world(); */
/* extern is not needed since declaration always refers extern for
 * implementation. */
void hello_world();

/* Static function shortcut */
void hello_heaven_shortcut() { hello_heaven(); }

int a = 5;

void hello_underworld()
{
    static int k = 0;
    i++;
    j++;
    k++;
    printf("-----------------------------------------------\n");
    printf("hello_underworld called from lib\n");
    printf("static variable i from lib: %d\n", i);
    printf("extern variable j from lib: %d\n", j);
    printf("static variable k from lib hello_underworld: %d\n", k);
    hello_world();
}
```

**lib.h**

```c
void hello_heaven();
void hello_heaven_shortcut();
void hello_underworld();
```

**main.c**

```c
#include "lib.h"
#include <stdio.h>

static int i = 0;

int j = 0;

/* multiple definition of `a' during linking since it's defined elsewhere */
/* int a = 10; */

void hello_world()
{
    i++;
    j++;
    printf("-----------------------------------------------\n");
    printf("hello_world called from main\n");
    printf("static variable i from main: %d\n", i);
    printf("extern variable j from main: %d\n", j);
}

int main()
{
    /* undefined reference to `hello_heaven' during linking since it's static in
     * lib.c */
    /* hello_heaven(); */
    hello_heaven_shortcut();
    hello_world();
    hello_world();
    hello_world();
    hello_underworld();
    hello_underworld();
}
```

```
$ gcc -c lib.c -o lib.o
$ gcc -c main.c -o main.o
$ gcc -o main main.o lib.o 
$ ./main 
-----------------------------------------------
hello_heaven called from lib
-----------------------------------------------
hello_world called from main
static variable i from main: 1
extern variable j from main: 1
-----------------------------------------------
hello_world called from main
static variable i from main: 2
extern variable j from main: 2
-----------------------------------------------
hello_world called from main
static variable i from main: 3
extern variable j from main: 3
-----------------------------------------------
hello_underworld called from lib
static variable i from lib: 1
extern variable j from lib: 4
static variable k from lib hello_underworld: 1
-----------------------------------------------
hello_world called from main
static variable i from main: 4
extern variable j from main: 5
-----------------------------------------------
hello_underworld called from lib
static variable i from lib: 2
extern variable j from lib: 6
static variable k from lib hello_underworld: 2
-----------------------------------------------
hello_world called from main
static variable i from main: 5
extern variable j from main: 7
```

## References

[Storage-Class Specifiers - C++ Reference](https://en.cppreference.com/w/c/language/storage_duration)