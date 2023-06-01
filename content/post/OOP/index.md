---
slug: oop-java
title:  面向对象与Java
date: 2023-05-02 00:00:00+0000
categories:
    - Learn
---
## 变量类型
### Local Variables
方法体内
### Instance Variables
成员变量,类中方法体外
### Class Variables
类变量,静态成员变量,同一种类只有一份拷贝
### Parameters
传参
### 常量
final修饰,不能更改
## 修饰符[^1]
### 访问修饰符
- default(什么也不写): 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。      

- private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）       

- public : 对所有类可见。使用对象：类、接口、变量、方法       

- protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类） 
### 非访问修饰符
#### static 修饰符 
用来修饰类方法和类变量。       
##### 静态变量     

static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。         

##### 静态方法       

static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。      

#### final 修饰符
用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。
##### final变量
final 修饰符通常和 static 修饰符一起使用来创建类常量。
##### final方法
父类中的 final 方法可以被子类继承，但是不能被子类重写
abstract 修饰符，用来创建抽象类和抽象方法。
#### abstract修饰符
详见[抽象](#抽象)


## 继承
### 关键词 extends
### 调用父类方法 super 
我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类。

>在构造中子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 super 关键字调用父类的构造器并配以适当的参数列表。如果父类构造器没有参数，则在子类的构造器中不需要使用 super 关键字调用父类构造器，系统会自动调用父类的无参构造器。[^2]
>
记得super放在构造器的第一行

### 关键词this
this关键字：指向自己的引用。
另外参数变量名和成员变量名重复的时候常使用this关键词区分

### Override 与 Overload
#### 重写方法
1. 返回值和形参不能改
2. 抛出的异常不能变得比父类广泛
#### 重载方法
1. 访问权限不能更小
2. 入参不能改
3. 返回值可以不同(但是必须是父类返回值的派生类)
4. 抛出的异常可以改变

### upcase 和 downcase
- upcase:子类可以转为父类类型
- downcase: 只有由子类转成父类的父类才可以转为子类
### 关键词instanceof
`A istanseof Class`,其中 A 为一个对象，Class 表示一个类或者一个接口，当 obj 为 Class 的对象，或者是其直接或间接子类，或者是其接口的实现类，结果都返回 true，否则返回false。
### 注意
java中不能多继承

## 抽象
### 关键词abstract
### 特点
不能实例化对象  
### 抽象方法特点
1. 如果一个类包含抽象方法，那么该类必须是抽象类。
2. 任何子类必须重写父类的抽象方法，或者声明自身为抽象类
3. 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法
```java
public abstract class A{
    public abstract void ToDo();
}
```

## 接口
### 特点
- 都为抽象方法
- 不支持非final/static修饰的变量(不写默认为static final)
- 不需要写出abstract
### 继承
接口继承接口:extends[^3]
接口允许多继承
### 接口的实现
关键词:implements
类可以实现多个接口

## 异常处理
### 异常捕获
```java
try{
   // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}catch(异常类型3 异常的变量名3){
  // 程序代码
}finally{
    //to-do
}
```
finally无论是否try/catch都会触发   
try 代码后不能既没catch也没finally   
### throw
`throw new Exception("aaa");`
### throws
表明可能抛出异常
### 常用
`e.getMessage()` 获取e中的字符串
### 自定义异常
>这里只处理检测性异常
#### 模板
```java
public class A extends Exception{
    public A(String s){
        super(s);
    }
} 
```
## 泛型
### 泛型标记符
E - Element (在集合中使用，因为集合中存放的是元素)
T - Type（Java 类）
K - Key（键）
V - Value（值）
N - Number（数值类型）
？ - 表示不确定的 java 类型
### 泛型上限/下限
`<T extends/implements B>`  表示泛型应为B或B的子类   
`<T super B>` 表示泛型应为B或B的父类  
### 泛型类与泛型方法
```java
public class A<T>{
    //todo
}

public <T> void ff(T t1,T t2){
    //todo
}
```
## 字符串
### 字符串相等
equals()
```java
//源自菜鸟教程
String s1 = "Hello";              // String 直接创建
String s2 = "Hello";              // String 直接创建
String s3 = s1;                   // 相同引用
String s4 = new String("Hello");  // String 对象创建
String s5 = new String("Hello");  // String 对象创建
 
s1 == s1;         // true, 相同引用
s1 == s2;         // true, s1 和 s2 都在公共池中，引用相同
s1 == s3;         // true, s3 与 s1 引用相同
s1 == s4;         // false, 不同引用地址
s4 == s5;         // false, 堆中不同引用地址
 
s1.equals(s3);    // true, 相同内容
s1.equals(s4);    // true, 相同内容
s4.equals(s5);    // true, 相同内容
```

## 可变数组
```java
import java.util.ArrayList; 
```
`ArrayList<String> sites = new ArrayList<String>();`
get()访问元素
set(i,"xxx")修改元素
add()添加元素
remove(i)删除下标为i的元素
removeAll()删除所有元素
size()大小















[^1]:摘自菜鸟教程
[^2]:摘自菜鸟教程
[^3]:请与接口的实现区分