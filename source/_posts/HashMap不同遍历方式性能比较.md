---
title: HashMap不同遍历方式性能比较
date: 2017-03-01 09:55:59
tags:
---
HashMap的不同遍历方式
<!--more-->
## HashMap的不同遍历方式
1、遍历keySet，再用get方法获得value。
（1）利用iterator遍历
HashMap<String,String> map = new HashMap<String,String>();
Iterator<String> iterator = map.keySet().iterator();
while (iterator.hasNext())
    map.get(iterator.next());
（2）利用foreach遍历
HashMap<String,String> map = new HashMap<String,String>();
Set<String> key = map.keySet();
for(String str: key)
    map.get(str);
2、遍历values，直接得到value。
（1）利用iterator遍历
HashMap<String,String> map = new HashMap<String,String>();
Iterator<String> iterator = map.values().iterator();
while (iterator.hasNext())
    iterator.next();
（2）利用foreach遍历
HashMap<String,String> map = new HashMap<String,String>();
Collection<String> value = map.values();
for(String str: value);
3、遍历entrySet ,再分别用getKey和getValue得到key、value。
（1）利用iterator遍历
HashMap<String,String> map = new HashMap<String,String>();
Iterator<Map.Entry<String,String>> iterator = map.entrySet().iterator();
while(iterator.hasNext()){
    iterator.next().getKey();
    iterator.next().getValue();
}
（2）利用foreach遍历
HashMap<String,String> map = new HashMap<String,String>();
Set<Map.Entry<String,String>> entry = map.entrySet();
for(Map.Entry<String,String> en: entry){
     en.getKey();
     en.getValue();
}
## 不同遍历方式下的时间性能比较（这里设定HashMap大小为1000000）
遍历方式
所需时间(ms)
iterator遍历keySet
59
iterator遍历values
28
iterator遍历entrySet
32
foreach遍历keySet
40
foreach遍历values
26
foreach遍历entrySet
29

## 总结
从结果可以看出：
（1）利用foreach语句遍历普遍比iterator所需的时间少。
（2）直接遍历values所需的时间最少。
（3）遍历keySet所需的时间最多。原因是除了遍历keySet，我们还需要用get方法得到每一个key的value。get方法通过计算key的hash值找到对应的value，增加了遍历的时间。
