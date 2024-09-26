# C语言程序设计 现代方法

[美]K.N.金（K. N. King）

###### TODO:

```
第二章 C语言基本概念
```

## 第一章 C语言概述

### 1.1 C语言的历史

#### 1.1.1 起源

![image-20240921193824862](.\C语言程序设计现代方法.assets\image-20240921193824862.png)

#### 1.1.2 标准化

K&B -> C89/C90 -> C99 -> C11 -> C18

#### 1.1.4 基于C的语言

- C++：包括了所有C的特性，增加了类和其他特性以支持面向对象编程
- Java：基于C++
- C#：由C++和Java发展起来
- Perl：最初是一种简单的脚本语言，发展过程中采用了C的许多特性

### 1.2 C语言的优缺点

源于C语言的最初用途（编写操作系统和其他系统软件）和自身的基础理论体系.

- C语言是一种底层语言：C 语言提供了对机器级概念（如字节和地址）的访问（为了适应系统编程的需要）、与计算机内置指令紧密协调的操作，使得程序可以快速执行.
- C语言是一种小型语言：为了保持较少量的特性，C语言在很大程度上依赖一个标准函数的“库”.
- C语言是一种包容性语言：C语言提供了比其他许多语言更高的自由度，此外C语言不像其他语言那样强制进行详细的错误检查.

#### 1.2.1 C语言的优点

- 高效：发明C语言就是为了编写那些以往由汇编语言编写的应用程序
- 可移植：C程序具有可移植性的一个原因是该语言没有分裂成不兼容的多种分支（归功于C语言早期与UNIX系统的结合以及后来的ANSI/ISO标准）；另一个原因是C语言编译器规模小且容易编写；C语言自身的特性也支持可移植性（尽管它没有阻止程序员编写不可移植的程序）
- 功能强大：C语言拥有一个庞大的数据类型和运算符集合，使得C语言具有强大的表达能力
- 灵活：C语言现在可以用于编写从嵌入式系统到商业数据处理的各种应用程序；C语言在其特性使用上的限制非常少，在其他语言中认定为非法的操作在C语言中往往是允许的，如C语言允许一个字符与一个整数值/浮点数相加
- 标准库：~包含了数百个可以用于输入/输出、字符串处理、存储分配以及其他实用操作的函数
- 与UNIX系统的集成：C语言在与UNIX系统（包括Linux）结合方面特别强大

#### 1.2.2 C语言的缺点

C语言的缺点和它的许多优点是同源的，均来自C语言与机器的紧密结合

- C程序更容易隐藏错误
- C程序可能会难以理解
- C程序可能会难以修改

---

C语言混乱代码大赛（International Obfuscated C Code Contest, IOCCC） 1991年的“最佳小程序”

功能是打印出八皇后问题的全部解决方案

```c
v,i,j,k,l,s,a[99];
main()
{
    for(scanf("%d",&s);*a-s;v=a[j*=v]-a[i],k=i<s,j+=(v=j<s&&
(!k&&!!printf(2+"\n\n%c"-(!l<<!j)," #Q"[l^v?(l^j)&1:2])&&
++l||a[i]<s&&v&&v-i+j&&v+i-j))&&!(l%=s),v||(i==j?a[i+=k]=0:
++a[i])>=s*k&&++a[--i])
    ;
}
```

---

#### 1.2.3 高效地使用C语言

- 学习如何避免C语言的缺陷：可以参考《C陷阱与缺陷》
- 使用软件工具使程序更加可靠：lint可以对程序进行更加广泛的错误分析，一般由UNIX系统提供
- 利用现有的代码库
- 采用一套切合实际的编码规范：采纳某些规范并且坚持使用它们
- 避免“投机取巧”和极度复杂的代码：编码应该相当简洁但仍然易于理解
- 紧贴标准：若非却有必要，最好避免使用C编译器提供的不属于C89、C99或C1X标准的特性和库函数

## 第二章 C语言基本概念

### 2.1 编写一个简单的C程序

程序：显示双关语

---

pun.c

```c
#include <stdio.h>

int main(void)
{
    printf("To c, or not to C: that is the question.\n");
    return 0;
}
```

#### 2.1.1  编译和链接

运行需要把pun.c程序转化为机器可以执行的形式，对C程序来说，转化通常包含下列3个步骤：

- 预处理：首先程序被交给预处理器（preprocessor），~执行以#开头的命令（通常称为指令）；预处理器有点类似于编辑器，它可以给程序添加内容，也可以修改程序
- 编译：修改后的程序进入编译器，~把程序翻译成机器指令（即目标代码），这时程序还是不可运行的
- 链接：最后，链接器（linker）把由编译器产生的目标代码和所需的其他附加代码整合到一起，产生完全可执行的程序；这些附加代码包括程序中用到的库函数（如printf函数）

