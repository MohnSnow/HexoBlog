---
title: String-StringBuffer-StringBuilder性能对比
date: 2017-07-21 19:42:56
tags: Java
categories: "Java"
toc: true
---
String-StringBuffer-StringBuilder性能对比,以及常见的几道面试题。
<!--more-->
```
package com.meng.Jason.standard;

/**
 * Created by MengDexin.
 * Date : 17/7/21.
 * Time : 17:51.
 */
public class StringTest {
    private static int time = 50000;

    public static void main(String[] args) {
        testString();
        testStringBuffer();
        testStringBuilder();
        test1String();
        test2String();
    }

    public static void testString() {
        String s = "";
        long begin = System.currentTimeMillis();
        for (int i = 0; i < time; i++) {
            s += "java";
        }
        long over = System.currentTimeMillis();
        System.out.println("操作" + s.getClass().getName() + "类型使用的时间为：" + (over - begin) + "毫秒");
    }

    public static void testStringBuffer() {
        StringBuffer sb = new StringBuffer();
        long begin = System.currentTimeMillis();
        for (int i = 0; i < time; i++) {
            sb.append("java");
        }
        long over = System.currentTimeMillis();
        System.out.println("操作" + sb.getClass().getName() + "类型使用的时间为：" + (over - begin) + "毫秒");
    }

    public static void testStringBuilder() {
        StringBuilder sb = new StringBuilder();
        long begin = System.currentTimeMillis();
        for (int i = 0; i < time; i++) {
            sb.append("java");
        }
        long over = System.currentTimeMillis();
        System.out.println("操作" + sb.getClass().getName() + "类型使用的时间为：" + (over - begin) + "毫秒");
    }

    public static void test1String() {
        long begin = System.currentTimeMillis();
        for (int i = 0; i < time; i++) {
            String s = "I" + "love" + "java";
        }
        long over = System.currentTimeMillis();
        System.out.println("字符串直接相加操作：" + (over - begin) + "毫秒");
    }

    public static void test2String() {
        String s1 = "I";
        String s2 = "love";
        String s3 = "java";
        long begin = System.currentTimeMillis();
        for (int i = 0; i < time; i++) {
            String s = s1 + s2 + s3;
        }
        long over = System.currentTimeMillis();
        System.out.println("字符串间接相加操作：" + (over - begin) + "毫秒");
    }
}
```
结果
```
操作java.lang.String类型使用的时间为：2457毫秒
操作java.lang.StringBuffer类型使用的时间为：6毫秒
操作java.lang.StringBuilder类型使用的时间为：2毫秒
字符串直接相加操作：1毫秒
字符串间接相加操作：7毫秒
```
分析:
1. 对于直接相加字符串，效率很高，因为在编译器便确定了它的值，也就是说形如"I"+"love"+"java"; 的字符串相加，在编译期间便被优化成了"Ilovejava"。这个可以用javap -c命令反编译生成的class文件进行验证。
2. String、StringBuilder、StringBuffer三者的执行效率：
　　StringBuilder(线程不安全的) > StringBuffer(线程安全的) > String
　　当然这个是相对的，不一定在所有情况下都是这样。
　　比如String str = "hello"+ "world"的效率就比 StringBuilder st  = new StringBuilder().append("hello").append("world")要高。
　　因此，这三个类是各有利弊，应当根据不同的情况来进行选择使用：
　　当字符串相加操作或者改动较少的情况下，建议使用 String str="hello"这种形式；
　　当字符串相加操作较多的情况下，建议使用StringBuilder，如果采用了多线程，则使用StringBuffer。
1. 下面这段代码的输出结果是什么？
　　String a = "hello2"; 　　String b = "hello" + 2; 　　System.out.println((a == b));
　　输出结果为：true。原因很简单，"hello"+2在编译期间就已经被优化成"hello2"，因此在运行期间，变量a和变量b指向的是同一个对象。
2. 下面这段代码的输出结果是什么？
　　String a = "hello2"; 　  String b = "hello";       String c = b + 2;       System.out.println((a == c));
　　输出结果为:false。由于有符号引用的存在，所以  String c = b + 2;不会在编译期间被优化，不会把b+2当做字面常量来处理的，因此这种方式生成的对象事实上是保存在堆上的。因此a和c指向的并不是同一个对象。
3. 下面这段代码的输出结果是什么？
　　String a = "hello2";   　 final String b = "hello";       String c = b + 2;       System.out.println((a == c));
　　输出结果为：true。对于被final修饰的变量，会在class文件常量池中保存一个副本，也就是说不会通过连接而进行访问，对final变量的访问在编译期间都会直接被替代为真实的值。那么String c = b + 2;在编译期间就会被优化成：String c = "hello" + 2;
4. 请别再拿“String s = new String("xyz");创建了多少个String实例”来面试了吧 http://rednaxelafx.iteye.com/blog/774673/





