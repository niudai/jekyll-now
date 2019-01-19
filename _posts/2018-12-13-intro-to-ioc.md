---
layout: index
title: 控制反转实践操作
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   控制反转实践操作
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="part-intro.html" rel="up" title="Part I. Spring Introduction"/>
  <link href="core-concepts-our-example-in-spring-ioc.html" rel="prev" title="4. Our Example In Spring IoC"/>
  <link href="intro-to-ioc-basic-constructor-injection.html" rel="next" title="2. Basic Constructor Injection"/>
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
       <a accesskey="p" href="core-concepts-our-example-in-spring-ioc.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
        Part I. 初识Spring
       </div>
       <div class="subHeaderSubTitle">
       控制反转实践操作
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="intro-to-ioc-basic-constructor-injection.html">
        Next
       </a>
      </td>
     </tr>
    </table>
   </div>
  </div>
  <link href="http://www.springbyexample.org/feed/" rel="alternate" title="RSS Feed" type="application/rss+xml"/>
  <div class="article" lang="en">
   <div class="titlepage">
    <div>
     <div>
      <h1 class="title">
       <a name="intro-to-ioc">
       </a>
       控制反转实践操作
      </h1>
     </div>
     <div>
      <div class="author">
       <h3 class="author">
        <span class="firstname">
         Susan
        </span>
        <span class="surname">
         Kerschbaumer
        </span>
       </h3>
      </div>
     </div>
     <div>
      <div class="author">
       <h3 class="author">
        <span class="firstname">
         David
        </span>
        <span class="surname">
         Winterfeldt
        </span>
       </h3>
      </div>
     </div>
     <div>
      <p class="pubdate">
       2009
      </p>
     </div>
    </div>
    <hr/>
   </div>
   <p>
    如我们之前提到过的, Spring框架的核心是
    <span class="bold">
     <strong>
      Inversion of Control
     </strong>
    </span>
    容器。
    <code class="code">
     BeanFactory
    </code>
    ，也就是IoC容器会去管理java实例的创造和销毁。<br>
    【译者云：BeanFactory，就是“豆子工厂”，非常形象，它就是用来生产和销毁“豆子”的，它是IoC容器的具体实现。】<br>
    被IoC容器创造的Java实例称作beans，IoC容器也同时管理这些beans的作用范围，生命周期，
    以及所有它被配置或设定的AOP特性。<br>
    【译者云：所谓AOP，即是Aspect Oriented Programming，也就是面向切面编程。没有IoC容器之前，
    我们的代码不仅需要写这些POJOs，还需要管理这些POJOs的生命周期，实例的创造和销毁等，所以是
    OOP（Object Oriented Programming）。但现在你无需做这一切，你需要做的仅仅是写这些POJOs，
    这些POJOs是应用的各种组件，这些组件便是你程序的“方面”，也就是aspect。所以我们将其成为AOP。】<br>
   </p>
   <p>
       IoC容器使用
    <span class="emphasis">
     <em>
      依赖注入
     </em>
    </span>
    模式去连接你的组件, 降低它们的耦合度，使得各组件之间只通过接口进行交流。这章是一个简单的教学，教大家如何创造一个bean，配置这个bean，并且对它进行单元测试。
   </p>
   <div class="sect1" lang="en">
    <div class="titlepage">
     <div>
      <div>
       <h2 class="title" style="clear: both">
        <a name="intro-to-ioc-basic-bean-creation">
        </a>
        1. Bean的创建
       </h2>
      </div>
     </div>
    </div>
    <p>
    IoC容器中的bean在这里其实就是POJO。POJOs被定义为可复用的模块化组件 - 它们本质上只是普通的java类，
    而它们之间的相互依赖关系是由IoC容器进行管理的。创造一个bean和写一个普通的java类没有什么本质区别，多出的步骤仅仅是在Spring的xml配置文件中声明你写的这个类是一个bean，或者通过注解（annotation）的方式声明这是一个bean。
    </p>
    <p>
    现在开始我们的教学，我们创建一个没有声明构造函数（constructor）的普通的Java类，叫
     <code class="code">
      Message
     </code>
    ，我们只在它里面写两个方法，分别是
     <code class="code">
      getMessage()
     </code>
     和
     <code class="code">
      setMessage(String message)
     </code>。
    </p>
    <div class="example">
     <a name="d0e513">
     </a>
     <p class="title">
      <b>
       Example 1.
       <code class="code">
        DefaultMessage
       </code>
      </b>
     </p>
     <div class="example-contents">
      <pre class="programlisting">
                
public class DefaultMessage {

    private String message = "Spring is fun.";

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
     下方xml代码中的
     <span class="emphasis">
      <em>
       bean 
      </em>
     </span>
     元素代表一个
     <code class="code">
      DefaultMessage
     </code>
    类型的bean。它的id是“message”。 
     这个bean的实例会在容器中被注册。
    </p>
    <div class="informalexample">
     <span class="emphasis">
      <em>
       DefaultMessageTest-context.xml
      </em>
     </span>
     <pre class="programlisting">
                
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
	   					   http://www.springframework.org/schema/beans/spring-beans.xsd"&gt;

    &lt;bean id="message"
          class="org.springbyexample.di.xml.DefaultMessage" /&gt;

&lt;/beans&gt;
                
            </pre>
    </div>
    <p>
    当容器替你实例化了id为“
     <span class="emphasis">
      <em>
       message
      </em>
     </span>
     ”的bean的时候，本质上相当于你用'
     <code class="code">
      new DefaultMessage()
     </code>
     '创造了一个DefaultMessage实例。
    </p>
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
      <a accesskey="p" href="core-concepts-our-example-in-spring-ioc.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="part-intro.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="intro-to-ioc-basic-constructor-injection.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      4. Our Example In Spring IoC
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      2. Basic Constructor Injection
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