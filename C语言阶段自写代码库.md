# C语言阶段自写代码库

## 递归

### 计算 n 的 k 次方

```C
#include<stdio.h>
int power(int n, int k) {
    if (k == 0) return 1;
    if (k < 0) return 0;
    if (k > 0) return n * power(n, k - 1);
}
int main() {
    int n = 0, k = 0;
    printf("请输入基数 n:"); scanf_s("%d", &n);
    printf("请输入指数 k:"); scanf_s("%d", &k);
    int result = power(n, k);
    printf("%d的%d次方是 %d\n", n, k, result);
    return 0;
}
```

### 斐波那契数列（递归版）

```C
#include<stdio.h>
int Fib(int n) {
    if(n <= 2) return 1;
    else return Fib(n-1) + Fib(n-2);
}
int main() {
    int n = 0;
    scanf("%d", &n);
    int ret = Fib(n);
    printf("%d\n", ret);
    return 0;
}
```

### 斐波那契数列（迭代版）

```C
#include<stdio.h>
int Fib(int n) {
    int a = 1, b = 1, c = 1;
    while (n >= 3) {
        c = a + b;
        a = b; b = c;
        n--;
    }
    return c;
}
int main() {
    int n = 0;
    scanf_s("%d", &n);
    int ret = Fib(n);
    printf("%d", ret);
    return 0;
}
```

### 计算一个数字的各位之和

```C
#include<stdio.h>
int DigitSum(int n) {
    if (n == 0) return 0;
    else return (n % 10) + DigitSum(n / 10);
}
int main() {
    int n = 0;
    scanf_s("%d", &n);
    int ret = DigitSum(n);
    printf("%d\n", ret);
    return 0;
}
```

### 阶乘（递归版）

```C
#include<stdio.h>
int factorial(int n) {
    if (n == 0) return 1;
    else return n * factorial(n - 1);
}
int main() {
    int n = 0;
    scanf_s("%d", &n);
    int ret = factorial(n);
    printf("%d的阶乘是%d", n, ret);
    return 0;
}
```

### 阶乘（迭代版）

```C
#include<stdio.h>
int i = 0, ret = 1;
int factorial(int n) {
    for (i = 1; i <= n; i++) ret *= i;
    return ret;
}
int main() {
    int n = 0;
    scanf_s("%d", &n);
    int ret = factorial(n);
    printf("%d的阶乘是:%d\n", n, ret);
    return 0;
}
```

### 顺序打印一个整数的每一位

```C
#include <stdio.h>
void print(int n) {
    if (n > 9) { print(n / 10); printf(" %d", n % 10); }
    else printf(" %d", n);
}
int main() {
    int n = 0;
    printf("请输入要拆分的数字:"); scanf_s("%d", &n);
    printf("该数字的每一位是:"); print(n);
    return 0;
}
```

## 位操作

### 统计二进制中 1 的个数（逐位法）

```C
#include<stdio.h>
int main() {
    int n = 0, count = 0;
    scanf_s("%d", &n);
    for (int i = 0; i <= 32; i++) {
        if ((n & 1) == 1) count++;
        n >>= 1;
    }
    printf("%d\n", count);
    return 0;
}
```

### 统计二进制中 1 的个数（n & (n-1) 法）

```C
#include<stdio.h>
int main() {
    int n = 0;
    scanf_s("%d", &n);
    int count = 0;
    while (n) { n = n & (n - 1); count++; }
    printf("%d\n", count);
    return 0;
}
```

### 不创建临时变量交换两个整数

```C
#include<stdio.h>
int main() {
    int a = 10, b = 20;
    a = a ^ b; b = a ^ b; a = a ^ b;
    printf("a的值是:%d b的值是:%d", a, b);
    return 0;
}
```

### 统计两个数二进制位不同的个数

```C
#include<stdio.h>
int main() {
    int a = 0, b = 0, count = 0;
    printf("两个数分别是:"); scanf_s("%d %d", &a, &b);
    int n = a ^ b;
    while (n) { n = n & (n - 1); count++; }
    printf("%d", count);
    return 0;
}
```

## 字符串函数实现

### my_strlen

```C
#include <stdio.h>
size_t my_strlen(const char* str) {
    if (*str == '\0') return 0;
    else return 1 + my_strlen(str + 1);
}
int main() {
    char str[100];
    printf("请输入一个字符串: "); scanf_s("%s", str, sizeof(str));
    size_t length = my_strlen(str);
    printf("字符串的长度是: %zu\n", length);
    return 0;
}
```

### my_strcpy

