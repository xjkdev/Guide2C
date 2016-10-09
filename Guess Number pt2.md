#猜数游戏 第二部分
学习完了循环，我们便可以完善我们的猜数游戏了

## Version 0.05
```c
#include<stdio.h>

#define random_number 666

int main() {
  int guess;
  for(int i = 0;i<10;i++) {
    printf("Please input your guess:");
    scanf("%d",&guess);  
    if(guess == random_number) //判断是否相等
      printf("You win\n"); //相等玩家就赢了
    else {
      if(guess > random_number)
        printf("Too high\n"); //太高
      else
        printf("Too low\n"); //太低
    }
  }
  return 0;
}
```

## Version 0.06
我们到现在都用的只是一个固定的数，而这样就没有游戏的意义了。让我带你们用一些新的库和函数，完善它。
```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

int main() {
    int guess, random_number;

    //生成随机数的代码
    srand(time(NULL));
    random_number = rand()%1000;

    for (int i = 0; i<10; i++) {
        printf("Please input your guess:");
        scanf("%d", &guess);
        if (guess == random_number) //判断是否相等
            printf("You win\n"); //相等玩家就赢了
        else {
            if (guess > random_number)
                printf("Too high\n"); //太高
            else
                printf("Too low\n"); //太低
        }
    }
    return 0;
}
```
我引用了两个库
1. 以后经常会用到的stdlib.h，其中包含了`srand`、`rand`函数，这两个函数用来生成伪随机数。
2. time.h包含了一些和时间有关的函数，其中用到了`time`函数，用来获取当前时间
我解释一下这些函数：
1. `rand`函数生成一个伪随机数
2. `srand`函数，生成一个随机种子，如果不调用这个函数，`rand`生成的随机数每次都是一样的。
3. `time`函数，获取的是从1970年1月1日0点0分0秒起至今的总秒数。

用当前的时间去生成随机种子，便可以使每次随机出来的随机数都不一样。
至此我们的猜数游戏就完成了！
