---
title: HashMap的循环方式性能对比
date: 2017-02-10 11:11:11
tags: Java 对比
categories: "Java"
toc: true
---
### 一、缘由
代码重构过程中发现许多这样的代码:
```
for (Movie movie : showMap.keySet()) {
    List<ShowModel> models = showMap.get(movie);
    if (CollectionUtils.isEmpty(models)) {
    .............
}
```
<!--more-->
### 二、两种循环方式的实测数据
```
package com.meng.Jason.collections;

import java.util.HashMap;
import java.util.Map;

/**
 * Created by MengDexin.
 * Date : 17/7/19.
 * Time : 17:53.
 */
public class MapTest {

    public static void main(String[] args) {
        test();
    }

    public static void test() {
        //准备数据
        Map<String, String> map = new HashMap<String, String>();
        for (int i = 0; i < 10000; i++) {
            map.put("a" + i, "a" + i);
        }

        for (int c = 0; c < 10; c++) {
            //循环方式
            long start = System.currentTimeMillis();
            int count = 100, n = 0;
            while (n < count) {
                for (Map.Entry<String, String> entry : map.entrySet()) {
                    String value = entry.getValue();
                }
                ++n;
            }
            System.out.print("方式一：" + (System.currentTimeMillis() - start) + "  ms, ");

            start = System.currentTimeMillis();
            n = 0;
            while (n < count) {
                for (String key : map.keySet()) {
                    String value = map.get(key);
                }
                ++n;
            }

            System.out.println("方式二：" + (System.currentTimeMillis() - start) + " ms");
        }
    }
}
```
结果:
```
方式一：24  ms, 方式二：42 ms
方式一：11  ms, 方式二：18 ms
方式一：14  ms, 方式二：17 ms
方式一：12  ms, 方式二：18 ms
方式一：10  ms, 方式二：19 ms
方式一：12  ms, 方式二：18 ms
方式一：11  ms, 方式二：24 ms
方式一：10  ms, 方式二：18 ms
方式一：11  ms, 方式二：19 ms
方式一：10  ms, 方式二：18 ms
```
### 三、原理分析
基于以上的测试，可以得出结论:
* 第一种循环Map的方式效率要比第二种高不少。

下面分析一下这两种循环方式的源码得出性能差异的原因:
原因一： 方式一 map.entrySet() 的效率比方式二 map.keySet() 高，map.keySet() 比map.entrySet() 多了一次请求
```
private final class KeyIterator extends HashIterator<K> {
     public K next() {
         return nextEntry().getKey();
     }
 }
```
而  方法nextEntry() 里面有如下while循环：
```
final Entry<K,V> nextEntry() {
    if (modCount != expectedModCount)
        throw new ConcurrentModificationException();
    Entry<K,V> e = next;
    if (e == null)
        throw new NoSuchElementException();
    if ((next = e.next) == null) {
        Entry[] t = table;
        while (index < t.length && (next = t[index++]) == null)
            ;
    }
    current = e;
    return e;
}
```
原因二：方式一 中Map.Entry 中已经有了key以及value，但是方式二中还需要根据key调用map.getKey() 去获取对应的value，map.getKey()里面存在这样一段代码：
```
/**
  * Returns the entry associated with the specified key in the
  * HashMap.  Returns null if the HashMap contains no mapping
  * for the key.
  */
 final Entry<K,V> getEntry(Object key) {
     if (size == 0) {
         return null;
     }
     int hash = (key == null) ? 0 : hash(key);
     for (Entry<K,V> e = table[indexFor(hash, table.length)];
          e != null;
          e = e.next) {
         Object k;
         if (e.hash == hash &&
             ((k = e.key) == key || (key != null && key.equals(k))))
             return e;
     }
     return null;
 }
```
此处存在一个for循环，当hashCode值分布较好无冲突的时候，这个for循环只需要循环一次，但是当map中的hashCode冲突较大的时候，这个for循环会运行多次，造成性能损耗,所以，结论是第一种循环取值操作效率要高，在应用中，推荐尽量使用第一种方式进行HashMap的循环取值操作