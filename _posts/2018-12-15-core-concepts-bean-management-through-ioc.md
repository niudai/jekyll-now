---
layout: index
title: 3. IoC对Bean的管理
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   3. IoC对Bean的管理
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="core-concepts.html" rel="up" title="Spring In Context: Core Concepts"/>
  <link href="core-concepts-dependency-injection-to-the-rescue.html" rel="prev" title="2. Dependency Injection To The Rescue"/>
  <link href="core-concepts-our-example-in-spring-ioc.html" rel="next" title="4. Our Example In Spring IoC"/>
 </head>
 <body alink="#0000FF" bgcolor="white" link="#0000FF" text="black" vlink="#840084">
  <div id="header">
   <div id="headerTitle">
    <a href="http://www.springbyexample.org">
     Spring by Example
    </a>
   </div>
   <div class="subHeader">
    <table width="100%">
     <tr>
      <td align="left" width="10%">
       <a accesskey="p" href="core-concepts-dependency-injection-to-the-rescue.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
        Spring In Context框架：核心概念
       </div>
       <div class="subHeaderSubTitle">
        3. IoC对Bean的管理
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="core-concepts-our-example-in-spring-ioc.html">
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
       <a name="core-concepts-bean-management-through-ioc">
       </a>
       3. IoC对Bean的管理
      </h2>
     </div>
    </div>
   </div>
   <p>
    【译者云：所谓“Bean”，翻译成中文便是“豆子”，这些“豆子”其实就是开发者写的各种类，而在Spring中，围绕这些类的实例的创造，销毁等是由IoC容器完成的，所以生成“豆子”的东西叫做：“豆子工厂”。开发者只需开发这些“豆子”，剩下的交给IoC容器即可。】<br>
    在BeanFactory中，在工厂生产中，Spring的IoC容器对那些配置好的对象进行实例化。Spring对容器本身的管理增强了开发者对应用的控制力和灵活度，
    并且提供了对你的POJO的配置管理。<br>
    【译者云：所谓POJO，便是Plain Old Java Objects，说白了就是平凡的java对象，就是开发者写的那些类，那些class而已，
    Spring为你管理这些POJO的生命周期，什么时候创造一个实例，什么时候销毁，都由Spring来管理，你可以通过修改配置文件来
    告知Spring如何对你的这些POJO进行管理。】<br>
   </p>
   <p>
    比如，在Spring IoC中你可以设置需要创造的实例个数 - 不管这个组件是单例还是别的 - 还有在什么时候这个实例在内存中被创造或是被销毁。在Spring中，bean由框架操纵的实例化和使用
    <code class="code">
     new
    </code>
    关键字实例化本质上是相同的。一旦框架实例化了一个对象，那么它就会根据配置文件声明的信息而管理这个bean的作用范围，生命周期。
   </p>
   <p>
    因为IoC容器在管理这些beans，JavaEE容器中的JNDI查找就不再需要了，使框架内部和外部的单元测试更加容易进行。当你面向接口进行编程的时候，Spring允许你通过依赖注入的形式对接口的具体实现方式进行管理，使代码更干净，耦合性更低。
   </p>
   <p>
    你也可以通过配置IoC容器使得其接收某个bean的创造或销毁的event。<br>
    【译者云：所谓event，既是“事件”，就是某个对象的某个状态发生改变，就称为一个event，比如某个实例被销毁，这就是一个event，而IoC可以第一时间得知这个bean被销毁，从而做出特定的举动（callback）。】<br>
    一些组件比如数据库连接池在应用关闭的时候很显然需要初始化并销毁。你无需自己手动进行这一切，Spring框架帮你管理它们的生命周期。
   </p>
  </div>
  <div class="copyright">
   © 2008-2015 David Winterfeldt.  All rights reserved.
  </div>
  <div class="navfooter">
   <hr/>
   <table summary="Navigation footer" width="100%">
    <tr>
     <td align="left" width="40%">
      <a accesskey="p" href="core-concepts-dependency-injection-to-the-rescue.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="core-concepts.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="core-concepts-our-example-in-spring-ioc.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      2. 依赖注入
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      4. Our Example In Spring IoC
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