![image-20240922145221949](.\C语言程序设计现代方法.assets\image-20240922145221949.png)

上述过程往往是自动实现的；预处理器通常会和编译器集成在一起

UNIX系统中通常把C编译器命名为 cc ，编译和链接pun.c程序需要在终端或命令行窗口输入：

```
% cc pun.c
```

（字符 % 是UNIX系统的提示符，不需要输入）使用编译器 cc 时，系统自动进行链接操作；编译和链接好后，编译器cc会把可执行程序放到默认名为a.out的文件中；编译器cc的 -o 选项允许为含有可执行程序的文件选择 名字

```
% cc -o pun pun.c
```

---

GCC

GCC是最流行的C编译器之一，随Linux发行，使用与传统的UNIX cc编译器相似

```
% gcc -o pun pun.c
```

GCC最初是GNU C Compiler的简称，现指GNU Compiler Collection，因为最新版GCC能编译用Ada, C, C++, Fortran, Java和Objective-C等多种语言编写的程序

GCC由多个命令行选项来控制程序检查的彻底程度

- -Wall                                      使编译器在检测到可能的错误时生成警告消息（-W  后面可以加上具体的警告代码
                                                              -Wall 表示“所有的-W选项”）为了获得最好的效果，-Wall应与-O选项结合使用
- -W                                            除了-Wall生成的警告消息外，还需要针对具体情况的额外警告消息
- -pedantic                              根据C标准的要求生成警告消息。这样可以避免在程序中使用非标准特性
- -ansi                                        禁用GCC的非标准C特性，并启用一些不太常用的标准特性
- -std=c89或-std=c99        指明使用哪个版本的C编译器来检查程序

这些选项通常可以结合使用：

```
% gcc -O -Wall -W -pedantic -std=c99 -o pun pun.c
```

#### 2.1.2集成开发环境

集成开发环境（integrated development environment, IDE）是一个软件包，可以在其中编辑、编译、链接、执行甚至调试程序

### 2.2 简单程序的一般形式

简单的C程序一般具有如下形式：

```c
指令

int main(void)
{
    语句
}
```

即使是最简单的C程序也依赖3个关键的语言特性：

- 指令（在编译前修改程序的编辑命令）
- 函数（被命名的可执行代码块，如main函数）
- 语句（程序运行时执行的命令）

#### 2.2.1 指令

预处理器执行的命令称为指令

\#include <stdio.h>这条指令说明，在编译前把<stdio.h>中的信息“包含”到程序中

<stdio.h>包含C标准输入/输出库的信息

C语言拥有大量类似于<stdio.h>的头（header），每个头都包含一些标准库的内容

C语言没有内置的“读”和“写”命令，输入/输出功能由标准库中的函数实现

所有指令都是以字符#开头的，#可以把C程序中的指令和其他代码区分开，指令默认占一行，结尾没有分号或其他特殊标记

#### 2.2.2 函数

函数分为两大类：一类是程序员编写的函数，另一类是作为C语言实现的一部分提供的函数，后者称为库函数（library function），因为他们属于一个由编译器提供的函数“库”

计算数值的函数用return语句来指定所“返回”的值

一个C程序可以包含多个函数，但只有main函数是必须有的，在执行程序时系统会自动调用main函数；main函数会在程序终止时向操作系统返回一个状态码。

语句 return 0 有两个作用：一是使 main 函数终止（从而结束程序），二是指出main函数的返回值是0；当exit(0)语句出现在main函数中时和return 0语句等价

如果main函数的末尾没有return语句，程序仍然能终止，但许多编译器会产生一条警告信息；在C89中，返回给操作系统的值是未定义的，在C99中，如果main函数声明中的返回类型是int，程序会向操作系统返回0，否则程序会返回一个不确定的值

#### 2.2.3 语句

语句是程序运行时执行的命令，程序pun.c只用到两种语句：一种时返回（return）语句，另一种时函数调用（function call）语句；要求某个函数执行分派给它的任务称为调用这个函数。

C语言规定每条语句都要以分号结尾（复合语句不以分号结尾），指令通常只占一行不需要用分号结尾

#### 2.2.4 显示字符串

字面串（string literal）是用一对双引号包围的一系列字符

printf函数不会自动跳转到下一输出行，需要在要显示的字符串中包含 \n（换行符）

```
printf("To C, or not to C: that is the question.\n");
//效果等同于
printf("To C, or not to C: ");
printf("that is the question.\n");
```

换行符可以在一个字面串中出现多次：

