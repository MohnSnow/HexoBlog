---
title: web.xml详解
date: 2017-12-27 16:12:43
tags:
---
一  web.xml常用配置文件元素及其意义概览
<!--more-->
```
 <web-app>
       <!--定义了WEB应用的名字-->
       <display-name></display-name>
       <!--声明WEB应用的描述信息-->
       <description></description>

      <!--context-param元素声明应用范围内的初始化参数-->
      <context-param></context-param>

      <!--过滤器元素将一个名字与一个实现javax.servlet.Filter接口的类相关联-->
      <filter></filter>

      <!--一旦命名了一个过滤器，就要利用filter-mapping元素把它与一个或多个servlet或JSP页面相关联-->
      <filter-mapping></filter-mapping>

      <!--servlet API的版本2.3增加了对事件监听程序的支持，事件监听程序在建立、修改和删除会话或servlet环境时得到通知。
          Listener元素指出事件监听程序类-->
      <listener></listener>

      <!--在向servlet或JSP页面制定初始化参数或定制URL时，必须首先命名servlet或JSP页面。
          Servlet元素就是用来完成此项任务的-->
      <servlet></servlet>

      <!--服务器一般为servlet提供一个缺省的URL：http://host/webAppPrefix/servlet/ServletName。
          但是，常常会更改这个URL，以便servlet可以访问初始化参数或更容易地处理相对URL。
          在更改缺省URL时，使用servlet-mapping元素-->
      <servlet-mapping></servlet-mapping>

      <!--如果某个会话在一定时间内未被访问，服务器可以抛弃它以节省内存。可通过使用HttpSession的
          setMaxInactiveInterval方法明确设置单个会话对象的超时值，或者可利用session-config元素制定缺省超时值-->
      <session-config></session-config>

      <!--如果Web应用具有想到特殊的文件，希望能保证给他们分配特定的MIME类型，则mime-mapping元素提供这种保证-->
      <mime-mapping></mime-mapping>

      <!--指示服务器在收到引用一个目录名而不是文件名的URL时，使用哪个文件-->
      <welcome-file-list></welcome-file-list>

      <!--在返回特定HTTP状态代码时，或者特定类型的异常被抛出时，能够制定将要显示的页面-->
      <error-page></error-page>

      <!--对标记库描述符文件（Tag Libraryu Descriptor file）指定别名。此功能使你能够更改TLD文件的位置，
          而不用编辑使用这些文件的JSP页面-->
      <taglib></taglib>

      <!--声明与资源相关的一个管理对象-->
      <resource-env-ref></resource-env-ref>

      <!--声明一个资源工厂使用的外部资源-->
      <resource-ref></resource-ref>

      <!--制定应该保护的URL。它与login-config元素联合使用-->
      <security-constraint></security-constraint>

      <!--指定服务器应该怎样给试图访问受保护页面的用户授权。它与sercurity-constraint元素联合使用-->
      <login-config></login-config>

      <!--给出安全角色的一个列表，这些角色将出现在servlet元素内的security-role-ref元素的role-name子元素中。
          分别地声明角色可使高级IDE处理安全信息更为容易-->
      <security-role></security-role>

      <!--声明Web应用的环境项-->
      <env-entry></env-entry>

      <!--声明一个EJB的主目录的引用-->
      <ejb-ref></ejb-ref>

      <!--声明一个EJB的本地主目录的应用-->
      <ejb-local-ref></ejb-local-ref>

  </web-app>
  ```
二、各个配置文件详解
 2.1 Web应用名称：提供GUI工具可能会用来标记这个特定应用的一个名称
<display-name>Tomcat Example</display-name>


 2.2 Web应用描述：给出与此应用相关的说明性文本
<disciption>Tomcat Example servlets and JSP pages.</disciption>


2.3上下文参数：生命应用范围内的初始化参数
<context-param>
    <param-name>参数名</para-name>
    <param-value>参数值</param-value>
    <description>参数描述</description>
</context-param>
可以通过sce.getServletContex.getInitParameter("参数名")获得参数的取值，其中sce是一个ServletContexEvent实例，可以在容器开启时执行连接数据库等操作。

2.4过滤器配置：在请求和相应对象在Servlet处理之前或之后，可以通过此此过滤器对两个对象进行处理。

        filter-class 中指定的过滤器类须继承 javax.servlet.Filter 具有须有以下三种方法

                init(FilterConfig filterConfig)：初始化;一般情况下时读取配置文件中的init-param参数值 如 filterConfig.getInitParameter("encoding")

                doFilter(...)：用于对request,response进行处理，并能过chain.doFilter(...) 交过下一个控制器

               destroy()：资源销毁

       例如编码过滤器：
