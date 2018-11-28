---
title: Java集合[Array、Collection、Set、List、Map]
date: 2017-07-18 10:38:21
tags: Java
categories: "Java"
toc: true
---
大多数真实应用程序都会处理像文件、变量、来自文件的记录或数据库结果集这样的集合。Java 语言有一个复杂的集合框架，您可以使用它创建和管理各种类型的对象集合。本单元将介绍最常用的集合类并帮助您开始使用它们。
<!--more-->
### 1.入门

![Java集合类](http://ol5edn32j.bkt.clouddn.com/262238192165666.jpg)

-------------------
### 2.数组
下面介绍stackoverflow中12个关于数组操作得票数最多的问题
#### 2.1 声明数组
```
String[] aArray = new String[5];
String[] bArray = {"a","b","c", "d", "e"};
String[] cArray = new String[]{"a","b","c","d","e"};
```
#### 2.2 输出一个数组
```
int[] intArray = { 1, 2, 3, 4, 5 };
String intArrayString = Arrays.toString(intArray);
// print directly will print reference value
System.out.println(intArray);
// [I@7150bd4d
System.out.println(intArrayString);
// [1, 2, 3, 4, 5]
```
#### 2.3 从一个数组创建数组列表
```
String[] stringArray = { "a", "b", "c", "d", "e" };
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(stringArray));
System.out.println(arrayList);
// [a, b, c, d, e]
```
#### 2.4 检查一个数组是否包含某个值
```
String[] stringArray = { "a", "b", "c", "d", "e" };
boolean b = Arrays.asList(stringArray).contains("a");
System.out.println(b);
// true
```
#### 2.5 连接连个数组
```
int[] intArray = { 1, 2, 3, 4, 5 };
int[] intArray2 = { 6, 7, 8, 9, 10 };
// Apache Commons Lang library
int[] combinedIntArray = ArrayUtils.addAll(intArray, intArray2);
```
#### 2.6 声明一个内联数组（Array inline）
```
method(new String[]{"a", "b", "c", "d", "e"});
```
#### 2.7 把提供的数组元素放入一个字符串
```
// containing the provided list of elements
// Apache common lang
String j = StringUtils.join(new String[] { "a", "b", "c" }, "-");
System.out.println(j);
// a-b-c
```
#### 2.8 将一个数组列表转换为数组
```
String[] stringArray = { "a", "b", "c", "d", "e" };
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(stringArray));
String[] stringArr = new String[arrayList.size()];
arrayList.toArray(stringArr);
for (String s : stringArr)
    System.out.println(s);
```
#### 2.9 将一个数组列表转换集(Set)
```
String[] stringArray = { "a", "b", "c", "d", "e" };
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(stringArray));
String[] stringArr = new String[arrayList.size()];
arrayList.toArray(stringArr);
for (String s : stringArr)
    System.out.println(s);
```
#### 2.10 逆向一个数组
```
int[] intArray = { 1, 2, 3, 4, 5 };
ArrayUtils.reverse(intArray);
System.out.println(Arrays.toString(intArray));
//[5, 4, 3, 2, 1]
```
#### 2.11 移除数组中的元素
```
int[] intArray = { 1, 2, 3, 4, 5 };
int[] removed = ArrayUtils.removeElement(intArray, 3);//create a new array
System.out.println(Arrays.toString(removed));
```
#### 2.12 移除数组中的元素
```
byte[] bytes = ByteBuffer.allocate(4).putInt(8).array();
for (byte t : bytes) {
   System.out.format("0x%x ", t);
}
```
#### 2.12 数组其他知识
1. [for和foreach的性能对比](http://www.cnblogs.com/suneryong/p/6520442.html)

### 3.Collection


### 4.Map


### 5.List


#### 6.Set

