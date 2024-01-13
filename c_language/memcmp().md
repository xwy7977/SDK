# memcmp()

## 语法

```C
int memcmp( const void* lhs, const void* rhs, size_t count );
```

- lhs，rhs：指向被比较对象的指针。
- count：被比较的字节数。

函数`memcmp()`定义在头文件`<string.h>`中。它比较指针`lhs`和`rhs`指向的对象的前`count`个字节，按照字典序进行比较。

在进行比较时，每个字节都被解释为无符号字符型（unsigned char）。函数的返回值的正负与被比较对象中的第一对不同字节的差值的正负相同：如果`lhs`小于`rhs`，返回负值；如果`lhs`等于`rhs`，返回0；如果`lhs`大于`rhs`，返回正值。

如果访问到了`lhs`和`rhs`所指向的对象的末尾之后，或者`lhs`和`rhs`有一个是空指针，都是未定义的行为。

## Example

```C
#include <stdio.h>
#include <string.h>
 
void demo(const char* lhs, const char* rhs, size_t sz)
{
    for(size_t n = 0; n < sz; ++n)
        putchar(lhs[n]);
 
    int rc = memcmp(lhs, rhs, sz);
    const char *rel = rc < 0 ? " precedes " : rc > 0 ? " follows " : " compares equal ";
    fputs(rel, stdout);
 
    for(size_t n = 0; n < sz; ++n)
        putchar(rhs[n]);
    puts(" in lexicographical order");
}
 
int main(void)
{
    char a1[] = {'a','b','c'};
    char a2[sizeof a1] = {'a','b','d'};
 
    demo(a1, a2, sizeof a1);
    demo(a2, a1, sizeof a1);
    demo(a1, a1, sizeof a1);
}
```

**Output**
```
abc precedes abd in lexicographical order
abd follows abc in lexicographical order
abc compares equal to abc in lexicographical order
```

## 参考

[memcmp - cppreference.com](https://en.cppreference.com/w/c/string/byte/memcmp)

[[C语言]memcmp函数返回值讨论_memcmp返回值是什么-CSDN博客](https://blog.csdn.net/weixin_43727672/article/details/112260503)

[c - What, exactly, is memcmp supposed to return? - Stack Overflow](https://stackoverflow.com/questions/44975110/what-exactly-is-memcmp-supposed-to-return)

[memcmp, wmemcmp | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/memcmp-wmemcmp?view=msvc-170)