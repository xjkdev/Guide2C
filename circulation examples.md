# 一些循环举例

## 数列求和

### 1+2+3+...+100
```c
#include<stdio.h>

int main() {
  int sum = 0;
  for(int i = 1;i<=100;i++) {
    sum += i;
  }
  printf("sum is %d\n",sum);
  return 0;
}
```
其中我用了两种常用的简便写法，今后我也会经常这么写
+ `i++` 相当于 `i = i + 1` （我之后还会讲到它，它比这个还要复杂一些，现在请只在for循环的自增处使用它）
+ `sum += i` 等同于 `sum = sum + i`同理 `a -= b` 等同于 `a = a - b`，`a *= b` 等同于 `a = a * b`

### 累加器(输入0退出)
```c
#include<stdio.h>

int main() {
  int sum = 0;
  int i;
  while(1){ //常用法，表示无限循环
    scanf("%d",&i);
    if(i == 0)
      break;
    sum += i;
    printf("You input %d and sum is %d\n",i,sum);
  }
  printf("The loop is breaked\n");
  return 0;
}
```

### 累加器（只加偶数）
```c
#include<stdio.h>

int main() {
  int sum = 0;
  int i;
  while(1){
    scanf("%d",&i);
    if(i == 0)
      break;
    if(i % 2 == 1) { //常用法 判断奇数
      printf("%d is an odd,sum is %d\n",i,sum);
      continue;
    }
    sum += i;
    printf("You input %d and sum is %d\n",i,sum);
  }
  printf("The loop is breaked\n");
  return 0;
}
```

### 判断质数
```c
#include<stdio.h>

int main() {
  int num;
  printf("input a number:");
  scanf("%d", &num);
  for(int i = 2;i * i <= num;i++){
    if(num % i == 0) {
      printf("%d is not an prime number\n",num);
      return 0;
    }
  }
  printf("%d is an prime number\n",num);
  return 0;
}
```
