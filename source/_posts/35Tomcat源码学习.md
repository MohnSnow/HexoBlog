---
title: IntelliJ IDEA运行Tomcat源码环境的搭建
date: 2019-05-29 19:18:17
tags: Tomcat
toc: true
---
#### 总览
在进行搭建之前，我们首先来说一下总体的思路。
我们知道Tomcat运行的时候，一部分是源代码编译以后的可运行的Jar,另外一部分则是运行时的环境
（也就是我们从官方下载下来的二进制分发包中的一系列的配置文件以及目录结构，说的更直白点就是CATALINA_HOME环境变量指定的目录）,
<!--more-->
本文对于第一部分采用IntelliJ IDEA 运行tomcat-8.5.41 tag的源代码，
而对于第二部分运行环境，我们则直接采用tomcat-8.5.41的二进制分发包。明白了上述的思路以后，咋们就来一步步的搭建吧。
首先咋们来看看搭建完成以后的总体的目录结构，然后再一步步的去分解搭建过程。笔者搭建完以后，最终的运行结构如下图所示：
![最终效果](last.png)
下面分别解释一下上图工程结构中涉及到的文件和目录：
1. .idea和tomcat-study.iml是IntelliJ IDEA的文件，如果你用Eclipse的话不会存在这两个东东 。
2. catalina-home是从官方下载的8.5.41的二进制分发包解压后的目录。
3. target是Maven编译项目以后生成的文件夹，熟悉Maven的读者应该很熟悉此目录。
4. tomcat-8.5.41-sourcecode是从Tomcat 官方仓库 下载的tags的源代码，或点此下载tomcat8.5.41源码。
5. pom.xml是Maven的配置文件,此工程中有两个pom.xml，这里运用了Maven聚合的特性。
6. 了解了最终的结构以后，咋们就来一步步的搭建它吧。
#### 一.创建项目目录结构
本文假设我们将项目放在 /Users/MengDexin/workspace/apache 目录中。
首先创建：tomcat-study 文件夹

#### 二.下载Tomcat二进制分发包
也就是：apache-tomcat-8.5.41.zip
解压重命名为：catalina-home
然后把这个文件夹移到tomcat-study 文件夹中
#### 三.下载Tomcat源代码
也就是：apache-tomcat-8.5.41-src.zip
解压重命名为：catalina-tomcat-source
然后把这个文件夹移到tomcat-study 文件夹中

#### 四.catalina-tomcat-source文件夹中创建pom.xml文件
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
 
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>catalina-tomcat-source</artifactId>
    <name>catalina-tomcat-source</name>
    <version>8.5.41</version>
 
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.easymock</groupId>
            <artifactId>easymock</artifactId>
            <version>3.4</version>
        </dependency>
        <dependency>
            <groupId>org.apache.ant</groupId>
            <artifactId>ant</artifactId>
            <version>1.7.0</version>
        </dependency>
        <dependency>
            <groupId>wsdl4j</groupId>
            <artifactId>wsdl4j</artifactId>
            <version>1.6.2</version>
        </dependency>
        <dependency>
            <groupId>javax.xml</groupId>
            <artifactId>jaxrpc</artifactId>
            <version>1.1</version>
        </dependency>
        <dependency>
            <groupId>org.eclipse.jdt.core.compiler</groupId>
            <artifactId>ecj</artifactId>
            <version>4.5.1</version>
        </dependency>
    </dependencies>

    <build>
        <finalName>tomcat</finalName>
        <sourceDirectory>java</sourceDirectory>
        <testSourceDirectory>test</testSourceDirectory>
        <resources>
            <resource>
                <directory>java</directory>
            </resource>
        </resources>
        <testResources>
            <testResource>
                <directory>test</directory>
            </testResource>
        </testResources>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```
#### 五.catalina-study文件夹中创建根pom.xml文件
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

   <modelVersion>4.0.0</modelVersion>
   <groupId>net.imtiger</groupId>
   <artifactId>tomcat-study</artifactId>
   <name>Tomcat 7.0 Study</name>
   <version>1.0</version>
   <packaging>pom</packaging>

   <modules>
      <module>tomcat-7.0.75-sourcecode</module>
   </modules>
</project>
```
#### 六.用IntelliJ IDEA 打开项目根目录的pom.xml
这一步需要注意，要用IDEA 打开项目根目录的pom.xml文件
#### 七.运行Tomcat
Edit Configurations -> 点击+号 -> Application  开始相关配置：
Main Class: org.apache.catalina.startup.Bootstrap
BM Options: 
```
-Dcatalina.home=catalina-home 
-Dcatalina.base=catalina-home 
-Djava.endorsed.dirs=catalina-home/endorsed 
-Djava.io.tmpdir=catalina-home/temp 
-Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager 
-Djava.util.logging.config.file=catalina-home/conf/logging.properties
```
配置好的页面如下：
![界面](jiemian.png)
这时候会出现一个报错：
![错误](error.png)
需要增加这个测试Util类
```
/*
 * Licensed to the Apache Software Foundation (ASF) under one or more
 * contributor license agreements.  See the NOTICE file distributed with
 * this work for additional information regarding copyright ownership.
 * The ASF licenses this file to You under the Apache License, Version 2.0
 * (the "License"); you may not use this file except in compliance with
 * the License.  You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package util;

import java.util.Locale;
import java.util.StringTokenizer;

/**
 * Processes a cookie header and attempts to obfuscate any cookie values that
 * represent session IDs from other web applications. Since session cookie names
 * are configurable, as are session ID lengths, this filter is not expected to
 * be 100% effective.
 *
 * It is required that the examples web application is removed in security
 * conscious environments as documented in the Security How-To. This filter is
 * intended to reduce the impact of failing to follow that advice. A failure by
 * this filter to obfuscate a session ID or similar value is not a security
 * vulnerability. In such instances the vulnerability is the failure to remove
 * the examples web application.
 */
public class CookieFilter {

    private static final String OBFUSCATED = "[obfuscated]";

    private CookieFilter() {
        // Hide default constructor
    }

    public static String filter(String cookieHeader, String sessionId) {

        StringBuilder sb = new StringBuilder(cookieHeader.length());

        // Cookie name value pairs are ';' separated.
        // Session IDs don't use ; in the value so don't worry about quoted
        // values that contain ;
        StringTokenizer st = new StringTokenizer(cookieHeader, ";");

        boolean first = true;
        while (st.hasMoreTokens()) {
            if (first) {
                first = false;
            } else {
                sb.append(';');
            }
            sb.append(filterNameValuePair(st.nextToken(), sessionId));
        }


        return sb.toString();
    }

    private static String filterNameValuePair(String input, String sessionId) {
        int i = input.indexOf('=');
        if (i == -1) {
            return input;
        }
        String name = input.substring(0, i);
        String value = input.substring(i + 1, input.length());

        return name + "=" + filter(name, value, sessionId);
    }

    public static String filter(String cookieName, String cookieValue, String sessionId) {
        if (cookieName.toLowerCase(Locale.ENGLISH).contains("jsessionid") &&
                (sessionId == null || !cookieValue.contains(sessionId))) {
            cookieValue = OBFUSCATED;
        }

        return cookieValue;
    }
}

```
这时候就可以起来了
#### 八.参考文档
- http://www.tuicool.com/articles/Rz6Fnyf
- http://www.jb51.net/article/95120.htm
- http://blog.csdn.net/catontower/article/details/8559623
- http://www.suiyiwen.com/question/4411



