---
title: HashMap不同遍历方式性能比较
date: 2017-02-11 09:55:59
tags: Java 对比
categories: "Java"
toc: true
---
#### 一、遍历keySet，再用get方法获得value。
（1）利用iterator遍历
```
HashMap<String,String> map = new HashMap<String,String>();
Iterator<String> iterator = map.keySet().iterator();
while (iterator.hasNext())
    map.get(iterator.next());
```
<!--more-->
（2）利用foreach遍历
```
HashMap<String,String> map = new HashMap<String,String>();
Set<String> key = map.keySet();
for(String str: key)
    map.get(str);
```
#### 二、遍历values，直接得到value。
（1）利用iterator遍历
```
HashMap<String,String> map = new HashMap<String,String>();
Iterator<String> iterator = map.values().iterator();
while (iterator.hasNext())
    iterator.next();
```
（2）利用foreach遍历
```
HashMap<String,String> map = new HashMap<String,String>();
Collection<String> value = map.values();
for(String str: value);
```
#### 三、遍历entrySet ,再分别用getKey和getValue得到key、value。
（1）利用iterator遍历
```
HashMap<String,String> map = new HashMap<String,String>();
Iterator<Map.Entry<String,String>> iterator = map.entrySet().iterator();
while(iterator.hasNext()){
    iterator.next().getKey();
    iterator.next().getValue();
}
```
（2）利用foreach遍历
```
HashMap<String,String> map = new HashMap<String,String>();
Set<Map.Entry<String,String>> entry = map.entrySet();
for(Map.Entry<String,String> en: entry){
     en.getKey();
     en.getValue();
}
```
#### 四、不同遍历方式下的时间性能比较（这里设定HashMap大小为1000000）
遍历方式|所需时间(ms)
-|-
iterator遍历keySet|59
iterator遍历values|28
iterator遍历entrySet|32
foreach遍历keySet|40
foreach遍历values|26
foreach遍历entrySet|29

#### 五、 总结
从结果可以看出：
1. 利用foreach语句遍历普遍比iterator所需的时间少。
2. 直接遍历values所需的时间最少。
3. 遍历keySet所需的时间最多。原因是除了遍历keySet，我们还需要用get方法得到每一个key的value。get方法通过计算key的hash值找到对应的value，增加了遍历的时间。

#### 六、 代码

```
private static void test1() {
    //准备数据
    Map<String, String> map = new HashMap<String, String>();
    for (int i = 0; i < 1000000; i++) {
        map.put("a" + i, "a" + i);
    }
    String temp;
    // 分别计算10次
    for (int c = 0; c < 10; c++) {
        long start = System.currentTimeMillis();
        Iterator<String> iterator1 = map.keySet().iterator();
        while (iterator1.hasNext()){
            temp = map.get(iterator1.next());
        }
        System.out.print("KeySet->iterator->getKey：" + (System.currentTimeMillis() - start) + "  ms, ");

        start = System.currentTimeMillis();
        Set<String> key = map.keySet();
        for(String str: key)
            temp =  map.get(str);
        System.out.print("KeySet->for->getKey：" + (System.currentTimeMillis() - start) + "  ms, ");

        start = System.currentTimeMillis();
        Iterator<String> iterator2 = map.values().iterator();
        while (iterator2.hasNext())
            temp = iterator2.next();
        System.out.print("values->iterator：" + (System.currentTimeMillis() - start) + "  ms, ");

        start = System.currentTimeMillis();
        Collection<String> value = map.values();
        for(String str: value)
            temp = str;
        System.out.print("values->for：" + (System.currentTimeMillis() - start) + "  ms, ");

        start = System.currentTimeMillis();
        Iterator<Map.Entry<String,String>> iterator3 = map.entrySet().iterator();
        while(iterator3.hasNext()){
            temp = iterator3.next().getValue();
        }
        System.out.print("entrySet->iterator->getKey：" + (System.currentTimeMillis() - start) + "  ms, ");

        start = System.currentTimeMillis();
        Set<Map.Entry<String,String>> entry = map.entrySet();
        for(Map.Entry<String,String> en: entry){
            temp = en.getValue();
        }
        System.out.println("entrySet->for->getKey：" + (System.currentTimeMillis() - start) + "  ms");
    }
}
```
结果:
```
KeySet->iterator->getKey：55  ms, KeySet->for->getKey：58  ms, values->iterator：29  ms, values->for：25  ms, entrySet->iterator->getKey：26  ms, entrySet->for->getKey：26  ms
KeySet->iterator->getKey：39  ms, KeySet->for->getKey：52  ms, values->iterator：63  ms, values->for：29  ms, entrySet->iterator->getKey：19  ms, entrySet->for->getKey：19  ms
KeySet->iterator->getKey：42  ms, KeySet->for->getKey：34  ms, values->iterator：22  ms, values->for：20  ms, entrySet->iterator->getKey：20  ms, entrySet->for->getKey：21  ms
KeySet->iterator->getKey：33  ms, KeySet->for->getKey：29  ms, values->iterator：23  ms, values->for：32  ms, entrySet->iterator->getKey：24  ms, entrySet->for->getKey：20  ms
KeySet->iterator->getKey：35  ms, KeySet->for->getKey：30  ms, values->iterator：22  ms, values->for：20  ms, entrySet->iterator->getKey：34  ms, entrySet->for->getKey：22  ms
KeySet->iterator->getKey：51  ms, KeySet->for->getKey：28  ms, values->iterator：21  ms, values->for：20  ms, entrySet->iterator->getKey：22  ms, entrySet->for->getKey：21  ms
KeySet->iterator->getKey：37  ms, KeySet->for->getKey：45  ms, values->iterator：24  ms, values->for：21  ms, entrySet->iterator->getKey：22  ms, entrySet->for->getKey：21  ms
KeySet->iterator->getKey：40  ms, KeySet->for->getKey：33  ms, values->iterator：21  ms, values->for：22  ms, entrySet->iterator->getKey：45  ms, entrySet->for->getKey：24  ms
KeySet->iterator->getKey：40  ms, KeySet->for->getKey：33  ms, values->iterator：21  ms, values->for：21  ms, entrySet->iterator->getKey：20  ms, entrySet->for->getKey：34  ms
KeySet->iterator->getKey：39  ms, KeySet->for->getKey：33  ms, values->iterator：22  ms, values->for：19  ms, entrySet->iterator->getKey：19  ms, entrySet->for->getKey：22  ms

```