# glibc概述

## 什么是lib（library）

> In computer science, a library is a collection of non-volatile resources used by computer programs, often for software development. These may include configuration data, documentation, help data, message templates, pre-written code and subroutines, classes, values or type specifications. -- wikipedia

在计算机科学中，库是计算机程序使用的非易失性资源的集合，通常用于软件开发。库可能包括配置数据、文档、帮助数据、消息模板、预先编写的代码和子例程、类、值或类型定义。

## 什么是libc

> The C standard library or libc is the standard library for the C programming language, as specified in the ISO C standard. Starting from the original ANSI C standard, it was developed at the same time as the C library POSIX specification, which is a superset of it. Since ANSI C was adopted by the International Organization for Standardization, the C standard library is also called the ISO C library. 
> 
> The C standard library provides macros, type definitions and functions for tasks such as string handling, mathematical computations, input/output processing, memory management, and several other operating system services.

libc，通常指的是C语言标准库，会提供一些用于字符串处理、数学计算、输入输出处理、内存管理等操作系统服务的宏、类型定义和函数。

存在许多libc的实现，他们适用于不同的操作系统和C编译器，下面是一些比较流行的libc：

- BSD libc：在BSD的衍生操作系统上实现的libc。
- GNU C Library (glibc)：在GNU Hurd, GNU/kFreeBSD 和 Linux上使用。
- Microsoft C run-time library：Microsoft Visual C++的一部分，存在两个版本MSVCRT和UCRT。
- dietlibc：C标准库的替代品，更小。
- μClibc：嵌入式μClinux使用的libc.
- Newlib：嵌入式系统中使用的libc.
- klibc：主要用于启动linux系统。
- musl：linux系统的轻量级C标准库。
- Bionic：继承自BSD libc,是Google用于Android嵌入式系统的。
- picolibc：主要用于内存有限的嵌入式系统，基于Newlib和AVR libc进行开发。

## 什么是glibc

glibc，即GNU C Library，是Linux平台上使用最广泛的C运行库。

glibc最初由自由软件基金会FSF(FreeSoftware Foundation)发起开发，目的是为GNU操作系统开发一个C标准库。GNU操作系统最初计划的内核是Hurd，一个微内核的构架系统。Hurd因为种种原因开发进展缓慢，而Linux因为它的实用性而逐渐风靡，最后取代Hurd成了GNNU操作系统的内核。于是glibc从最初开始支持Hurd到后来渐渐发展成同时支持Hurd和Linux，而且随着Linux的越来越流行，glibc也主要关注Linux下的开发，成为了Linux平台的C标准。

20世纪90年代初，在glibc成为Linux下的C运行库之前，Linux的开发者们因为开发的需要，从Linux内核代码里面分离出了一部分代码，形成了早期Linux下的C运行库。这个C运行库又被称为Linux libc。这个版本的C运行库被维护了很多年，从版本2一直开发到版本5。如果你去看早期版本的Linux，会发现/lib目录下面有1ibc.so.5这样的文件，这个文件就是第五个版本的Linux libc。1996年FSF发布了glibc2.0，这个版本的glibc开始支持诸多特性，比如它完全支持POSIX标准、国际化、IPv6、64-位委数据访问、多线程及改进了代码的可移植性。在此时Linux libc的开发者也认识到单独地维护一份Linux下专用的C运行库是没有必要的，于是Linux开始采用glibc作为默认的C运行库，并且将2.x版本的glibc看作是Linux libc的后继版本。于是我们可以看到，glibc在/lib（或者lib64）目录下的.so文件为libc.so.6，即第六个libc版本，而且在各个Linux发行版中，glibc往往被称为libc6。glibc在Linux平台下占据了主导地位之后，它又被移植到了其他操作系统和其他硬件平台，诸如FreeBSD、NetBSD等，而且它支持数十种CPU及嵌入式平台。

## 参考

https://en.wikipedia.org/wiki/Library_(computing)

https://en.wikipedia.org/wiki/C_standard_library

https://www.gnu.org/software/libc/

https://linuxstory.org/musl-libc-yet-another-libc/

https://en.wikipedia.org/wiki/Glibc

https://www.cnblogs.com/lvzh/p/17795997.html

https://sourceware.org/glibc/manual/pdf/libc.pdf