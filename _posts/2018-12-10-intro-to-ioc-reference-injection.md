---
layout: index
title: 4. Reference 注入
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   4. Reference 注入
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="intro-to-ioc.html" rel="up" title="A Practical Introduction to Inversion of Control"/>
  <link href="intro-to-ioc-basic-setter-injection.html" rel="prev" title="3. Basic Setter Injection"/>
  <link href="intro-to-ioc-creating-a-spring-application.html" rel="next" title="5. Creating a Spring Application"/>
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
       <a accesskey="p" href="intro-to-ioc-basic-setter-injection.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
                控制反转实例展示
       </div>
       <div class="subHeaderSubTitle">
        4. Reference 注入
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="intro-to-ioc-creating-a-spring-application.html">
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
       <a name="intro-to-ioc-reference-injection">
       </a>
       4. Reference 注入
      </h2>
     </div>
    </div>
   </div>
   <p>
    【译者云：在刚才的讲解中，我们已经知道了如何将依赖注入到我们的bean中，但是这个依赖本身，到目前位置
    还只是一些普通的value，比如字符串类型，“hello world”，整数类型：8，如果我们依赖本身就是一个java的
    实例呢？】
    到目前位置我们已经通过constructor和setter的方式注入了静态变量。但是值也可以通过
    <span class="emphasis">
     <em>
                引用
     </em>
    </span>
    的方式进行传递 ——
    bean可以被注入到其他的bean中。
    为了达成此目的，我们用和
    <span class="emphasis">
     <em>
      constructor-arg
     </em>
    </span>
    和
    <span class="emphasis">
     <em>
      property
     </em>
    </span>
    的
    <span class="emphasis">
     <em>
      ref
     </em>
    </span>
    属性来完成这一切，无需使用
    <span class="emphasis">
     <em>
      value
     </em>
    </span>
    属性。<br>
    【译者云：上节课中，依赖是一个字符串，我们直接用property的value属性，给value
    赋予了一个字符串，便完成了依赖注入。但现在我们要注入的是一个对象，是一个bean，所以我们
    需要使用引用的方式，改用ref属性。】<br>
    <span class="emphasis">
     <em>
      ref
     </em>
    </span>
    的本质即是通过bean的id对另一个bean的引用。
   </p>
   <p>
    在如下的例子中，第一个bean所在的类是
    <code class="code">
     java.lang.String
    </code>
    ，id是
    <span class="emphasis">
     <em>
      springMessage
     </em>
    </span>
    。
    通过
    <span class="emphasis">
     <em>
      property
     </em>
    </span>
    元素的
    <span class="emphasis">
     <em>
      ref
     </em>
    </span>
    属性，用引用的方式将“springMessage”注入到“message”中。
   </p>
   <div class="informalexample">
    <span class="emphasis">
     <em>
      ReferenceSetterMessageTest-context.xml
     </em>
    </span>
    <pre class="programlisting">
                
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
                           http://www.springframework.org/schema/beans/spring-beans.xsd"&gt;

    &lt;bean id="springMessage" 
          class="java.lang.String"&gt;
        &lt;constructor-arg value="Spring is fun." /&gt;
    &lt;/bean&gt;

    &lt;bean id="message"
          class="org.springbyexample.di.xml.SetterMessage"&gt;
        &lt;property name="message" ref="springMessage" /&gt;
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
      <a accesskey="p" href="intro-to-ioc-basic-setter-injection.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="intro-to-ioc.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="intro-to-ioc-creating-a-spring-application.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      3. Basic Setter Injection
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      5. Creating a Spring Application
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