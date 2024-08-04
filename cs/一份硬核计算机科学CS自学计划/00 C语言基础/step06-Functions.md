# 开始

创建一个 combi.c 文件，放入下列代码
```c
#include <math.h>
#include <stdio.h>
#include <stdlib.h>

/*
 * Name : <qimo090>
 * Program to determine combinations
 */

int main() {
  int n;
  int k;
  int b;

  printf("Input n: ");
  scanf("%d", &n);
  if (n < 1) {
    printf("Must be greater than zero\n");
    exit(1);
  }

  printf("Input k: ");
  scanf("%d", &k);
  if (k < 0 || k > n) {
    printf("Must be between 0 and %d inclusive\n", n);
    exit(1);
  }
}
```

然后编译代码
```shell
gcc -o combi -lm combi.c
```
最后运行代码
```shell
./combi
```
# 1. 组合

如果给你一副扑克牌，可以从五张牌中抽出多少种可能的手牌？此类问题使用二项式系数求解：
$$\binom{n}{k}$$
数学上，二项式系数定义为：
$$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$
所以我们创建一个阶乘函数如下，放在 combi.c 底部, 和 main 函数平级

```c
// int main() {
//    ...
// }

/* Factorial Function */  
int Factorial(int n) {  
    int f = 1;  
    int i;  
    for(i = 1; i <= n; i++) {  
        f *= i;  
    }  
    return f;  
}
```