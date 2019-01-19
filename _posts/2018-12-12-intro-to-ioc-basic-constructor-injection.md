---
layout: index
title: 2. constructor注入
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   2. constructor注入
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="intro-to-ioc.html" rel="up" title="A Practical Introduction to Inversion of Control"/>
  <link href="intro-to-ioc.html" rel="prev" title="A Practical Introduction to Inversion of Control"/>
  <link href="intro-to-ioc-basic-setter-injection.html" rel="next" title="3. Basic Setter Injection"/>
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
       <a accesskey="p" href="intro-to-ioc.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
        控制反转实例展示
       </div>
       <div class="subHeaderSubTitle">
        2. constructor函数注入
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="intro-to-ioc-basic-setter-injection.html">
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
       <a name="intro-to-ioc-basic-constructor-injection">
       </a>
       2. 构造函数注入
      </h2>
     </div>
    </div>
   </div>
   <p>
    现在我们有了刚才id为‘message’的bean的java类和基本的配置信息，现在我们可以展示第一个依赖注入
    的例子。通过xml配置文件，你可以在配置bean的时候告知IoC容器你需要传给constructor的具体参数。
    Spring会帮你把这些变量注入到bean中。这就是所谓的 
    <span class="bold">
     <strong>
      构造函数注入
     </strong>
    </span>
    。
   </p>
   <p>
    在如下的例子中，String message 是通过构造函数来初始化的。这个例子和之前的例子基本相同，
    <a href="intro-to-ioc.html#intro-to-ioc-basic-bean-creation" title="1. Basic Bean Creation">
     bean的创建
    </a>
    基本相同，除了
    <code class="code">
     message
    </code>
    的默认值是
    <code class="code">
     null
    </code>
    ，也就是没有给定，所以它的实例创建必须要传递一个String到constructor内部，
    message才能有确切的值。
   </p>
   <div class="example">
    <a name="d0e561">
    </a>
    <p class="title">
     <b>
      Example 2.
      <code class="code">
       ConstructorMessage
      </code>
     </b>
    </p>
    <div class="example-contents">
     <pre class="programlisting">
                
public class ConstructorMessage {

    private String message = null;

    /**
     * Constructor
     */
    public ConstructorMessage(String message) {
        this.message = message;
    }

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
    配置文件和上一节基本一样，除了新增加的
    <span class="emphasis">
     <em>
      constructor-arg
     </em>
    </span>
    元素。
    <span class="emphasis">
     <em>
      constructor-arg
     </em>
    </span>
    元素会在bean被实例化的时侯作为构造函数的唯一参数被注入进去。
   </p>
   <div class="informalexample">
    <span class="emphasis">
     <em>
      ConstructorMessageTest-context.xml
     </em>
    </span>
    <pre class="programlisting">
                
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
	   					   http://www.springframework.org/schema/beans/spring-beans.xsd"&gt;

    &lt;bean id="message"
          class="org.springbyexample.di.xml.ConstructorMessage"&gt;
        &lt;constructor-arg value="Spring is fun." /&gt;
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
      <a accesskey="p" href="intro-to-ioc.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="intro-to-ioc.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="intro-to-ioc-basic-setter-injection.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      A Practical Introduction to Inversion of Control
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      3. Basic Setter Injection
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