```
<filter>
	<filter-name>encodingfilter</filter-name>
	<filter-class>com.my.app.EncodingFilter</filter-class>
	<init-param>
		<param-name>encoding</param-name>
		<param-value>UTF-8</param-value>
	</init-param>
</filter>
<filter-mapping>
	<filter-name>encodingfilter</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
```
java代码：
```
/**
*
*/
package com.myapp;

import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
* @author louisliao
*
*/
public class EncodingFilter implements Filter {

	/**
	* 配置中默认的字符编码
	*/
	protected String encoding = null;
	protected FilterConfig filterConfig;
	/**
	* 当没有指定默认编码时是否允许跳过过滤
	*/
	protected boolean ignore = true;
	/**
	*
	*/
	public EncodingFilter() {
		// TODO Auto-generated constructor stub
	}

	/* (non-Javadoc)
	* @see javax.servlet.Filter#destroy()
	*/
	public void destroy() {
		// TODO Auto-generated method stub
		this.encoding=null;
		this.filterConfig=null;
	}

	/* (non-Javadoc)
	* @see javax.servlet.Filter#doFilter(javax.servlet.ServletRequest, javax.servlet.ServletResponse, javax.servlet.FilterChain)
	*/
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		// TODO Auto-generated method stub
		HttpServletRequest hRequest=(HttpServletRequest)request;
		HttpServletResponse hResponse=(HttpServletResponse)response;
		//Conditionally select and set the character encoding to be used
		if(ignore || hRequest.getCharacterEncoding()==null){
			String coding=selectEncoding(hRequest);
			if(coding!=null){
				hRequest.setCharacterEncoding(coding);
				hResponse.setCharacterEncoding(coding);
			}
		}
		//将控制器传向下一个filter
		chain.doFilter(hRequest, hResponse);

	}

	/* (non-Javadoc)
	* @see javax.servlet.Filter#init(javax.servlet.FilterConfig)
	*/
	public void init(FilterConfig filterConfig) throws ServletException {
		// TODO Auto-generated method stub
		this.filterConfig=filterConfig;
		this.encoding=filterConfig.getInitParameter("encoding");
		System.out.println(this.encoding);
		String value = filterConfig.getInitParameter("ignore");
		if (value == null) {
			this.ignore = true;
		} else if (value.equalsIgnoreCase("true")) {
			this.ignore = true;
		} else if (value.equalsIgnoreCase("yes")) {
			this.ignore = true;
		} else {
			this.ignore = false;
		}
	}
	protected String selectEncoding(ServletRequest request) {
	return (this.encoding);
	}
}
```
init方法是在WEB应用启动就会调用,doFilter则是在访问filter-mapping映射到的url时会调用。
2.5 监听器配置：
Servlet监听器是Servlet规范中定义的一种特殊类，用于监听ServletContext、HttpSession和ServletRequest等域对象的创建与销毁事件，以及监听这些域对象中属性发生修改的事件。

监听对象：

1、ServletContext：application，整个应用只存在一个

2、HttpSession：session，针对每一个对话

3、ServletRequest：request，针对每一个客户请求

监听内容：创建、销毁、属性改变事件

监听作用：可以在事件发生前、发生后进行一些处理，一般可以用来统计在线人数和在线用户、统计网站访问量、系统启动时初始化信息等。

<listener>
    <listerner-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
监听器的分类：

用于监听应用程序环境对象(ServletContext)的事件监听器，实现ServletContextListener、ServletContextAttributeListener接口
用于监听用户会话对象(HttpSeesion)的事件监听器，实现HttpSessionListener、HttpSessionAttributeListener接口
用于监听请求消息对象(ServletRequest)的事件监听器，实现ServletRequestListener、ServletRequestAttributeListener接口
2.6 Servlet配置：
<servlet>
     <servlet-name>servlet名称</servlet-name>
     <servlet-class>servlet类全路径</servlet-class>
     <init-param>
         <param-name>参数名</param-name>
         <param-value>参数值</param-value>
     </init-param>
     <run-as>
         <description>Security role for anonymous access</description>
         <role-name>tomcat</role-name>
     </run-as>
  　 <load-on-startup>指定当Web应用启动时，装载Servlet的次序</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>servlet名称</servlet-name>
    <url-pattern>映射路径</url-pattern>
