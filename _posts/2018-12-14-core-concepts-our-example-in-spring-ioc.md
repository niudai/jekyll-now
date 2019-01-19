---
layout: index
title: 4. Spring IoC实例展示
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   4. Spring IoC实例展示
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="core-concepts.html" rel="up" title="Spring In Context: Core Concepts"/>
  <link href="core-concepts-bean-management-through-ioc.html" rel="prev" title="3. Bean management through IoC"/>
  <link href="intro-to-ioc.html" rel="next" title="A Practical Introduction to Inversion of Control"/>
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
       <a accesskey="p" href="core-concepts-bean-management-through-ioc.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
       Spring框架：核心概念
       </div>
       <div class="subHeaderSubTitle">
        4. Spring IoC实例展示
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="intro-to-ioc.html">
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
       <a name="core-concepts-our-example-in-spring-ioc">
       </a>
       4. Spring IoC实例展示
      </h2>
     </div>
    </div>
   </div>
   <p>
    所以我们如何在IoC容器中配置我们的之前的投票箱程序呢？
   </p>
   <p>
    我们的代码保持原样，无需改变。我们需要做的只是在xml格式的配置文件中告知Spring：
    <span class="emphasis">
     <em>
      recorder
     </em>
    </span>
    bean 由
    <code class="code">
     LocalVoteRecorder
    </code>
    进行实现。如下：
   </p>
   <p>
   </p>
   <pre class="programlisting">
                
&lt;bean id="recorder"
      class="com.springindepth.LocalVoteRecorder" /&gt;
                
            </pre>
   <p>
   </p>
   <p>
    然后我们只需通过setter注入的方法将
    <span class="emphasis">
     <em>
      recorder
     </em>
    </span>
    注入到
    <code class="code">
     VotingBooth
    </code>
    中。<br>
    【译者云：在配置文件中声明了property之后，spring框架会创造一个voteRecorder实例，将其作为votingBooth中setter方法的参数注入到votingBooth内部。
   </p>
   <p>
   </p>
   <pre class="programlisting">
                
&lt;bean id="votingBooth"
      class="com.springindepth.VotingBooth"&gt;
    &lt;property name="voteRecorder" ref="recorder"/&gt;
&lt;/bean&gt;
                
            </pre>
   <p>
   </p>
   <p>
    神奇的Spring框架会为你处理类的实例化，所以你的应用代码无需在意任何类的实例化。现在在配置文件和Spring框架的帮助下，通过
    依赖注入，我们最终成功地，彻底地去除了高层模块对底层模块的内部依赖，完全实现了代码之间的解耦，实现了真正的依赖反转！
    【译者云：为什么叫做“反转”呢？在引入依赖注入思想前，我们的代码的高层模块内部包含有低层模块，也就是说我们高层模块从内部
    依赖于低层模块，然而现在高层模块的内部并没有任何关于低层模块的实现和实例化，销毁，反而是低层模块需要根据配置文件决定它要被注入到哪里，也就是所谓的“依赖反转”】。
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
      <a accesskey="p" href="core-concepts-bean-management-through-ioc.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="core-concepts.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="intro-to-ioc.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      3. IoC对Bean的管理
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      A Practical Introduction to Inversion of Control
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