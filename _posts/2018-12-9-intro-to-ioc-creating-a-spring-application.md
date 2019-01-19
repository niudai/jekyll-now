---
layout: index
title: 5. 创建一个Spring应用
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   5. 创建一个Spring应用
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="intro-to-ioc.html" rel="up" title="A Practical Introduction to Inversion of Control"/>
  <link href="intro-to-ioc-reference-injection.html" rel="prev" title="4. Reference Injection"/>
  <link href="intro-to-ioc-unit-test-beans-from-application-context.html" rel="next" title="6. Unit Test Beans from Application Context"/>
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
       <a accesskey="p" href="intro-to-ioc-reference-injection.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
        控制反转实例展示
       </div>
       <div class="subHeaderSubTitle">
        5. 创建一个Spring应用
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="intro-to-ioc-unit-test-beans-from-application-context.html">
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
       <a name="intro-to-ioc-creating-a-spring-application">
       </a>
       5. 创建一个Spring应用
      </h2>
     </div>
    </div>
   </div>
   <p>
        Spring框架可以在标准应用，网络应用，JavaEE应用，或者其他的容器中使用，对开发环境唯一的需求就是JVM(java虚拟机)。
        Spring的资源抽象使你可以从任何你想要的地方导入配置文件 -- classpath，文件系统，FTP协议，HTTP协议等。你也可以使用Spring的资源抽象在你的应用中加载其他的文件。
   </p>
   <p>
        一旦IoC容器被初始化，你就可以获得所有你在配置文件中声明的那些beans。然而事实上在大多数情况下你不需要直接获取IoC容器，因为大多数时候你的IoC容器是自动完成你的控制器的实例化并且为你的控制器注入它们需要的beans.<br>
        【译者云：所谓控制器，即是controller，在网络应用中是一个重要的组成部分，它的作用是接收用户端发送的请求，比如一个HTTP请求，然后对这个请求进行处理，这里面便是你的业务逻辑，然后controller的返回值一般是MVC层中的Model，
        这个Model里面装着经过controller处理后产出的信息，然后Model被传入View层，View根据Model提供的信息渲染出页面，发送给用户端。】
    <sup>
     [
     <a href="#ftn.d0e681" name="d0e681">
      5
     </a>
     ]
    </sup>
   </p>
   <p>
        IoC容器的最底层实现是
    <code class="code">
     BeanFactory
    </code>
    , 但我们更推荐使用
    <code class="code">
     ApplicationContext
    </code>
    <code class="code">
     ApplicationContext
    </code>
    继承自
    <code class="code">
     BeanFactory
    </code>
    接口，所有
    <code class="code">
     BeanFactory
    </code>
    有的功能，它都有。
    除非你在写一个需要的内存极少的脚本，
    <code class="code">
     BeanFactory
    </code>
    一般不应该被直接调用。
   </p>
   <p>
    Spring框架中有好几种不同的
    <code class="code">
     ApplicationContext
    </code>
    的具体实现，你可以在Spring框架文档和源代码中了解它们。
    对于这个例子，我们将使用很常用的
    <code class="code">
     ClassPathXmlApplicationContext
    </code>
    , 它默认从classpath中读取配置文件。
    如果你要使用你自定义的class位置，你可以在配置文件的路径前加一个前缀，比如“file”，
    “http”等。<br>
    【译者云：所谓classpath，是java编译器对你的应用进行编译时的必须信息，java在编译你的项目时，
    会在classpath下查找所有的java源代码，然后把这些java源代码进行整合编译。换句话说，classpath之外
    的java源代码，是不能被java编译器“看到的”。】<br>
    这会使
    <code class="code">
     ApplicationContext
    </code>
    从非默认的，你指定的路径去读取配置信息。
   </p>
   <div class="example">
    <a name="d0e719">
    </a>
    <p class="title">
     <b>
      Example 4.
      <code class="code">
       MessageRunner
      </code>
     </b>
    </p>
    <div class="example-contents">
     <p>
      下面的class是一个标准的Java应用，
      <code class="code">
       main
      </code>
      方法在其内部。
      main方法的第一行创建了一个
      <code class="code">
       ClassPathXmlApplicationContext
      </code>
      的实例，将'/application-context.xml'作为参数传到了构造函数中，在这种情况下配置文件在classpath的根目录中。下面一行，
      <code class="code">
       ApplicationContext
      </code>
      的
      <code class="code">
       getBean(String beanName)
      </code>
      方法被用来从IoC容器中获取id为message的bean（上节课的）。
     </p>
     <pre class="programlisting">
                
public class MessageRunner {

    final static Logger logger = LoggerFactory.getLogger(MessageRunner.class);
    
    /**
     * Main method.
     */
    public static void main(String[] args) {
        logger.info("Initializing Spring context.");
        
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("/application-context.xml");
        
        logger.info("Spring context initialized.");

        Message message = (Message) applicationContext.getBean("message");

        logger.debug("message='" + message.getMessage() + "'");
    }

}
                
     </pre>
    </div>
   </div>
   <br class="example-break"/>
   <div class="informalexample">
    <span class="emphasis">
     <em>
      application-context.xml
     </em>
    </span>
    <pre class="programlisting">
                
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
	   					   http://www.springframework.org/schema/beans/spring-beans.xsd"&gt;

    &lt;bean id="message"
          class="org.springbyexample.di.app.Message"&gt;
        &lt;property name="message" value="Spring is fun." /&gt;
    &lt;/bean&gt;

&lt;/beans&gt;
                
            </pre>
   </div>
   <div class="footnotes">
    <br/>
    <hr align="left" width="100"/>
    <div class="footnote">
     <p>
      <sup>
       [
       <a href="#d0e681" name="ftn.d0e681">
        5
       </a>
       ]
      </sup>
      将ApplicationContext实例化并没有违反依赖反转的规则一，因为ApplicationContext是更高级的模块。
                    (见
      <a href="core-concepts.html">
       Spring框架：核心概念
      </a>
      )
     </p>
    </div>
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
      <a accesskey="p" href="intro-to-ioc-reference-injection.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="intro-to-ioc.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="intro-to-ioc-unit-test-beans-from-application-context.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      4. Reference Injection
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      6. Unit Test Beans from Application Context
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