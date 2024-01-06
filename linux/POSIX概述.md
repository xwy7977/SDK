# POSIX概述

## 什么是POSIX

> The Portable Operating System Interface (POSIX; IPA: /ˈpɒz.ɪks/) is a family of standards specified by the IEEE Computer Society for maintaining compatibility between operating systems. POSIX defines both the system and user-level application programming interfaces (APIs), along with command line shells and utility interfaces, for software compatibility (portability) with variants of Unix and other operating systems. POSIX is also a trademark of the IEEE. POSIX is intended to be used by both application and system developers.

POSIX（Portable Operating System Interface，可移植操作系统接口），是IEEE计算机协会为保持操作系统之间的兼容性而制定的**一系列标准**。POSIX定义了系统级和用户级应用程序编程接口（API），以及shell命令行和实用程序接口，以实现Unix和各个Unix变体以及其他操作系统之间的软件兼容性（可移植性）。POSIX也是IEEE的商标。 POSIX旨在供应用程序和系统开发人员使用。

### POSIX的由来

Richard Stallman 解释了 POSIX 的由来。

> The IEEE had finished developing the spec but had no concise name for it. The title said something like "portable operating system interface," though I don't remember the exact words. The committee put on "IEEEIX" as the concise name. I did not think that was a good choice. It is ugly to pronounce—it would sound like a scream of terror, "Ayeee!"—so I expected people would instead call the spec "Unix."
>
> Since GNU's Not Unix, and it was intended to replace Unix, I did not want people to call GNU a "Unix system." I, therefore, proposed a concise name that people might actually use. Having no particular inspiration, I generated a name the unclever way: I took the initials of "portable operating system" and added "ix." The IEEE adopted this eagerly.

IEEE 已经完成了规范的制定，但没有简洁的名称。标题是 “可移植的操作系统接口”，虽然我不记得确切的字眼了。委员会把 “IEEEIX” 作为简写。我不认为这是个好的选择。它的发音很难听 —— 听起来就像恐怖的尖叫声，“Ayeee！” —— 所以我预计人们会把这个规范叫为 “Unix”。

由于 GNU 不是 Unix，而它的目的是取代 Unix，我不希望人们把 GNU 称为 “Unix 系统”。因此，我提出了一个人们可能真正使用的简洁的名字。在没有特别灵感的情况下，我用了一种很笨的方式取了一个名字。我取了 “可移植操作系统” 的首字母并加上 “ix”。IEEE 马上就采用了这个名字。

## POSIX版本

在1997年之前，POSIX主要包括以下几个标准：

- **POSIX.1**，即 IEEE Std 1003.1-1988。
- **POSIX.1b**，即 IEEE Std 1003.1b-1993。
- **POSIX.1c**，即 IEEE Std 1003.1c-1995。
- **POSIX.2**，即 IEEE Std 1003.2-1992。

在1997年之前，POSIX主要包括以下几个标准：

- **POSIX.1-2001**，即 IEEE Std 1003.1-2001。
- **POSIX.1-2008**，即 IEEE Std 1003.1-2008。
- **POSIX.1-2001**，即 IEEE Std 1003.1-2017。

## POSIX定义了哪些东西

POSIX定义了以下4部分内容：

- Base Definitions：包含该标准中的一些基本定义，比如一些术语、概念等。
- System Interfaces：包含该标准中提供给应用程序的接口。
- Shell and Utilities：包含该标准中提供的命令行和实用程序。
- Rationale：包含有关本标准内容的历史信息，以及标准开发人员为什么包含或放弃这些功能。

## 哪些系统兼容POSIX

Linux、macOS、Windows NT等都是兼容POSIX的。

## 参考

[The origin of the name POSIX.](https://stallman.org/articles/posix.html)

[The Open Group Base Specifications Issue 7, 2018 edition](https://pubs.opengroup.org/onlinepubs/9699919799/)

[1003.1-2017 - IEEE Standard for Information Technology--Portable Operating System Interface (POSIX(TM)) Base Specifications, Issue 7 | IEEE Standard | IEEE Xplore](https://ieeexplore.ieee.org/document/8277153)

[What is POSIX? Richard Stallman explains | Opensource.com](https://opensource.com/article/19/7/what-posix-richard-stallman-explains?ref=itsfoss.com)

[What is POSIX (Portable Operating System Interface)?](https://www.techtarget.com/whatis/definition/POSIX-Portable-Operating-System-Interface)

[A Guide to POSIX | Baeldung on Linux](https://www.baeldung.com/linux/posix)

[POSIX - Wikipedia](https://en.wikipedia.org/wiki/POSIX)

[观点|Linux 黑话解释：什么是 POSIX？](https://linux.cn/article-14201-1.html)

[posix是什么都不知道，还好意思说你懂Linux？ - 知乎](https://zhuanlan.zhihu.com/p/392588996)

