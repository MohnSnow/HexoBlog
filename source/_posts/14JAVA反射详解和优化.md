---
title: JAVA反射详解和优化
date: 2017-07-19 19:32:28
tags: Java
categories: "Java"
toc: true
---
### 1.何为反射机制
反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。
<!--more-->

### 2.反射的应用场景
1. 在运行时判断任意一个对象所属的类；
2. 在运行时构造任意一个类的对象；
3. 在运行时判断任意一个类所具有的成员变量和方法；
4. 在运行时调用任意一个对象的方法；
5. 生成动态代理；

### 3.反射机制相关API
1. 通过一个对象获得完整的包名和类名
```
public class TestReflect {
    public static void main(String[] args) throws Exception {
        TestReflect testReflect = new TestReflect();
        System.out.println(testReflect.getClass().getName());
        // 结果 com.gemini.test.TestReflect
    }
}
```
2. 实例化Class类对象
```
public class TestReflect {
    public static void main(String[] args) throws Exception {
        Class<?> class1 = null;
        Class<?> class2 = null;
        Class<?> class3 = null;
        // 一般采用这种形式
        class1 = Class.forName("com.gemini.test.TestReflect");
        class2 = new TestReflect().getClass();
        class3 = TestReflect.class;
        System.out.println("类名称   " + class1.getName());
        System.out.println("类名称   " + class2.getName());
        System.out.println("类名称   " + class3.getName());
    }
}
```
3. 获取一个对象的父类与实现的接口
```
import java.io.Serializable;
public class TestReflect implements Serializable {
    private static final long serialVersionUID = -2862585049955236662L;
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("net.xsoftlab.baike.TestReflect");
        // 取得父类
        Class<?> parentClass = clazz.getSuperclass();
        System.out.println("clazz的父类为：" + parentClass.getName());
        // clazz的父类为： java.lang.Object
        // 获取所有的接口
        Class<?> intes[] = clazz.getInterfaces();
        System.out.println("clazz实现的接口有：");
        for (int i = 0; i < intes.length; i++) {
            System.out.println((i + 1) + "：" + intes[i].getName());
        }
        // clazz实现的接口有：
        // 1：java.io.Serializable
    }
}

```
4. 通过反射机制实例化一个类的对象
```
import java.lang.reflect.Constructor;
public class TestReflect {
    public static void main(String[] args) throws Exception {
        Class<?> class1 = null;
        class1 = Class.forName("com.gemini.test.User");
        // 第一种方法，实例化默认构造方法，调用set赋值
        User user = (User) class1.newInstance();
        user.setAge(20);
        user.setName("Rollen");
        System.out.println(user); // 结果 User [age=20, name=Rollen]

        // 第二种方法 取得全部的构造函数 使用构造函数赋值
        Constructor<?> cons[] = class1.getConstructors();
        // 查看每个构造方法需要的参数
        for (int i = 0; i < cons.length; i++) {
            Class<?> clazzs[] = cons[i].getParameterTypes();
            System.out.print("cons[" + i + "] (");
            for (int j = 0; j < clazzs.length; j++) {
                if (j == clazzs.length - 1)
                    System.out.print(clazzs[j].getName());
                else
                    System.out.print(clazzs[j].getName() + ",");
            }
            System.out.println(")");
        }
        // 结果
        // cons[0] (java.lang.String)
        // cons[1] (int,java.lang.String)
        // cons[2] ()
        user = (User) cons[0].newInstance("Rollen");
        System.out.println(user);
        // 结果 User [age=0, name=Rollen]
        user = (User) cons[1].newInstance(20, "Rollen");
        System.out.println(user);
        // 结果 User [age=20, name=Rollen]
    }
}
class User {
    private int age;
    private String name;
    public User() {
        super();
    }
    public User(String name) {
        super();
        this.name = name;
    }
    public User(int age, String name) {
        super();
        this.age = age;
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    @Override
    public String toString() {
        return "User [age=" + age + ", name=" + name + "]";
    }
}
```
4. 获取某个类的全部属性
```
import java.io.Serializable;
import java.lang.reflect.Field;
import java.lang.reflect.Modifier;
public class TestReflect implements Serializable {
    private static final long serialVersionUID = -2862585049955236662L;
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("com.gemini.test.TestReflect");
        System.out.println("===============本类属性===============");
        Field[] field = clazz.getDeclaredFields(); // 取得本类的全部属性
        for (int i = 0; i < field.length; i++) {
            int mo = field[i].getModifiers();// 权限修饰符
            String priv = Modifier.toString(mo);
            Class<?> type = field[i].getType();// 属性类型
            System.out.println(priv + " " + type.getName() + " " + field[i].getName() + ";");
        }
        System.out.println("==========实现的接口或者父类的属性==========");
        Field[] filed1 = clazz.getFields(); // 取得实现的接口或者父类的属性
        for (int j = 0; j < filed1.length; j++) {
            int mo = filed1[j].getModifiers();// 权限修饰符
            String priv = Modifier.toString(mo);
            Class<?> type = filed1[j].getType();// 属性类型
            System.out.println(priv + " " + type.getName() + " " + filed1[j].getName() + ";");
        }
    }
}
```
5. 获取某个类的全部方法
```
import java.io.Serializable;
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
public class TestReflect implements Serializable {
    private static final long serialVersionUID = -2862585049955236662L;
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("com.gemini.test.TestReflect");
        Method method[] = clazz.getMethods();
        for (int i = 0; i < method.length; ++i) {
            Class<?> returnType = method[i].getReturnType();
            Class<?> para[] = method[i].getParameterTypes();
            int temp = method[i].getModifiers();
            System.out.print(Modifier.toString(temp) + " ");
            System.out.print(returnType.getName() + "  ");
            System.out.print(method[i].getName() + " ");
            System.out.print("(");
            for (int j = 0; j < para.length; ++j) {
                System.out.print(para[j].getName() + " " + "arg" + j);
                if (j < para.length - 1) {
                    System.out.print(",");
                }
            }
            Class<?> exce[] = method[i].getExceptionTypes();
            if (exce.length > 0) {
                System.out.print(") throws ");
                for (int k = 0; k < exce.length; ++k) {
                    System.out.print(exce[k].getName() + " ");
                    if (k < exce.length - 1) {
                        System.out.print(",");
                    }
                }
            } else {
                System.out.print(")");
            }
            System.out.println();
        }
    }
}
```
6. 通过反射机制调用某个类的方法
```
import java.lang.reflect.Method;
public class TestReflect {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("net.xsoftlab.baike.TestReflect");
        // 调用TestReflect类中的reflect1方法
        Method method = clazz.getMethod("reflect1");
        method.invoke(clazz.newInstance());
        // Java 反射机制 - 调用某个类的方法1.
        // 调用TestReflect的reflect2方法
        method = clazz.getMethod("reflect2", int.class, String.class);
        method.invoke(clazz.newInstance(), 20, "张三");
        // Java 反射机制 - 调用某个类的方法2.
        // age -> 20. name -> 张三
    }
    public void reflect1() {
        System.out.println("Java 反射机制 - 调用某个类的方法1.");
    }
    public void reflect2(int age, String name) {
        System.out.println("Java 反射机制 - 调用某个类的方法2.");
        System.out.println("age -> " + age + ". name -> " + name);
    }
}
```
7. 通过反射机制操作某个类的属性
```
import java.lang.reflect.Field;
public class TestReflect {
    private String proprety = null;
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("net.xsoftlab.baike.TestReflect");
        Object obj = clazz.newInstance();
        // 可以直接对 private 的属性赋值
        Field field = clazz.getDeclaredField("proprety");
        field.setAccessible(true);
        field.set(obj, "Java反射机制");
        System.out.println(field.get(obj));
    }
}
```
8. 反射机制的动态代理
```
// 获取类加载器的方法
TestReflect testReflect = new TestReflect();
        System.out.println("类加载器  " + testReflect.getClass().getClassLoader().getClass().getName());
package com.gemini.test;
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;
//定义项目接口
interface Subject {
    public String say(String name, int age);
}
// 定义真实项目
class RealSubject implements Subject {
    public String say(String name, int age) {
        return name + "  " + age;
    }
}
class MyInvocationHandler implements InvocationHandler {
    private Object obj = null;
    public Object bind(Object obj) {
        this.obj = obj;
        return Proxy.newProxyInstance(obj.getClass().getClassLoader(), obj.getClass().getInterfaces(), this);
    }
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        Object temp = method.invoke(this.obj, args);
        return temp;
    }
}
/**
 * 在java中有三种类类加载器。
 *
 * 1）Bootstrap ClassLoader 此加载器采用c++编写，一般开发中很少见。
 *
 * 2）Extension ClassLoader 用来进行扩展类的加载，一般对应的是jrelibext目录中的类
 *
 * 3）AppClassLoader 加载classpath指定的类，是最常用的加载器。同时也是java中默认的加载器。
 *
 * 如果想要完成动态代理，首先需要定义一个InvocationHandler接口的子类，已完成代理的具体操作。
 *
 * @author xsoftlab.net
 *
 */
public class TestReflect {
    public static void main(String[] args) throws Exception {
        MyInvocationHandler demo = new MyInvocationHandler();
        Subject sub = (Subject) demo.bind(new RealSubject());
        String info = sub.say("Rollen", 20);
        System.out.println(info);
    }
}
```
9. 将反射机制应用于工厂模式
```
interface fruit {
    public abstract void eat();
}
class  Apple implements fruit {
    public void eat() {
        System.out.println("Apple");
    }
}
class Orange implements fruit {
    public void eat() {
        System.out.println("Orange");
    }
}
class Factory {
    public static fruit getInstance(String ClassName) {
        fruit f = null;
        try {
            f = (fruit) Class.forName(ClassName).newInstance();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return f;
    }
}
/**
 * 对于普通的工厂模式当我们在添加一个子类的时候，就需要对应的修改工厂类。 当我们添加很多的子类的时候，会很麻烦。
 * Java 工厂模式可以参考
 * http://baike.xsoftlab.net/view/java-factory-pattern
 *
 * 现在我们利用反射机制实现工厂模式，可以在不修改工厂类的情况下添加任意多个子类。
 * 但是有一点仍然很麻烦，就是需要知道完整的包名和类名，这里可以使用properties配置文件来完成。
 */
public class TestReflect {
    public static void main(String[] args) throws Exception {
        fruit f = Factory.getInstance("com.gemini.test.Apple");
        if (f != null) {
            f.eat();
        }
    }
}
```
### 4.反射机制优化
1. 描述
从事java开发的都知道反射的运行速度慢，所以很多java的开发者都对反射机制的使用望而却步(包括BME组件SDO)。我想知道，究竟反射机制慢在哪里？有没有改进方法，让我们可以继续使用它？如果一个好东西因为其自身的一些缺陷而不使用它，那么实在可惜，反射也是这样。我想说的是：我们应该一点点的改进它。
2. 错误的使用方法
错误的使用方法是每次需要获取Class的对象时都使用Class.forName方法，或者需要调用Class对象上的方法时都调用getDeclaredMethod(String name, Class<?>... parameterTypes)或getMethod(String name, Class<?>... parameterTypes)方法获取Method对象，再调用其上的invoke(Object obj, Object... args)方法。
这里存在两个容易造成性能损耗的地方：
Class.forName方法的调用会执行Class类文件在整个类路径下的搜索，频繁调用比较影响性能。
Class对象上的getDeclaredMethod (String, Class<?>...)或getMethod(String, Class<?>...)方法的调用会执行Method对象在Class对象上的搜索。有些同事还使用getMethods()方法获取Method数组，然后执行搜索任务，实际上getMethods()还会执行方法对象的集体Copy比直接使用(String, Class<?>...)或getMethod(String, Class<?>...)方法还要消耗时间及空间。
3. Cache思想
Cache的思想是将需要的反射中间件给存储下来，以便以后使用。不管使用什么方法获取Class对象上的Method对象，返回的都是Method对象的copy对象。这些copy对象有的只是使用一次就被回收了，未免有些可惜。我们可这以将这些对象给缓存下来，以便以后使用。而在存储数据结构中，无疑HashMap的查找速度是最快的，它主要是通过对象的Hash码进行一次查找，速度超快。但是HashMap上的操作不是线程安全的，需要改进方法实现同步。
4. 具体实现
需要两个组件ClassInfo和ReflectionCache。
ClassInfo主要保存Class对象的信息，主要是方法Map。其中ClassInfo中包括三部分方法的Map: Getter, Setter, Other。Getter是Class的属性的获取方法，Setter是Class的属性的设置方法，Other是其它方法。需要注意的是Getter和Setter的方法需要完全符合Javabean规范(isXXX方法属于Getter方法范围内)，其key值是方法对应的属性名。Other方法是除Getter和Setter以外的其它方法。
ReflectionCache组件主要是通过HashMap对ClassInfo进行缓存。缓存的键值是ClassInfo中Class对象的全称。如一个String对象，它缓存的键值就是java.lang.String。并且ReflectionCache提供了几种不同get和put方法来方便用户的操作。
另外ClassInfo的生成需要用到ClassInfoUtils工具。它的主要工作是创建ClassInfo对象，其中创建ClassInfo时可以提供Method Type信息来指定缓存的方法类型（如：所有方法-All、存取器方法-Access、获取方法-Getter和设置方法-Setter）。
5. 同步控制
ReflectionCache中ClassInfoMap是一个静变量，那么随之而来的就是HashMap的同步问题。我对ReflectionCache的做了些改进，主要是对put方法的处理。首先HashMap的获取操作（get操作）没有加入同步操作，因此获取的操作是可以并发的。现在的问题在于如果获取不了ClassInfo对象时会要执行设置操作（set操作），此时并发问题随之而来。可能在同一时刻会有很多线程去设置ClassInfo，在第一个设置完ClassInfo的线程结束后，第二个线程应该停止设置ClassInfo。在此需求之上，我们需要对ReflectionCache的put操作上加上同步块，并且让put操作再执行一个额外的操作：返回添加到ClassInfoMap中的ClassInfo，不管它是不是其它线程添加的。因此我们在设置ClassInfo时，可以这样操作：
ClassInfo classInfo = ReflectionCache.putClassInfo(String.class);
6. 改进效率
改进之后的效率的提高是明显的。主要是节省了中间变量创建及反射数据的查找时间。测试数据:
100000次，20个线程，无Class.forName操作
一般用法: 11375 milliseconds
ReflectionCache: 2562 milliseconds
100000次，20个线程，有Class.forName操作
一般用法: 16125 milliseconds
ReflectionCache: 4187 milliseconds
可见使用ReflectionCache明显提高了效率。

