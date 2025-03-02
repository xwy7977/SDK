```
/*
 * github: https://github.com/google/Sanitizers
 * address santizer
 * 
 * 注意：在Mingw64中并不支持Sanitizers，以下代码是在Ubuntu 22.04中运行的。
 */

#include "stdio.h"

void f()
{
    int a[2] = {1, 0};
    int b = a[2];
    printf("b is: %d\n", b);
}

int main()
{
    f();
    return 0;
}

/*
1. 使用 gcc san-addr.c 编译后运行，会打印一个随机值。这个随机值是不固定的。

b is: -1032651776

2. 使用 gcc -fsanitize=address san-addr.c 编译后运行，会打印如下信息，提示错误。

=================================================================
==9604==ERROR: AddressSanitizer: stack-buffer-overflow on address 0x7ffdb2aac9e8 at pc 0x561ad2c9037d bp 0x7ffdb2aac9a0 sp 0x7ffdb2aac990
READ of size 4 at 0x7ffdb2aac9e8 thread T0
    #0 0x561ad2c9037c in f (/test/a.out+0x137c)
    #1 0x561ad2c90406 in main (/test/a.out+0x1406)
    #2 0x7f4662255d8f  (/lib/x86_64-linux-gnu/libc.so.6+0x29d8f)
    #3 0x7f4662255e3f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x29e3f)
    #4 0x561ad2c90184 in _start (/test/a.out+0x1184)

Address 0x7ffdb2aac9e8 is located in stack of thread T0 at offset 40 in frame
    #0 0x561ad2c90258 in f (/test/a.out+0x1258)

  This frame has 1 object(s):
    [32, 40) 'a' (line 5) <== Memory access at offset 40 overflows this variable
HINT: this may be a false positive if your program uses some custom stack unwind mechanism, swapcontext or vfork
      (longjmp and C++ exceptions *are* supported)
SUMMARY: AddressSanitizer: stack-buffer-overflow (/test/a.out+0x137c) in f
Shadow bytes around the buggy address:
  0x10003654d8e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d8f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d900: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d910: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d920: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x10003654d930: 00 00 00 00 00 00 00 00 f1 f1 f1 f1 00[f3]f3 f3
  0x10003654d940: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d950: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d960: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d970: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10003654d980: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
  Shadow gap:              cc
==9604==ABORTING

*/
```