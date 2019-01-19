---
layout: index
title: 3. Setter注入
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   3. Setter注入
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="intro-to-ioc.html" rel="up" title="A Practical Introduction to Inversion of Control"/>
  <link href="intro-to-ioc-basic-constructor-injection.html" rel="prev" title="2. Basic Constructor Injection"/>
  <link href="intro-to-ioc-reference-injection.html" rel="next" title="4. Reference Injection"/>
 </head>
 <body alink="#0000FF" bgcolor="white" link="#0000FF" text="black" vlink="#840084">
  <div id="header">
   <div id="headerTitle">
    <a href="http://www.springbyexample.org">
     实例驱动学习之Spring框架
    </a>
   </div>
   <div class="subHeader">
    <table width="100%">
     <tr>
      <td align="left" width="10%">
       <a accesskey="p" href="intro-to-ioc-basic-constructor-injection.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
        控制反转实例展示
       </div>
       <div class="subHeaderSubTitle">
        3. Basic Setter Injection
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="intro-to-ioc-reference-injection.html">
        Next
       </a>
      </td>
     </tr>
    </table>
   </div>
  </div>
  <link href="http://www.springbyexample.org/feed/" rel="alternate" title="RSS Feed" type="application/rss+xml"/>
  <div class="sect1" lang="en">
   <div class="titlepage">
    <div>
     <div>
      <h2 class="title" style="clear: both">
       <a name="intro-to-ioc-basic-setter-injection">
       </a>
       3. Setter注入
      </h2>
     </div>
    </div>
   </div>
   <p>
    IoC容器同样支持
    <span class="bold">
     <strong>
      setter注入
     </strong>
    </span>
    , 这种方法在Spring中很常用。在IoC容器的帮助下，
    <code class="code">
     setter
    </code>
   方法会获取在xml配置文件中声明的和setter对应的变量同名的property（见下方代码）。
   </p>
   <p>
    从配置文件的角度看，setter注入更易读，因为声明的property可以看作bean的属性，property属性里包含了变量名和变量本身。
   </p>
   <p>
    对于property的命名，Spring遵循JavaBeans的规范：<br>
            (
    <a href="http://www.oracle.com/technetwork/java/javase/documentation/spec-136004.html" target="_top">
     http://www.oracle.com/technetwork/java/javase/documentation/spec-136004.html
    </a>
    ).
   </p>
   <p>
    在大多数情况下，Spring会使用setter方法名中，在“set”之后的那部分，并且把第一个大写字母转换成小写，将这部分作为property的名称。比如对于
    <code class="code">
     setMessage()
    </code>
    方法来讲，property的名称是“message”，去掉set，将第一个字母变成小写，很简单。 再比如
    <code class="code">
     setFirstName()
    </code>
    方法，property的名称就为“firstName”。
   </p>
   <p>
    但如果是set后字母全为大写的话，Spring则对set后面的所有字母保持大写，将其作为property名称。比如：
    <code class="code">
     setXML()
    </code>
    property的名称则为“XML”。
   </p>
   <p>
    因为Spring是根据setter方法名决定property名的，你的setter方法的方法名必须要遵循
    JavaBeans的规范，或者至少在你自己的应用中秉承一致的规则。看下面的例子：
   </p>
   <div class="example">
    <a name="d0e616">
    </a>
    <p class="title">
     <b>
      Example 3.
      <code class="code">
       SetterMessage
      </code>
     </b>
    </p>
    <div class="example-contents">
     <pre class="programlisting">
                
public class SetterMessage {

    private String message = null;

    /**
     * Gets message.
     */
    public String getMessage() {
        return message;
    }

    /**
     * Sets message.
     */
    public void setMessage(String message) {
        this.message = message;
    }

}
                
            </pre>
    </div>
   </div>
   <br class="example-break"/>
   <p>
    <span class="emphasis">
     <em>
      property
     </em>
    </span>
    元素被用来定义setter注入。
   </p>
   <div class="informalexample">
    <span class="emphasis">
     <em>
      SetterMessageTest-context.xml
     </em>
    </span>
    <pre class="programlisting">
                
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
	   					   http://www.springframework.org/schema/beans/spring-beans.xsd"&gt;

    &lt;bean id="message"
          class="org.springbyexample.di.xml.SetterMessage"&gt;
        &lt;property name="message" value="Spring is fun." /&gt;
    &lt;/bean&gt;

&lt;/beans&gt;
                
            </pre>
   </div>
  </div>
  <div class="copyright">
   © 2008-2015 David Winterfeldt.  All rights reserved.
  </div>
  <div class="navfooter">
   <hr/>
   <table summary="Navigation footer" width="100%">
    <tr>
     <td align="left" width="40%">
      <a accesskey="p" href="intro-to-ioc-basic-constructor-injection.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="intro-to-ioc.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="intro-to-ioc-reference-injection.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      2. Basic Constructor Injection
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      4. Reference Injection
     </td>
    </tr>
   </table>
  </div>
  <script type="text/javascript">
   var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "http://www.");
document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));
  </script>
  <script type="text/javascript">
   var pageTracker = _gat._getTracker("UA-3737499-1");
pageTracker._initData();
pageTracker._trackPageview();
  </script>
 </body>
</html>