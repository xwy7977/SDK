# grep

## grep的历史

wikipedia这样介绍 grep 的历史

    Before it was named, grep was a private utility written by Ken Thompson to search files for certain patterns. Doug McIlroy, unaware of its existence, asked Thompson to write such a program. Responding that he would think about such a utility overnight, Thompson actually corrected bugs and made improvements for about an hour on his own program called s (short for "search"). The next day he presented the program to McIlroy, who said it was exactly what he wanted. Thompson's account may explain the belief that grep was written overnight.

    Thompson wrote the first version in PDP-11 assembly language to help Lee E. McMahon analyze the text of The Federalist Papers to determine authorship of the individual papers. The ed text editor (also authored by Thompson) had regular expression support but could not be used to search through such a large amount of text, as it loaded the entire file into memory to enable random access editing, so Thompson excerpted that regexp code into a standalone tool which would instead process arbitrarily long files sequentially without buffering too much into memory. He chose the name because in ed, the command g/re/p would print all lines featuring a specified pattern match. grep was first included in Version 4 Unix. Stating that it is "generally cited as the prototypical software tool", McIlroy credited grep with "irrevocably ingraining" Thompson's tools philosophy in Unix.

    在这个工具被命名前，他只是 Ken Thompson 的私人工具，用来根据正则表达式在文件中进行搜索。Doug McIlroy，并不知道 grep 的存在，就请 Thompson 来写一个这样的程序。Thompson 回应说他花一个晚上就可以完成，回去以后，Thompson 花了一个晚上对自己的程序进行了修正，第二天就给了 McIlroy，McIlroy 说这就是他想要的。

    Thompson 在PDP-11上使用汇编语言编写了第一个版本，帮助 Lee E. McMahon 分析《联邦党人文集》的文本，以确定个别论文的作者身份。ed 文本编辑器（也由 Thompson 编写）支持正则表达式，但不能用于搜索如此大量的文本，因为它需要将整个文件加载到内存中以实现随机访问，而内存没有那么大，因此 Thompson 将实现正则搜索功能的代码摘录到一个独立的工具中，该工具将按顺序处理任意长的文件，而不会在内存中缓冲太多。 他之所以选择这个名字，是因为在 ed 中，命令g/re/p将打印匹配正则表达式的所有行。grep最初包含在 Unix 版本 4 中。McIlroy指出，它“通常被认为是典型的软件工具”，他认为 grep 在 Unix 中“不可逆转地继承”了 Thompson 的工具哲学。



## grep的用法

## 参考

https://www.bilibili.com/video/BV1QC4y1W7N1

https://en.wikipedia.org/wiki/Grep

https://cn.linux-console.net/?p=13411#gsc.tab=0