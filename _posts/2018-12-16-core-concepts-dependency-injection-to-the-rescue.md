---
layout: index
title:  2. 依赖注入
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
   2. 依赖注入
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="core-concepts.html" rel="up" title="Spring In Context: Core Concepts"/>
  <link href="core-concepts.html" rel="prev" title="Spring In Context: Core Concepts"/>
  <link href="core-concepts-bean-management-through-ioc.html" rel="next" title="3. Bean management through IoC"/>
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
       <a accesskey="p" href="core-concepts.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
       Spring框架：核心概念
       </div>
       <div class="subHeaderSubTitle">
        2. 依赖注入
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="core-concepts-bean-management-through-ioc.html">
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
       <a name="core-concepts-dependency-injection-to-the-rescue">
       </a>
       2. 依赖注入
      </h2>
     </div>
    </div>
   </div>
   <p>
    依赖注入在依赖反转原则的基础上更进了一步。依赖注入中有一个概念叫做
    <span class="bold">
     <strong>
      assembler
     </strong>
    </span>
    <sup>
     [
     <a href="#ftn.d0e357" name="d0e357">
      4
     </a>
     ]
    </sup>
    – 也就是java中的所谓
    <span class="bold">
     <strong>
      Factory 
     </strong>
    </span>
    -- 
    【译者云：工厂模式中，Factory即是工厂模式中的工厂，它承担创造实例的任务。】
     它用来创造那些应用需要的对象，并且从外界注入到它们所依赖的对象。
     【译者云：上节课的VotingBooth的例子，我们需要在main方法中创建实例，但有了Factory的帮助，
     我们不再需要创造任何实例，Factory帮助我们完成这一切。】
   </p>
   <p>
    对于这种依赖注入为导向的框架，比如Spring，组件之间是通过接口进行交流，就像之前在DIP例子中所说的那样。
    现在IoC容器帮我们管理这一切，实例的创造，管理，类型转换等等，开发者就不再需要做这些工作。
    IoC容器真正意义上帮助我们实现了依赖反转，完全满足了DIP准则。
   </p>
   <p>
    有三种由IoC容器调用的依赖注入类型。
   <div class="table">
    <a name="d0e371">
    </a>
    <p class="title">
     <b>
      Table 1. 依赖注入类型
     </b>
    </p>
    <div class="table-contents">
     <table border="0" style="border-collapse: collapse;border-top: 0.5pt solid ; border-bottom: 0.5pt solid ; border-left: 0.5pt solid ; border-right: 0.5pt solid ; " summary="Dependency Injection Types">
      <colgroup>
       <col/>
       <col/>
      </colgroup>
      <thead>
       <tr>
        <th style="border-right: 0.5pt solid ; border-bottom: 0.5pt solid ; ">
         依赖注入类型
        </th>
        <th style="border-bottom: 0.5pt solid ; ">
         Description
        </th>
       </tr>
      </thead>
      <tbody>
       <tr>
        <td style="border-right: 0.5pt solid ; border-bottom: 0.5pt solid ; ">
         Constructor 注入
        </td>
        <td style="border-bottom: 0.5pt solid ; ">
         构造函数（constructor）的参数在实例化的时候被注入。
        </td>
       </tr>
       <tr>
        <td style="border-right: 0.5pt solid ; border-bottom: 0.5pt solid ; ">
         Setter 注入
        </td>
        <td style="border-bottom: 0.5pt solid ; ">
        这是Spring最广泛的一种依赖注入的方法。依赖在Spring的配置文件中定义的setter方法中被确定。
        </td>
       </tr>
       <tr>
        <td style="border-right: 0.5pt solid ; ">
         Interface 注入
        </td>
        <td style="">
         该方法目前没有被Spring使用，但是在Avalon框架中出现过。这种不同的依赖注入类型将对象映射或是注入到指定的interface中。
        </td>
       </tr>
      </tbody>
     </table>
    </div>
   </div>
   <p>
    <br class="table-break"/>
   </p>
   <p>
    Spring使用一种称作
    <code class="code">
     BeanFactory
    </code>
    作为它的assember, 正是
    <code class="code">
     BeanFactory
    </code>
    管理这些你配置的JavaBeans。在下一节我们会讨论IoC容器及它是怎样利用依赖注入模式让你的代码避免成为垃圾代码，提升你的代码质量的。
   </p>
   <div class="footnotes">
    <br/>
    <hr align="left" width="100"/>
    <div class="footnote">
     <p>
      <sup>
       [
       <a href="#d0e357" name="ftn.d0e357">
        4
       </a>
       ]
      </sup>
      Martin Fowler,
      <em class="citetitle">
       Inversion of Control Containers and The Dependency Injection Pattern
      </em>
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
      <a accesskey="p" href="core-concepts.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="core-concepts.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="core-concepts-bean-management-through-ioc.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      Spring In Context: Core Concepts
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      3. Bean management through IoC
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