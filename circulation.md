#补上一课：循环
##跳转语句 goto
代码:
```c
#include<stdio.h>

int main() {
begin:
  printf("I'm looping\n");
  goto begin;
  return 0;
}
```
你会看到屏幕上停地输出`I'm looping`（可以按ctrl+c停止），我们已经实现了一个最简单的循环。

1. `begin:`我在这里标注了一个名叫begin的标签。相当于我在代码的这个地方做了一个记号。
2. `goto beigin;`这里使用了goto语句，和英语的意思一模一样 go to 去那里，也就是说程序跳转到了begin的位置。
于是乎 `printf`->`goto begin`->`printf`->...... 子子孙孙无穷尽也，这也便是最简单的循环。

但是这样只能做到无限循环，但我们往往还是需要正常退出的，于是我们可以结合条件语句来做到有条件的循环。
（第一种）
```c
#include<stdio.h>

int main() {
  int i = 0;
begin:
  printf("I'm looping if you want me to\n");
  i = i + 1;
  if (i < 10)
    goto begin;
  return 0;
}
```
现在再运行，便只输出了10条语句。
事实上这与我们熟悉程序框图可以一一对应。
  i = 0 -> printf -> i = i + 1 -> if(1<10) -> goto begin -
    -> printf -> i = i + 1 -> if(2<10) -> .... -> if(10<10) -> 结束

前面那个程序还有另一种写法，但结果完全一样：
（第二种）
```c
#include<stdio.h>

int main() {
  int i = 0;
begin:
  if(i<10) {
    printf("I'm looping if you want me to\n");
    i = i + 1;
    goto begin;
  }
  return 0;
}
```
这样也只是改变了判断条件的位置。
  i = 0 -> if(0<10) -> printf -> i = i + 1 -> goto begin -
    -> if(1<10) -> printf -> .... -> if(10<10) -> 结束


而使用goto语句必须要使用标签，而且标签的名字都是不能重复的，这样不免有些麻烦，因此C语言有几种专门的循环语句可以帮助我们更方便地写代码。

## while循环
while循环实际与第二种循环类似
格式为
```c
while(condition)
  statement||block
```
他是先判断contition若为真则运行stetement||block否则就直接执行后面的代码
之前那个程序用while改写便为：
```c
int main() {
  int i = 0;
  while (i < 10) {
    printf("I'm looping if you want me to\n");
    i = i + 1;  
  }
  return 0;
}
```
仔细观察它与第二种goto的循环其实一一对应

## do - while 循环
do - while 格式如下：
```c
do
  statement||block
while(condition);
```
**注意：C语言为了避免歧义，do while循环最后是有`;`结尾的！**
它与while循环十分相似，只是判断的部分在后面，是先运行一次代码再判断。
用它来改写便是：
```c
int main() {
  int i = 0;
  do {
    printf("I'm looping if you want me to\n");
    i = i + 1;
  }while(i < 10);
  return 0;
}
```
仔细观察它也是与第一种goto循环一一对应。

### while 与 do - while 有什么区别？
 最大的区别就是判断的位置，假设之前那个程序第一行改成 `int i = 100;` 再运行就会发现:
  + 用while循环的什么也没输出就退出了
  + 用do - while循环的输出了一句然后才退出

## for 循环
之前我们的循环都是用计数的，而c语言其实有一个更方便的方法做计数循环——for循环：
格式如下
```c
for(变量初始值;条件;变量增加)
  statement||block
```
具体用它来改写就是这样
```c
int main() {
  for(int i = 0;i < 10;i = i + 1)
    printf("I'm looping if you want me to\n");
  return 0;
}
```
这样看起来便更加简洁了。
注意:
+ for循环的判断条件和while一样是在运行前判断，所以里面的代码可能不会执行
+ for循环的变量增加是在运行完代码块后增加的
其实for循环前三个分号内的内容都是可选的，也就是说 其实可以这么写：
```c
int main() {
  int i = 0;
  for(;i < 10;) {
    printf("I'm looping if you want me to\n");
    i = i + 1
  }
  return 0;
}
```
实际上与while循环很像，而且 **大部分** 情况下可以替换。书上说for循环和while循环无条件等价是 **非常错误*** 的！！！

## 一些控制语句
为了更灵活，c中还有一些循环控制语句（这些语句也是结尾要加`;`号的）
### continue
`continue;`语句作用是跳过本次循环，并开始下一次循环（所以的条件都还是会判断，不达到条件会结束循环）
 + while 、 do while循环中，它将直接跳过后面所以的语句，包括`i = i + 1`这样的自增语句，如果没考虑清楚可能会造成死循环！
 + for循环中，如果把自增语句写在了`for(;;)`结构中，自增语句是不会被跳过的。
所以 **在用变量计数的循环中，用for语句更加安全。**
### break
`break;`语句能直接跳出循环，直接运行之后的代码
### return
`return value;`返回值时，直接结束了当前函数，也就跳出了当前循环。
### goto
`goto lable;`goto语句能跳到函数内的任何一个标签，使用它要注意安全，以免脑乱导致错误的结果。
