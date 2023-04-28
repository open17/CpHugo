---
title:  C语言快速入门
description: 作者：open17
slug: cstart
date: 2023-04-26 00:00:00+0000
image: cover.jpg
categories:
    - Alg
tags:
    - summary
    - c
---
```C
#include <stdio.h>
int main(){
    printf("Hello World!");
    return 0;
}
```
## 基础知识
### 分号 
每个语句**必须**以分号结束
### 符号类型  
一定要是**英文**符号
### 注释
- 单行注释
- 多行注释(也可单行)
```c
//单行注释

/*多行注释*/
```
### 数据类型
|TYPE|BYTE|MORE|
|----|----|:----:|
|**char**|	1 字节|	-128 到 127 | 
|**unsigned char**|	1 字节	|0 到 255|
|**signed char**|	1 字节|	-128 到 127  |
|**int**	|2 或 4 字节|———|	  
|**unsigned int**|	2 或 4 字节	 |———| 
|**short**|	2 字节	|———|  
|**unsigned short**|	2 字节|	———|  
|**long**|	4 字节  |———|
|**unsigned long**|	4 字节  |———|
|**float**	|4 字节|6 位有效位  |
|**double**	|8 字节|15 位有效位 | 
|**long double**| 16 字节|19 位有效位|

```c
//sizeof可以获取储存字节大小
#include <stdio.h>
int main()
{
   printf("int 存储大小 : %lu \n",sizeof(int));
   return 0;
}
```

### 常量
+ 整数常量
    > 整数常量可以是十进制、八进制或十六进制的常量。前缀指定基数：0x 或 0X 表示十六进制，0 表示八进制，不带前缀则默认表示十进制。  
    整数常量也可以带一个后缀，后缀是 U 和 L 的组合，U 表示无符号整数（unsigned），L 表示长整数（long）。后缀可以是大写，也可以是小写，U 和 L 的顺序任意。
+ 浮点常量
  > 浮点常量由整数部分、小数点、小数部分和指数部分组成。您可以使用小数形式或者指数形式来表示浮点常量。  
  当使用小数形式表示时，必须包含整数部分、小数部分，或同时包含两者。当使用指数形式表示时， 必须包含小数点、指数，或同时包含两者。带符号的指数是用 e 或 E 引入的。
+ **字符常量**
  - 单引号内
  - char -> 1字节
  - **转义字符**
    + \n  *换行符号*  
    + \b  *退格*   
    + \ (特殊符号) *本身*
+ 字符串常量
    >双引号中  
    多行时
+ **定义常量**
  ```c
  //name=value
  #define name value
  ```
### 变量  
*变量名可以是字母、数字和下划线的组合*  
规则  
1. 开头必须是字母或 ***下划线***（可以下划线）
2. 不可以是C语言关键字
3. 不能有空格
### **类型转换**  
- 显示转换
  ```c
  c=1.2F
  b=(int)c
  //要注意在c中强制转换不是一个函数式转换
  ```
- 隐式转换  
  - 方向： 精度上升
  - 特殊： scanf/printf 只能int-chr转换(精度上升的转换都不行？)