伪代码如下：
```
1.默认方式
Class clazz = Class.forName("com.dianping.csc.page_config.view.entity.ViewConfig");
clazz.newInstance();
2.Cache加载Class
CachedClass classInfo = ReflectionCache.getCachedClass(ViewConfig.class);
Class clazz = classInfo.getTheClass();
3.Cache加载Method
MethodAccess methodAccess = MethodAccess.get(classInfo.getTheClass());
methodAccess.invoke();
clazz.newInstance();
```
引用用包如下：
```
<dependency>
 <groupId>org.codehaus.groovy</groupId>
 <artifactId>groovy-all</artifactId>
 <version>2.4.7</version>
</dependency>

<dependency>
 <groupId>com.esotericsoftware</groupId>
 <artifactId>reflectasm</artifactId>
 <version>1.11.3</version>
</dependency>
```
程序示例：
```
/**
 *根据Body字符串，自动封装
 * @param issueBody
 * @param obj
 * @return
 * @throws CscConfigException
 */
public static Object setJavaBeanByRequestBody(String issueBody, Object obj) throws CscConfigException {
    try {
        JsonParser jsonParser = new JsonParser();
 JsonObject jsonObject = jsonParser.parse(issueBody).getAsJsonObject();
 Map<String, String> map = ObjectUtil.getObjectPro(obj.getClass());
 Set<Map.Entry<String, String>> mapping = map.entrySet();
 MethodAccess methodAccess = MethodAccess.get(obj.getClass());
 for (Map.Entry<String, String> me : mapping) {
            String name = me.getKey();
 String type = me.getValue();
 try{
                int index_ = methodAccess.getIndex("set" + StringUtil.toFirstUp(name));
 if (type.contains("String")) {
                    if (jsonObject.get(name) != null) {
                        String setValue = "";
 try{
                            setValue = jsonObject.get(name).getAsString();
 }catch(Exception e){
                            setValue = jsonObject.get(name).toString();
 }
                        if (setValue == null) {
                            setValue = "";
 }
                        setValue = setValue.replace("&quot;", "").replace("&nbsp;", "");
 methodAccess.invoke(obj,index_,setValue);
 }
                } else if (type.contains("Long")) {
                    if (jsonObject.get(name) != null) {
                        methodAccess.invoke(obj,index_,jsonObject.get(name).getAsLong());
 }
                } else if (type.contains("Date")) {
                    if (jsonObject.get(name) != null) {
                        DateFormat dateformat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
 Date date = dateformat.parse(jsonObject.get(name).toString());

 }
                } else if (type.contains("Integer")) {
                    if (jsonObject.get(name) != null) {
                        methodAccess.invoke(obj,index_,jsonObject.get(name).getAsInt());
 }
                } else {
                }
            }catch (Exception e){
                continue;
 }

        }
    } catch (Exception e) {
        e.printStackTrace();
 throw new CscConfigException(100001,"信息获取异常");
 }
    return obj;
}
```

