---
title: IntegerCache ByteCache CharacterCache LongCache ShortCache
date: 2018-08-30 11:25:56
tags:
---
new Integer(1) 与 Integer.valueOf(1) 的区别

使用 Integer.valueOf(1) 可以使用系统缓存，既减少可能的内存占用，也省去了频繁创建对象的开销。

public static Integer valueOf(int i) {
assert IntegerCache.high >= 127;
 if (i >= IntegerCache.low && i <= IntegerCache.high)
return IntegerCache.cache[i + (-IntegerCache.low)];
 return new Integer(i);
}
在[IntegerCache.low, IntegerCache.high] 之前的数字都已被缓存。

```
private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static final Integer cache[];
​
    static {
        // high value may be configured by property
        int h = 127;
        String integerCacheHighPropValue =
            sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
        if (integerCacheHighPropValue != null) {
            int i = parseInt(integerCacheHighPropValue);
            i = Math.max(i, 127);
            // Maximum array size is Integer.MAX_VALUE
            h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
        }
        high = h;
​
        cache = new Integer[(high - low) + 1];
        int j = low;
        for(int k = 0; k < cache.length; k++)
            cache[k] = new Integer(j++);
    }
​
    private IntegerCache() {}
}
```
默认区间是[-128, 127], 通过 VM 参数-XX:AutoBoxCacheMax=<size> 可以配置缓存的最大值.
Short Long Byte Characte也都类似，范围有所不同
类
区间
设置上限
Integer
[-128,127]
-XX:AutoBoxCacheMax=<size>
Short
[-128,127]
不可设置
Long
[-128,127]
不可设置
Byte
[-128,127]
不可设置
Character
[0,127]
不可设置