</servlet-mapping>
2.7 会话超时配置（单位为分钟）：
设置session的有效期，单位分钟

<session-config>
     <session-timeout>120</session-timeout>
</session-config>
2.8 Web应用图标：指出IDE和GUI工具用来表示Web应用的大图标和小图标
 <icon>
      <small-icon>/images/app_small.gif</small-icon>
      <large-icon>/images/app_large.gif</large-icon>
</icon>


2.9 MIME类型配置：
<mime-mapping>
     <extension>htm</extension>
     <mime-type>text/html</mime-type>
</mime-mapping>


2.10指定欢迎页面配置
<welcome-file-list>
     <welcome-file>index.jsp</welcome-file>
     <welcome-file>index.html</welcome-file>
     <welcome-file>index.htm</welcome-file>
</welcome-file-list>


2.11配置错误页面
通过错误码来配置error-page

<!--配置了当系统发生404错误时，跳转到错误处理页面NotFound.jsp-->
<error-page>
      <error-code>404</error-code>
      <location>/NotFound.jsp</location>
</error-page>
通过异常类型来配置error-page

<!--配置了当系统发生java.lang.NullException（即空指针异常）时，跳转到错误处理页面error.jsp-->
<error-page>
      <exception-type>java.lang.NullException</exception-type>
      <location>/error.jsp</location>
</error-page>
2.12TLD配置：
<taglib>
	<taglib-uri>http://jakarta.apache.org/tomcat/debug-taglib</taglib-uri>
    <taglib-location>/WEB-INF/jsp/debug-taglib.tld</taglib-location>
</taglib>


2.13资源管理对象配置
 <resource-env-ref>
      <resource-env-ref-name>jms/StockQueue</resource-env-ref-name>
 </resource-env-ref>


2.14资源工厂配置
 <resource-ref>
      <res-ref-name>mail/Session</res-ref-name>
      <res-type>javax.mail.Session</res-type>
      <res-auth>Container</res-auth>
 </resource-ref>


2.15安全限制配置
 <security-constraint>
       <display-name>Example Security Constraint</display-name>
       <web-resource-collection>
           <web-resource-name>Protected Area</web-resource-name>
           <url-pattern>/jsp/security/protected/*</url-pattern>
           <http-method>DELETE</http-method>
           <http-method>GET</http-method>
           <http-method>POST</http-method>
           <http-method>PUT</http-method>
       </web-resource-collection>
       <auth-constraint>
           <role-name>tomcat</role-name>
           <role-name>role1</role-name>
       </auth-constraint>
 </security-constraint>


2.16登录验证配置
<login-config>
     <auth-method>FORM</auth-method>
     <realm-name>Example-Based Authentiation Area</realm-name>
   <form-login-config>
          <form-login-page>/jsp/security/protected/login.jsp</form-login-page>
          <form-error-page>/jsp/security/protected/error.jsp</form-error-page>
     </form-login-config>
</login-config>


2.17安全角色：security-role元素给出安全角色的一个列表，这些角色将出现在servlet元素内的security-role-ref元素的role-name子元素中。
分别地声明角色可使高级IDE处理安全信息更为容易。
<security-role>
     <role-name>tomcat</role-name>
</security-role>


2.18Web环境参数：env-entry元素生命Web应用的环境项
<env-entry>
     <env-entry-name>minExemptions</env-entry-name>
     <env-entry-value>1</env-entry-value>
     <env-entry-type>java.lang.Integer</env-entry-type>
</env-entry>


2.19EJB声明
<ejb-ref>
     <description>Example EJB reference</decription>
     <ejb-ref-name>ejb/Account</ejb-ref-name>
     <ejb-ref-type>Entity</ejb-ref-type>
     <home>com.mycompany.mypackage.AccountHome</home>
     <remote>com.mycompany.mypackage.Account</remote>
</ejb-ref>


2.20本地EJB声明
<ejb-local-ref>
     <description>Example Loacal EJB reference</decription>
     <ejb-ref-name>ejb/ProcessOrder</ejb-ref-name>
     <ejb-ref-type>Session</ejb-ref-type>
     <local-home>com.mycompany.mypackage.ProcessOrderHome</local-home>
     <local>com.mycompany.mypackage.ProcessOrder</local>
</ejb-local-ref>






























