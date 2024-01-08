# alignas

## 概述

`alignas`用来改变内存中类型或对象的对齐方式。

## 语法

```cpp
alignas(expression)
alignas(type-id)
alignas(pack...)
```

## 用法示例

### alignas(expression)

`expression`必须是整型常量表达式，可以是0或者2的幂，其他的表达式都是不符合语法的。

`alignas`常用来控制用户自定义的类型的对齐，例如：

```cpp
struct alignas(8) S1
{
    int x;
};

static_assert(alignof(S1) == 8, "alignof(S1) should be 8");
```

当多个`alignas`用于同一个声明时，`expression`以最大的为准，`expression`为`0`时，忽略。例如：

```cpp
class alignas(4) alignas(16) C1 {};

// `alignas(0)` ignored
union alignas(0) U1
{
    int i;
    float f;
};

union U2
{
    int i;
    float f;
};

static_assert(alignof(C1) == 16, "alignof(C1) should be 16");
static_assert(alignof(U1) == alignof(U2), "alignof(U1) should be equivalent to alignof(U2)");
```

### alignas(type-id)

可以提供类型作为对齐值，类型的默认对齐方式用作对齐值。例如：

```cpp
struct alignas(double) S2
{
    int x;
};

static_assert(alignof(S2) == alignof(double), "alignof(S2) should be equivalent to alignof(double)");
```

### alignas(pack...)

模板参数包（template parameter pack）可以用于内存对齐值，包中的所有元素的最大的内存对齐值被用来作为内存对齐值。

```cpp
template <typename... Ts>
class alignas(Ts...) C2
{
    char c;
};

static_assert(alignof(C2<>) == 1, "alignof(C2<>) should be 1");
static_assert(alignof(C2<short, int>) == 4, "alignof(C2<short, int>) should be 4");
static_assert(alignof(C2<int, float, double>) == 8, "alignof(C2<int, float, double>) should be 8");
```

## 注意

1. 如果使用了多次`alignas`，会取最大值作为内存对齐值。

2. `alignas`所设置的内存对齐值不能小于变量原本的内存对齐值。例如：

3. 用户自定义类型在声明和定义时必须使用相同的内存对齐值。

    ```cpp
    // Declaration of `C3`
    class alignas(16) C3;

    // Definition of `C3` with differing alignment value
    class alignas(32) C3 {}; // Error: C2023 'C3': Alignment (32) different from prior declaration (16)

    int main()
    {
        alignas(2) int x; // ill-formed because the natural alignment of int is 4
    }
    ```

## 参考

[alignas specifier (since C++11) - cppreference.com](https://en.cppreference.com/w/cpp/language/alignas)

[C++11新增alignas关键字作用_alignas c++-CSDN博客](https://blog.csdn.net/buknow/article/details/113879907)

[Alignas in C++ 11 - GeeksforGeeks](https://www.geeksforgeeks.org/alignas-in-cpp-11/)

[alignas (C++) | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/cpp/alignas-specifier?view=msvc-170)