```
printf("Brevity is the soul of wit.\n  --ShakeSpeare\n");
//Brevity is the soul of wit.
//  --Shakespeare
```

### 2.3 注释

每一个程序都应该包含识别信息，即程序名、编写日期、作者、程序的用途以及其他相关信息，C语言把这类信息放在注释（comment）中；符号 /* 标记注释的开始，符号 /* 标记注释的结束

```
/* This is a comment */
```

注释几乎可以出现在程序的任何位置上，可以独占一行，也可以和其他程序文本出现在同一行中

注释还可以占用多行：

```
/* Name: pun.c
   Purpose: Prints a bad pun.
   Author: K. N. King
*/
```

C99提供了另一种类型的注释，以 // （两个相邻的斜杠）开始，这种会在行末自动终止

```
// This is a comment
```

传统风格的注释/\*...\*/不允许嵌套，C99（//）注释可以嵌套在传统风格注释中

### 2.4 变量和赋值

在程序执行过程中临时存储数据的这类存储单元被称为变量（variable）

#### 2.4.1 类型

每一个变量必须有一个类型（Type），用来说明变量所存储的数据的种类

int（integer的简写）型变量可以存储整数，如0、1、392或-2553，但取值 范围是受限制的，最大整数通常为2 147 483 647，某些计算机上也可能是32 767

float（即floating-point的简写）型变量可以存储比int型变量大得多的数值，并且可以存储带小数位的数，如379.125；float型变量所存储的值往往只是实际数值的一个近似值

#### 2.4.2 声明

在使用变量之前必须对其进行声明（为编译器所作的描述），首先指定变量的类型，然后说明变量的名字

```
int height;
float profit;
```

如果几个变量有相同的类型可以把它们的声明合，每一条完整的声明都要以分号结尾

```
int height, length, width, volume;
float profit, loss;
```

当main函数包含声明时，必须把声明放置在语句之前：

```
int main(void)
{
    声明
    语句
}
```

在C99中，声明可以不在语句之前

#### 2.4.3 赋值

变量通过赋值（assignment）的方式获得值

```
height = 8;
length = 12;
width = 10;
```

把数值8...分别赋值给height...；8, 12, 10称为常量（constant）

变量在赋值或以其他方式使用之前必须先声明：

```
int height;
height = 8;
//------------------
height = 8;    /** WRONG **/
int height;
```

当把一个包含小数点的常量赋值给float型变量时，最好在该常数后面加一个字符 f（代表float）；包含小数点但不以f结尾的常量是double（double precision的缩写）型的，double型的值比float型的值存储得更加精确，并且比float型的值大，如果在给float型变量赋值时不加f，编译器可能会生成一条警告消息告诉你存储到float型变量中的数可能超出了该变量的取值范围

```
profit = 2150.48f
```

混合类型赋值（例如把int型的 值赋给float型变量，或反过来）是可以的，但不一定安全

赋值运算的右侧可以是一个含有常量、变量和运算符的公式（在C语言的术语中称为表达式）

#### 2.4.4 显示变量的值

```
printf("Height: %d\n", height);
```

占位符%d用来指明在显示过程中变量height的值的显示位置。

%d仅用于int型变量；%f用于float型变量，默认显示小数点后6位数字，如果要强制%f显示小数点后p位数字，可以把 .p放置在%和 f 之间

```c
printf("Profit: $%.2f\n", profit);	//Profit: $2150.48
```

#### 2.4.5 初始化

当程序开始执行时，某些变量会被自动设置为零，而大多数变量则不会；没有默认值并且尚未在程序中被赋值的变量是未初始化的（uninitialized）

> 如果试图访问未初始化的变量，可能会得到不可预知的结果，如258、-30 891或者其他没有意义的数值，在某些编译器中可能是发生更坏的情况（甚至是程序崩溃）

除了采用赋值的方法给变量赋初始值，更简便的方法是：在变量声明中加入初始值

```c
int height = 8;
int height = 8, length = 12, width = 10;
int height, length, width = 10;	//只有变量width拥有初始化器10，height和length都没有
```

按照C语言的术语，数值8是一个初始化器（initializer）

#### 2.4.6 显示表达式的值

printf的功能不局限于显示变量中存储的数，它可以显示 任意数值表达式 的值，利用这一特性可以简化程序和减少变量的数量

```c
volume = height * length * widht;
printf("%d\n", volume);
//可以用以下形式代替
printf("%d\n", height * length * widht);
```

printf显示 表达式的值 的能力说明了C语言的一个通用原则：在任何需要数值的地方都可以使用具有相同类型的表达式

### 2.5 读入输入

scanf中的字母f和printf中的字母f含义相同，都表示“格式化”的意思，scanf函数和printf函数都需要使用 格式串（format string）来指定输入数据或输出数据的形式

```c
scanf("%d", &i);	/* reads an integer; stores into i */
scanf("%f", &x);	/* reads a float value; stores into x */
```

### 2.6 定义常量的名字

当程序含有常量时，建议给这些常量命名，以后阅读程序时也许会不明白这些常量的含义，可以采用称为 宏定义（macro definition）的特性给常量命名，还可以利用宏来定义表达式

```c
#define INCHES_PER_POUND 166
#define RECIPROCAL_OF_PI (1.0f / 3.14159f)
```

当宏包含运算符时，建议用括号 () 把表达式括起来；注意宏的名字只用大写字母，这是C程序员沿用了几十年的规范，但并不是C语言本身的要求。

这里的 #define 是预处理指令，类似于 #include，因此行尾也没有分号，当对程序进行编译时，预处理器会把每一个宏替换为其表示的值

```c
weight = (volume + INCHES_PER_POUND - 1) / INCHES_PER_POUND;
// 将变为
weight = (volume + 166 - 1) / 166;
```

程序：华氏温度转换为摄氏温度

---

提示用户输入一个华氏温度，然后输出一个对应的摄氏温度

celsius.c

```c
/* Converts a Fahrenheit temperature to Celsius */