```C
#include<stdio.h>
#include<assert.h>
char* my_strcpy(char* dest, const char* src) {
    char* ret = dest;
    assert(dest != NULL && src != NULL);
    while (*src != '\0') { *dest++ = *src++; }
    *dest = *src;
    return ret;
}
```

改进版：

```C
while(*dest++ = *src++) { ; }
// \0 赋值给 *dest 后，ASCII 码为 0，while(0) 终止循环
```

### my_strcat

```C
#include<stdio.h>
#include<assert.h>
char* my_strcat(char* dest, const char* src) {
    char* ret = dest;
    assert(dest && src);
    while (*dest) dest++;
    while (*dest++ = *src++) { ; }
    return ret;
}
int main() {
    char arr1[20] = "hello";
    char arr2[] = " world";
    my_strcat(arr1, arr2);
    printf("%s\n", arr1);
    return 0;
}
```

### my_strcmp

```C
#include<stdio.h>
#include<assert.h>
int my_strcmp(const char* s1, const char* s2) {
    assert(s1 && s2);
    while (*s1 == *s2) {
        if (*s1 == '\0') return 0;
        s1++; s2++;
    }
    if (*s1 < *s2) return -1;
    else return 1;
}
int main() {
    char arr1[] = "abcdef";
    char arr2[] = "abcdeg";
    int r = my_strcmp(arr1, arr2);
    if (r > 0) printf(">");
    else if(r < 0) printf("<");
    else printf("=");
    return 0;
}
```

### my_strstr

```C
#include<stdio.h>
char* my_strstr(const char* str1, const char* str2) {
    const char* cp = str1;
    const char* s1, *s2;
    if(*str2 == '\0') return (char*)str1;
    while (*cp) {
        s1 = cp; s2 = str2;
        while (*s1 != '\0' && *s2 != '\0' && *s1 == *s2) { s1++; s2++; }
        if (*s2 == '\0') return (char*)cp;
        cp++;
    }
    return NULL;
}
int main() {
    char arr1[] = "abcdefg";
    char arr2[] = "defg";
    char* ps = my_strstr(arr1, arr2);
    if (ps != NULL) printf("%s\n", ps);
    else printf("Not found\n");
    return 0;
}
```

|指针|角色|作用|
|-|-|-|
|`cp`|定位指针（外层）|记录当前尝试匹配的起始位置|
|`s1`|遍历指针（内层）|从 cp 开始逐个字符与 s2 比较|
|`s2`|遍历指针（内层）|指向子串的当前位置|

## 指针与数组

### 交换两个数（传址调用）

```C
#include<stdio.h>
void swap1(int* px, int* py) {
    int temp = 0;
    temp = *px; *px = *py; *py = temp;
}
int main() {
    int a = 0, b = 0;
    printf("请输入a b的值:"); scanf_s("%d %d", &a, &b);
    printf("交换前:a=%d b=%d\n", a, b);
    swap1(&a, &b);
    printf("交换后:a=%d b=%d\n", a, b);
    return 0;
}
```

### 指针遍历数组

```C
#include<stdio.h>
int main() {
    int arr[10] = { 0 };
    int* p = arr;
    int sz = sizeof(arr) / sizeof(arr[0]);
    for (int i = 0; i < sz; i++) { *p = i + 1; p++; }
    p = arr;
    for (int i = 0; i < sz; i++) printf("%d ", *(p + i));
    return 0;
}
```

小结：`arr[i] == *(arr + i) == *(p + i)`，通过加法交换律 `i[arr] == *(i + arr)`。

### 指针数组模拟二维数组

```C
#include<stdio.h>
int main() {
    int arr1[] = { 1,2,3,4,5 };
    int arr2[] = { 2,3,4,5,6 };
    int arr3[] = { 3,4,5,6,7 };
    int* arr[3] = { arr1,arr2,arr3 };
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 5; j++)
            printf("%d ", arr[i][j]);
        printf("\n");
    }
    return 0;
}
```

### 二维数组传参

```C
#include<stdio.h>
void print(int(*arr)[5], int r, int c) {
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++)
            printf("%d ", arr[i][j]);
        printf("\n");
    }
}
int main() {
    int arr[3][5] = { {1,2,3,4,5},{2,3,4,5,6},{3,4,5,6,7} };
    print(arr, 3, 5);
    return 0;
}
```

`arr[i][j] = *(*(arr + i) + j) = *(arr[i] + j)`

## 排序

### 冒泡排序

```C
#include<stdio.h>
void bubble_sort(int arr[], int sz) {
    for (int i = 0; i < sz - 1; i++) {
        for (int j = 0; j < sz - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
}
```

### 冒泡排序优化版

