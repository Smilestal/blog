---
title: Kotlin基本语法
date: 2017-10-31 15:16:27
tags:
- Kotlin
categories: 
- Kotlin
- 基本语法
---
#### 包
```kotlin
package com.firstkotlin
```
    
#### 函数
返回值函数
```kotlin
fun add(a: Int, b: Int): Int {
    return a + b
}

//表达式作为函数体，返回值类型自动推断
fun add(a: Int, b: Int) = a + b
```

无返回值函数
```kotlin
fun addPrint(a: Int, b: Int): Unit {
    println("sum $a and $b is ${a + b}")
}

//Unit返回类型可省略
fun addPrint(a: Int, b: Int) {
    println("sum $a and $b is ${a + b}")
}
```

#### 变量
```kotlin
fun variable() {
    //一次性赋值的变量
    val a: Int = 1
    val b = 2
    val c: Int //没有赋值不能省略类型
    c = 3

    //可变变量
    var x = 3
    x += 1
}
```

#### 注释
除块注释可嵌套外，注释方式与Java相同
```java
//行注释
/* 块注释 */
```

#### 字符串模板
```kotlin
//变量模板 
var s1 = "a is $a"

//表达式模板  
var s2 = "a + b = ${a+b}"
```

#### 条件表达式
```kotlin
fun max(a: Int, b: Int): Int {
    if (a > b)
        return a
    else
        return b
}

fun max(a: Int, b: Int) = if (a > b) a else b
```

#### 使用可空值及null检测
当某个变量的值可以为null的时候，必须在声明出的类型后添加？来标识该引用可为空。
```kotlin
fun parseInt(str: String): Int? {
    // ……
}
```

使用返回可空值的函数需要做null检测：
```kotlin
fun printProduct(arg1: String, arg2: String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)

    // 直接使用 `x * y` 可能会报错，因为他们可能为 null
    if (x != null && y != null) {
        // 在空检测后，x 和 y 会自动转换为非空值 （ non-nullable）
        println(x * y)
    } else {
        println("either '$arg1' or '$arg2' is not a number")
    }
}
```

#### 使用类型检测及自动类型转换
`is`运算符检测表达式是否是某类型的实例。如果一个未知类型的局部变量或属性已经判断出为某类型，那么检测后的分支中可以直接当做该类型使用，无需显式转换：
```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // `obj` 在该条件分支内自动转换成 `String`
        return obj.length
    } 
    // 在离开类型检测分支后，`obj` 仍然是 `Any` 类型
    return null
}
```

或者
```kotlin
fun getStringLength(obj: Any): Int? {
    // `obj` 在 `&&` 右边自动转换成 `String` 类型
    if (obj is String && obj.length > 0) {
        return obj.length
    } 
    return null
}
```

#### 循环结构
##### for循环
```kotlin
fun forfunction(){
    val items = listOf("aaa", "bbb", "ccc")
    //遍历元素
    for(item in items){
        println(item)
    }

    //遍历索引
    for (index in items.indices){
        println("item at $index is ${items[index]}")
    }
}
```

##### while循环
```kotlin
val items = listOf("aaa", "bbb", "ccc")
var index = 0
while (index < items.size) {
    println("item at $index is ${items[index]}")
    index++
}
```

##### when表达式
when表达式的用法类似于switch
```kotlin
fun describe(obj: Any): String =
        when (obj) {
            1 -> "one"
            "hello" -> "greeting"
            is Long -> "Long"
            !is String -> "not is String"
            else -> "UnKown"
        }
```

#### range区间
区间表达式由具有操作符形式`..`的`rangeTo`函数辅以`in`和`!in`形成。
使用`in`运算符检测某个数字是否在指定区间内：
```kotlin
val x = 10
val y = 9
if (x in 1..y+1) {
    println("fits in range")
}
```

检测某个数字是否在指定区间外:
```kotlin
val list = listOf("a", "b", "c")
if (-1 !in 0..list.lastIndex) {
    println("-1 is out of range")
}
if (list.size !in list.indices) {
    println("list size is out of valid list indices range too")
}
```

区间迭代：
```kotlin
for (x in 1..5) {
    print(x)
}

for (x in 1..10 step 2) {
    print(x)
}

for (x in 9 downTo 0 step 3) {
    print(x)
}
```