#include <stdio.h>

#define FREEZING_PT 32.0f
#define SCALE_FACTOR (5.0f / 9.0f)

int main(void)
{
    float fahrenheit, celsius;
    
    printf("Enter Fahrenheit temperature: ");
    scanf("%f", &fahrenheit);
    
    celsius = (fahrenheit - FREEZING_PT) * SCALE_FACTOR;
    
    printf("Celsius equivalent: %.1f\n", celsius);
    
    return 0
}
```

在定义SCALE_FACTOR时，表达式采用 (5.0f / 9.0f) 的形式而不是 (5 / 9) 的形式是因为，如果两个整数相除C语言会对结果向下舍入，表达式 (5 / 9) 的值是0

### 2.7 标识符

在编写程序时，需要对变量、函数、宏和其他实体进行命名，这些名字称为 标识符（identifier）

在C语言中，标识符可以含有字母、数字和下划线，但是必须以字母或者下划线开头

【C99中，标识符还可以使用某些“通用字符名】

合法标识符的示例： times10    get_next_char    _done

不合法的标识符：10times    get-next-char

C语言是区分大小写的，C语言对标识符的最大长度没有限制

标识符规范：

1. 只使用小写字母（常见于传统C）：symbol_table    current_page    name_and_address
2. 避免使用下划线，将每个单词用大写字母开头：symbolTable    currentPage    nameAndAddress

###### 关键字

关键字（keyword）对C编译器有着特殊的意义，因此这些关键字不能作为标识符来使用；下面有些关键字是C99新增的，有些是C1X新增的

|   auto   |      extern      |  short   |         while          |
| :------: | :--------------: | :------: | :--------------------: |
|  break   |      float       |  signed  |    _Alignas   (C11)    |
|   case   |       for        |  sizeof  |    _Alignof   (C11)    |
|   char   |       goto       |  static  |    _Atomic   (C11)     |
|  const   |        if        |  struct  |     _Bool   (C99)      |
| continue |  inline   (C99)  |  switch  |    _Complex   (C99)    |
| default  |       int        | typedef  |    _Generic   (C11)    |
|    do    |       long       |  union   |   _Imaginary   (C99)   |
|  double  |     register     | unsigned |   _Noreturn   (C11)    |
|   else   | restrict   (C99) |   void   | _Static_assert   (C11) |
|   enum   |      return      | volatile | _Thread_local   (C11)  |

### 2.8 C程序的书写规范

C语言允许在记号（token，即许多在不改变意思的情况下无法再分割的字符组）之间插入任意数量的间隔，有着以下意义

- 语句可以分开放在任意多行内，例如较长语句

  ```c
  printf("Dimensional weight (pounds): %d\n",
        (volume + INCHES_PER_POUND - 1) / INCHES_PER_POUND);
  ```

- 记号间的空格更容易区分记号，通常在每个运算符的前后都放上一个空格；逗号后边放一个空格

  ```
  volume = height * length * width;
  ```

- 缩进有助于轻松识别程序嵌套（可以缩进3个或4个空格）

- 空行可以把程序划分成逻辑单元，从而使读者更容易辨别程序的结构

把换行符加进字符串中（换句话说，就是把字符串分成两行）是非法的：

```c
printf("To C, or not to C:
that is the question.\n");	/*** WRONG ***/
```

