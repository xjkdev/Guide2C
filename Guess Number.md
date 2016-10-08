#猜数游戏
让我们来实现一个简单的小游戏，并通过这个程序来学习变量和控制语句。

##Version 0.01
我们先学习如何接收用户输入的字符：
```c
#include<stdio.h>

int main() {
  int number;
  printf("Please input a number:");
  scanf("%d",&number);
  printf("You input %d\n",number);
  return 0;
}
```
嗯，假设我输入了2333,你将看到
```
Please input a number:2333
You input 2333
```
1. `int number;`我定义了一个变量number,用来储存用户输入的数据。
2. `scanf("%d",&number);`这句与printf类似，%d表示我期望用户输入一个整数。这里注意一下：
 1. 这里的参数就不能像printf一样用普通数字了，必须是一个变量名。
 2. 变量名之前一定要写`&`，我们今后会解释它。
 3. scanf只有在用户按回车之后才会读取数字

##Version 0.02
我用骰子摇出了一个随机数：666，只要用户猜对了我的数字他就赢了。
我先用`#define`来定义一个常量。#define的格式为 #define [空格] *常量名* [空格] *常量值*,之后random_number便用来代表666这个数字。

```c
#include<stdio.h>

#define random_number 666

int main() {
  int guess;
  printf("Please input your guess:");
  scanf("%d",&guess);  
  //to be continue
}
```
慢着，我们怎么判断guess的值和random_number的值是否相等？
让我介绍c中的一些与比较有关的知识

1.由于c发明的时候比较古老，所以c中并没有bool型<sup>注1</sup>。c中逻辑值用整形表示。
   + 0是逻辑假
   + 其他的任何值都是真。
  c没有true和false常量，所以有一下常用法：
  ```
  #define true 1
  #define false 0
  ```

2.c中比较两个数用以下运算符
  + == 等于（**注意！ 必须是两个等号，一个等号是赋值号，比较两个数只使用一个等号是常见的错误原因之一**）
  + != 不等于
  + > >= 大于 大于等于
  + < <= 小于 小于等于
  例如：
   + 1 == 1 => 1
   + 1 == 0 => 0
   + 2 > 1 => 1
   + 2 >= 1 => 1
   + 2 >= 2 => 1
   注意c中不能 `1<x<2` 这样连写

3.另外c中有以下逻辑运算符
  + || 逻辑或
  + && 逻辑与
  + !  逻辑非
  例如：
   + !1 => 0
   + !0 => 1
   + 1 || 0 => 1
   + 1 && 0 => 0
  这些运算符的顺序都低于之前打大于小于等于运算符，所以可以这样：`1 <= x && x <= 2`，在 1 <= x 和 x <= 2外面可以不用加括号

  但我不推荐去背这几个逻辑运算符的顺序，需要连用时就加括号。例如: `(1 <= x && x <= 2) || (1 <= y && y <= 2)`这样看起来逻辑更加清晰，可读性更强。

知道了这些运算符之后 我们就可以学习if语句了。

if 语句用法如下（condition是条件，statements是多条语句，statement为单条语句）
```c
if(condition) {
  statements
}else if (condition){
  statements
}else {
  statements
}
```
如果花括号中只有一条语句可以省略花括号例如 if(condtion) statement;
注意：
 + if 语句花括号后面没有`;`号
 + if 语句只有if(conditions) { statements }必须有，其他的均为可选
 + else if 语句可以有不只一行
 + else 语句必须放最后
为了简便说明，今后{statments}我都用 block（语句块）代替，如果可以用单条语句替换我便写 statement||block
所以if语句的格式便为
1. 必选 if(condition) statement||block
2. 没有或一条或多条 else if(condition) statement||block
3. 没有或一条 else statement||block

所以我们的代码又可以扩展一些了：
```c
#include<stdio.h>

#define random_number 666

int main() {
  int guess;
  printf("Please input your guess:");
  scanf("%d",&guess);  
  if(guess == random_number) //判断是否相等
    printf("You win\n"); //相等玩家就赢了
  else
    printf("You lose\n"); //不相等玩家就输了
  return 0;
}
```

#Version 0.03
（练习if语句）
有玩家反映我们的程序太难了，只能猜一次，所以我决定放低难度，告诉玩家猜的是大还是小：
```c
#include<stdio.h>

#define random_number 666

int main() {
  int guess;
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
  return 0;
}
```

#Version 0.04
还是有玩家猜不出来，于是我决定让玩家猜3次：
```c
#include<stdio.h>

#define random_number 666

int main() {
  int guess;
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
  return 0;
}
```

#Version 0.05
还是有玩家猜不出来，于是我决定让玩家猜5次：
再多复制两次？
真傻！还有循环呢！


这个程序还有些bug，但只有学习完了控制语句才能解决。
***未完待续***

注1：C99标准定义了bool型但要引用stdbool.h才能使用，这个文件同时定义了true和false