```C
void bubble_sort(int arr[], int sz) {
    for (int i = 0; i < sz - 1; i++) {
        int flag = 1;
        for (int j = 0; j < sz - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                flag = 0;
                int tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
        if (flag == 1) break;
    }
}
```

## 函数指针

### 函数指针数组实现计算器

```C
#include<stdio.h>
void menu() {
    printf("----------1.Add      2.sub----------\n");
    printf("----------3.mul      4.div----------\n");
    printf("---------------0.exit---------------\n");
}
int Add(int x, int y) { return x + y; }
int sub(int x, int y) { return x - y; }
int mul(int x, int y) { return x * y; }
int div(int x, int y) {
    if (y == 0) { printf("除数不能为0"); return 0; }
    else return x / y;
}
int main() {
    int input = 0, x = 0, y = 0, ret = 0;
    int(*p[])(int, int) = { NULL,Add,sub,mul,div };
    do {
        menu();
        printf("请选择-->"); scanf_s("%d", &input);
        if (input >= 1 && input <= 4) {
            printf("请输入两个操作数:"); scanf_s("%d%d", &x, &y);
            ret = (*p[input])(x, y);
            printf("%d\n", ret);
        }
        else if (input == 0) printf("退出计算机");
        else printf("请输入0-4的数字");
    } while (input);
    return 0;
}
```

### 回调函数实现计算器

```C
#include<stdio.h>
void calc(int (*pf)(int, int)) {
    int x = 0, y = 0, r = 0;
    printf("请输入操作数:"); scanf_s("%d %d", &x, &y);
    r = pf(x, y);
    printf("计算的结果是:%d\n", r);
}
int main() {
    int input = 0;
    do {
        menu();
        printf("请选择:"); scanf_s("%d", &input);
        switch (input) {
        case 1: calc(Add); break;
        case 2: calc(sub); break;
        case 3: calc(mul); break;
        case 4: calc(div); break;
        case 0: printf("退出程序\n"); break;
        default: printf("程序错误\n"); break;
        }
    } while (input);
    return 0;
}
```

## 通用冒泡排序（qsort风格）

```C
#include <stdio.h>

void Swap(char* p1, char* p2, size_t width) {
    for (size_t i = 0; i < width; i++) {
        char tmp = p1[i];
        p1[i] = p2[i];
        p2[i] = tmp;
    }
}

int cmp_int(const void* p1, const void* p2) {
    return *(int*)p1 - *(int*)p2;
}

void bubble_sort2(void* base, size_t sz, size_t width, int (*cmp)(const void*, const void*)) {
    for (size_t i = 0; i < sz - 1; i++) {
        for (size_t j = 0; j < sz - 1 - i; j++) {
            char* p1 = (char*)base + j * width;
            char* p2 = (char*)base + (j + 1) * width;
            if (cmp(p1, p2) > 0) Swap(p1, p2, width);
        }
    }
}

void test4() {
    int arr[] = {8,7,6,5,4,3,2,9,1,0};
    int sz = sizeof(arr) / sizeof(arr[0]);
    bubble_sort2(arr, sz, sizeof(arr[0]), cmp_int);
    for (int i = 0; i < sz; i++) printf("%d ", arr[i]);
}
```

|参数|作用|
|-|-|
|`base`|数组起始地址|
|`sz`|元素个数|
|`width`|每个元素大小（字节）|
|`cmp`|比较函数的指针|

## 内存操作

### my_memcpy

```C
#include<stdio.h>
#include<assert.h>
void* my_memcpy(void* dest, const void* src, size_t sz1) {
    void* ret = dest;
    assert(dest && src);
    while (sz1--) {
        *(char*)dest = *(char*)src;
        dest = (char*)dest + 1;
        src = (char*)src + 1;
    }
    return ret;
}
```

### my_memmove

```C
#include<stdio.h>
#include<assert.h>
void* my_memmove(void* dest, const void* src, size_t num) {
    void* ret = dest;
    assert(dest && src);
    if (dest < src) {
        while (num--) {
            *(char*)dest = *(char*)src;
            dest = (char*)dest + 1;
            src = (char*)src + 1;
        }
    } else {
        while (num--) {
            *((char*)dest + num) = *((char*)src + num);
        }
    }
    return ret;
}
```

### strtok 使用示例

```C
#include<stdio.h>
#include<string.h>
int main() {
    char arr[] = "zhangxuefeng@qiaolezi.xuebi";
    const char* p = "@.";
    char buf[30] = { 0 };
    strncpy(buf, arr, 30);
    char* pr = NULL;
    for (pr = strtok(buf, p); pr != NULL; pr = strtok(NULL, p))
        printf("%s\n", pr);
    return 0;
}
```