- char - int 转换(显/隐)
  *详见*[字符ascii](#字符ascii)
### 储存类（不考）
### 运算符
- 算数运算符
  - \+ \- \* \/
  - 小心[隐式转换](#类型转换)（加减也会）
  - 除法取全舍去（负时偏向绝对值）
    ```c
    //例如
    10/3==-3; 
    10/(-3)==-3
    ```
  - 取模 % 
    >在算法中常/与%使用依次去位数  
    (高精度模板题)
  - ++-- 自增自减
    >***注意Attention！***  
    a++ 先赋值后运算  
    ++a 先运算后赋值
- 赋值运算符
  > 形式： *(算数运算符)$=$*  
  如 a **+=** 1 
- 关系运算符  
    \== != > < <= >=
    >***注意Attention！***  
    在c中不能1<a<b这样判断
- 逻辑运算符  
  - 与 &&
  - 或 || 
  - 非 !
- **位运算符号**   
  详见 [位运算](#位运算)
***
## 输入输出
### 输入流 stdin
未读取的不会清空，**共享**
```c
//手动清空输入流
//通过连续读取来清空输入流
int r=getchar();
while (r!=EOF){
  r=getchar()
}
```
### 输出流 stdout  
连续，不会自动换行 -> \n的重要性
```c
#include <stdio.h>
int main(){
    char a;
    //其实getchar()返回的是int，不过由于char-int的隐式转换，也无所谓
    //每当按下回车时getchar会读取stdin中第一个，并将其从stdin中弹出
    a=getchar();
    //putchar 接收的也是int
    putchar(a);
    //scanf 记得占位符正确和写寻地址符
    //当然数组名本身即使地址，不要寻地址符
    //每当按下回车时getchar会读取stdin中前n个（取决于占位符），并将其从stdin中弹出
    scanf("%c",&a);
    //一般函数最后输出结尾都会加上\n
    printf("%c\n",a);
    return 0;
}
```
### 占位符
|   占位符   | 类型  |
|  ----  | ----  |
| %d  | int |
| %c | char |
| %s | str(char[]) |
| %f | float |
| %.3f| 3位|
|%lf |double|
|%p|pointer|
### 字符ascii  
- 32 空格
- 48-57 数字0-9
- 65-90 大写字母
- 97-122 小写字母
```c
// 标准输入输出库
#include <stdio.h>
int main(){
    //隐式转换 97 a
    int c = 'a';
    printf("%c %d",c,c);
    //在c中取ascii码值可直接类型转换得出
    //而由“11”(str)取得11(int)可调库，或者哈希映射（自建数组下表映射或者ascii映射(+48))
    return 0;
}
```
### 更多输入输出
[详见字符串](#字符串)
***
## 文件读写
### 文件打开和关闭
**不要忘记关闭文件**
```c
// open
FILE *fopen( const char *filename, const char *mode );
// close
fclose( FILE *fp );
```
### filename 文件路径
### mode 访问模式
|mode|description|
|----|----|
|r|read 只读|
|w|write 只写，重写/新建(会覆盖)|
|a|add 只写，追加/新建(不会覆盖)|
|r+|读写|
|w+|读写，重写/新建(会覆盖)|
|a+|读写，追加/新建(不会覆盖)|  
> 二进制模式 "rb", "wb", "ab", "rb+", "r+b", "wb+", "w+b", "ab+", "a+b"
### EOF
```c
//在c中EOF标识符实际为-1
#define EOF -1
```
### 读取文件
**注意**fscanf()先要传入fp，和其它相反
```c
//char *buf 为缓冲区（自己开一个数组）
int fgetc( FILE * fp );
char *fgets( char *buf, int n, FILE *fp );
int fscanf(FILE *fp ,const char *s, char *buf);
```
> 函数 fgets() 从 fp 所指向的输入流中读取 n - 1 个字符。它会把读取的字符串复制到缓冲区 buf，并在最后追加一个 null 字符来终止字符串。如果这个函数在读取最后一个字符之前就遇到一个换行符 '\n' 或文件的末尾 EOF，则只会返回读取到的字符，包括换行符
>int fscanf(FILE *fp, const char *format, ...) 函数文件中读取字符串在遇到第一个空格和换行符时，会停止读取
### 写入文件  
**注意**fprintf()先要传入fp，和其它相反
```c
// 失败时返回EOF
int fputc( int c, FILE *fp );
int fputs( const char *s, FILE *fp );
int fprintf(FILE * fp,const char*s);
```
### 二进制读写
```c
fread();
fwrite();
```
***
## 二进制
### 比特与字节
- bit 二进制一个数位
- 1 byte = 8 bit
### 进制转换
10进制->2进制： 除2法取余数
2进制->10进制： 从右到左依次乘从$2^0$开始到$2^n$的和
### 位运算
1. 与 &
2. 或 |
3. 取反 ~
4. 异或 ^
5. 左右移 <<< >>>
```c
int a=4;
//二进制右移1位即除以2，左一乘以2
//同理，十进制则1位乘除10，注意c中左右移符号是二进制的移动
if (a>>1==a/2){
    printf("True");
}
```
1. 常见性质(略)
### 二进制算法
1. 二进制枚举
2. 快速幂
***
## 基础结构
### 分支结构
 ```c
 //分支
 if (){

 }
 else if (){

 }
 else{

 }
 
 //三元
 a==0?printf("a=0"):printf("a!=0");
 ```
 > **!!!注意**   
 > 如果switch没有break则会继续执行（会触发default或者其它case）   
 expression必须是常量表达式，必须是一个整型或枚举类型
 ```c
switch(expression){
    case constant-expression  :
       statement(s);
       break; /* 可选的 */
    case constant-expression  :
       statement(s);
       break; /* 可选的 */
  
    /* 您可以有任意数量的 case 语句 */
    default : /* 可选的 */
       statement(s);
}

 ```
### 循环结构
```c
int a=10;
while(1){
  a--;
  if (a>5){
    continue;
  }
  printf("NO")
  if (a<4) break;
}
for(a=10;a<3;a--){
  printf("%d,a");
}
do{
  printf("%d",a);
  a-=1
}while(a);
```
### 省略
如果只跟一个句子，可以省略大括号
单数字作为条件时0假其它真
如下面的句子是合法的
```c
for(int i=0;i<10;i++)
  for(int j=i;j<10;j++)
    printf("%d",j);

if(a==0) printf("YES!!!");

int a=0;
if(!a){
  printf("a is zero");
}
```
***
## 数组与字符串
### 一维数组
- 声明格式 type arrayName [ arraySize ];
  ```c
  int a[50];
  ```
- 初始化(**大括号**)
  ```c
  //标准初始化
  int a[2]={1,2};

  //可以只初始化少初始化，但不能多初始化
  //即大括号 { } 之间的值的数目不能大于我们在数组声明时在方括号 [ ] 中指定的元素数目
  int a[10]={1,4,3,5};

  //如果没有指定数组大小，则其等于初始化个数
  int a[]={1,2,4};
  ```
- 两种访问
  - 下标（索引）从0开始
  - 指针访问（数组名指向数组第一个元素的地址，数组储存连续）
    [详见指针](#指针)
### 高维数组
- 声明与初始化  
  ***(要记得大小从1开始，但索引从0开始)***
```c
  //
  int a[2][2][2];
  //
  int a[2][3]={{1,2,3},{2,4,6}};
  //
  int a[2][3]={1,2,3,2,4,6}
<<<<<<< HEAD
```
=======

```

>>>>>>> 08247bfa3aa6eb6eaa3d0a7568088d5cdb5f4654
- 两种访问
  - 下标（索引）从0开始
  - 指针访问
    - 列指针与行指针
    - 单指针（利用连续性）
    [详见指针](#指针)
### 字符串
>everal ways to initialize a string

**一定**以 ***'\0'*** 结尾
+ char str[20] = {'H', 'e', 'l', 'l', 'o', '\0'};  
+ char str[20] = "Hello"; // '\0' is automatically set to str[5]   
+ char str[] = "Hello"; //str's size is 6 

如果已经声明，就不能进行**初始化** 

#### 易错练习 
是否正确？
```c
//注意字符和字符串的引号
//注意隐式转换
char a[]={'a','c',0}
```
### 字符串相关  <stdio.h>
#### printf()
> %s
#### sprintf()
```c
int sprintf( char *str, const char *format, ... );


char buffer[50];
int n, a = 5, b = 3;
n = sprintf(buffer, "%d plus %d is %d", a, b, a+b);
// n 实际长度13
//buffer="5 plus 3 is 8"
```
#### puts()
> puts stops printing when it meets '\0'.

#### scanf()
- %s 读到空格停止
- %ns 读到空格/读n个字符停止
  
#### gets()
读一整行，字符数组开小了可能越界

#### fgets()
> fgets(your_line, sizeof(your_line), stdin)  
> 利用sizeof ，防止越界


### 字符串相关 <string.h>

#### strlen()
> length of str, not including '\0';

#### strcpy(destination,source)
**字符串赋值**要strcpy，别直接等于号赋值
> copy string from source to destination(包括'\0')  
> 小心越界

#### strncpy(destination, source, n)
> 复制前n个字符，最后自动加上'\0'

#### strcmp(str1, str2)
> 逐位比较ascii，直到某一位ascii不一样，str1>str2 返回 1，相等返回0，其余-1

#### strncmp(str1, str2, n)
> 前n个

#### strcat(destination, source); 
> 连接，加在dest上，小心越界

### 字符串相关 <stdlib.h>
#### atoi(str)
> str->int  
> 支持正负号  
> 取前面可以转换的，到非数字字符停止(无视空格) 
> ex. atoi("-10aaa")=-10

#### atof(str)
• Same as atoi  
• Space, +, - are acceptable  
• An E or e (exponent) is acceptable  
• A decimal point is acceptable  


### 相关算法（仅作了解）
- BF，BK，KMP，BM
- 前缀树
- 后缀树
- AC自动机
- 其它
***
## 基础语法
### 函数
- #### 函数的声明  
  如果函数放于main函数后面/多文件，需要提前声明
  声明时参数的名称并不重要，只有参数的类型是必需的，因此以下都是都是有效声明
  ```c
  int max(int, int);
  int max(int a, int b);
  ```
- #### void
  无返回值
- #### 返回多个值
  利用指针
- #### 形式参数
  详见作用域
- #### 传递数组
  1. 传一个指针
  2. 传不定长数组(ex. int a[],如果二维需要指定第二维度，int a[][3])
  3. 传定长数组(int a[20])
- ####  #define函数
  ```c
  #define MAX(a,b) a>b?a:b
  #define  SQ(x) x*x 
  ```
### 作用域
  - 3 types
    > 在函数或块内部的局部变量,在所有函数外部的全局变量,在形式参数的函数参数定义中
  - small has big
    > 小可以改大的，大不能改小的
  - 形参同名替代（小带大）
    > 但是在函数内，如果两个名字相同，会使用局部变量值，全局变量不会被使用

### 递归
  > 懂得都懂  ——佚名    
  > 自顶向下,利用系统栈
  ####  经典题 斐波那契
  ```c
  #include<stdio.h>
  int Fibonacci(int n){
    if (n<=2){
      return 1;
    }
    return Fibonacci(n-1)+Fibonacci(n-2);
  }
  int main(){
    int n;
    scanf("%d",&n);
    printf("%d",Fibonacci(n));
    return 0;
  }
  ```
### 命令行参数
```c
int main(int argc, char *argv[] ){
  return 0;
}
```
+ argc 存放命令行参数的个数
+ *argv[] 从argv[1]开始存放每一个参数的指针，第一个即argv[0]存放程序名
***
## 多文件
### 构成
> 宏文件（xxx.h） 文件存放声明  

> xxx.c 文件存放函数   
 
> 主函数里 #include"xxx.h"  
***
## 进阶语法
### **指针**
### 结构体
#### **结构体定义与初始化**
```c
//一个完整结构体的example
struct tag1{
  int a;
  char b[30];
}variable1={1,"ssss"};

struct tag1 variable2;

typedef struct{
  float f;
}tag2;

tag2 variable3;
```
***！！！注意！！！***  
1. 无论如何struct结尾必须有**分号**
2. typedef格式固定，下面不是变量而是标签
3. 如果变量已经声明，就不能进行初始化
   ```c
   //无typedef时下面一定是变量（无标签）
   struct {
    int a;
   }VARIABLE;
    //下面一定是tag
    //tag 不能放上面
    //实质 typedef struct{int a;} TAG;
    //类同 typedef unsigned char UC;
   typedef struct{
    int a;
   }TAG;
   ```
#### **结构体内部元素赋值**
  ```c
   struct day{
    char feeling[100];
    int time;
   }today;

   today.time=222;
   strcpy(today.feeling,"dddd");

   struct day yesterday={"good",221};
   ```
#### **结构体指针**
接着上文定义的结构体
```c
struct day *check;
check=&today
printf("%s",check->feeling);
```
#### 结构体数组
接着上文定义的结构体
```c
struct day holiday[60];
int i;
for(i=0;i<60;i++){
  strcpy(holiday[i].feeling,happy);
  holiday[i].time=i;
}
```
### 枚举类型
```c
enum week
{
  MON=1, TUE, WED, THU, FRI, SAT, SUN
}day;

day=MON;
printf("%d",day);
//若不初始化MON，默认第一个是 0
//注意：第一个枚举成员的默认值为整型的 0，后续枚举成员的值在前一个成员上加 1。
//如果我们把第3个枚举成员的值定义为 9，第4个就为 10，以此类推，第2个依然为1。

//可以和整形强制转化
int a=1;
days=(enum week)a;
//days=MON
```

### 动态内存
***
## 入门级基础算法
### 数学
- 求质数
  了解朴素质数判定即可
  ```c
  // 朴素质数判定
  /*
  已经声明过
  #define true 1
  #define false 0
  */
  int check(int a){
    if (a<2){
        return false;
    }
    int i;
    for(i=2;i*i<a;i++){
        if (a%i==0){
            return false;
        }
    }
    return true;
  }

  ```
- 最大公约数  
  了解欧几里得算法即可
  ```c
  int gcd(int a,int b){
    if (b==0) return a;
    return gcd(b, a % b);
  }
  ```
- 最小公倍数  
  $lcm(a,b)*gcd(a,b)=a*b$  
  先求出gcd即可

- 高精度（了解加法减法即可）
### 排序
- 稳定排序
- 不稳定排序
- 计数排序
- 桶排序
- qsort()
### 双指针
- 同向
- 逆向
- 滑窗