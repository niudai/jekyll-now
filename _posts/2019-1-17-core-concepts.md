---
layout: index
title: Spring框架：核心概念
categories: [spring]
---
<html>
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <title>
  Spring框架: 核心概念
  </title>
  <link href="css/stylesheet.css" rel="stylesheet" type="text/css"/>
  <meta content="DocBook XSL Stylesheets V1.70.0" name="generator"/>
  <link href="index.html" rel="start" title="
Spring by Example
"/>
  <link href="part-intro.html" rel="up" title="Part I. Spring Introduction"/>
  <link href="part-intro.html" rel="prev" title="Part I. Spring Introduction"/>
  <link href="core-concepts-dependency-injection-to-the-rescue.html" rel="next" title="2. Dependency Injection To The Rescue"/>
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
       <a accesskey="p" href="part-intro.html">
        Prev
       </a>
      </td>
      <td align="center" width="80%">
       <div class="subHeaderTitle">
        Part I. 初识Spring
       </div>
       <div class="subHeaderSubTitle">
        Spring框架: 核心概念
       </div>
      </td>
      <td align="right" width="10%">
       <a accesskey="n" href="core-concepts-dependency-injection-to-the-rescue.html">
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
       <a name="core-concepts">
       </a>
       Spring框架: 核心概念
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
   </p>
   <div class="blockquote">
    <table border="0" cellpadding="0" cellspacing="0" class="blockquote" summary="Block quote" width="100%">
     <tr>
      <td valign="top" width="10%">
      </td>
      <td valign="top" width="80%">
       <p>
        ...编程实践中一个东西已经被反复提及: "一坨屎"。一坨屎是专门指那种结构糟糕，臃肿，草率，
        代码高耦合，像一团线或是意大利面那般缠绕在一起...为什么这些垃圾代码如此之多？...我们是
        否能避免它？有必要避免吗？怎样让程序变得更完善？
       </p>
      </td>
      <td valign="top" width="10%">
      </td>
     </tr>
     <tr>
      <td valign="top" width="10%">
      </td>
      <td align="right" colspan="2" valign="top">
       --
       <span class="attribution">
        <span class="bold">
         <strong>
          一坨屎
         </strong>
        </span>
        , by Brian Foote and Joseph Yoder
       </span>
      </td>
     </tr>
    </table>
   </div>
   <p>
   </p>
   <p>
    每个人都知道像屎一样的代码是什么样的。你一定写过这样的代码，或者读到过，或者你尝试重构过它们。屎代码结构混乱，难以维护 -- 
    这些代码在1990's年代迅速增多，当时经济危机，金融泡沫横行，所以那时软件应用的开发有速度上的需求，技术人员更替很快，核心技术想往常一样
    在改进，为的就是增强这些代码的可扩展性。
   </p>
   <p>
    今天屎代码变得更多，更多的应用被这些垃圾代码所填充，威胁到了那些结构良好的代码的生存。结构糟糕，难以重构的应用就像是灾难 -- 对这些代码
    进行维护费事费力，往往效果还不如意。一些屎代码糟糕到根本无法进行维护。
   </p>
   <p>
    幸运的是，随着网络应用开始逐渐迁移到J2EE平台（就是现在的Java EE），Java EE的设计模式逐渐成型。<a href="http://www.oracle.com/technetwork/java/blueprints-141945.html" target="_top">
        http://www.oracle.com/technetwork/java/blueprints-141945.html
       </a>像Struts和Avalon这样的框架为网络应用提供了更好的规范，
    好的实践开始涌现，并且反过来影响这些框架的发展。Spring框架是以由Struts和Avalon引入的概念上进行扩展，并增加了其特有的元素：超级轻量化的控制反转容器。
    Spring之所以和其他框架不同，是因为其可以和任何Java组件，包括POJOs（Plain Old Java Objects）发生作用。
   </p>
   <p>
    这一章是从宏观角度如手，我们将逐步探索Spring框架背后的核心概念，并讲述它给Java EE面对对象编程方法带来了何种影响。我们也同时会
    简短地总结一些Ioc容器之外的特色，并阐述这些特色如果相互作用，共同工作地。
   </p>
   <div class="sect2" lang="en">
    <div class="titlepage">
     <div>
      <div>
       <h3 class="title">
        <a name="core-concepts-what-makes-a-framework-work">
        </a>
        什么在驱动框架工作？
       </h3>
      </div>
     </div>
    </div>
    <p>
    框架本质上就是一个骨架，你的应用就如肌肉，包裹在这个骨架之上。框架的设计遵循设计模式，由无法被开发者改变或调整的那些结构性组件和可被调整的
    部分所组成。开发者只能在骨骼上添加肌肉，也就是在“可被调整或改变”的部分上做文章，而这一部分就是java的POJOs（java中的各种类）组成。这些POJOs
    会运行在框架之上。
    </p>
    <p>
    在这章中，我们将探索Spring最重要的一个部分 - Ioc容器 - 还有Spring框架是如何引导你更好的进行面向对象编程，并且最终转换为“面向
    切面编程”（Aspect Oriented Programming）。Spring框架无法让垃圾代码变好，但是它可以趋势你和你的同事们写出结构良好，可复用的，
    可读性高的，易于管理的应用组件。
    </p>
   </div>
   <div class="sect1" lang="en">
    <div class="titlepage">
     <div>
      <div>
       <h2 class="title" style="clear: both">
        <a name="core-concepts-spring-and-ioc">
        </a>
        1. Spring框架与控制反转（Inversion of Control)
       </h2>
      </div>
     </div>
    </div>
    <p>
    很多人对Ioc容器抱有误解或是混淆 - 一些人将它和设计模式中的
     <span class="bold">
      <strong>
        “依赖注入”
      </strong>
     </span>
     – 
     （Dependency 
     Injection）等同 - 但是事实上IoC涵盖的东西比依赖注入要多很多。IoC容器在它的很多种具体形式中使用了
     依赖注入这种设计模式，并且还使用了很多其他的设计模式。
    </p>
    <p>
    控制反转背后的主要思想是组件之间的依赖，生命周期事件，还有组件之外的一些配置信息是独立于这些组件本身之外的（这些信息
    被储存在Spring框架中）。这听起来感觉放弃了很多开放上的自由度，失去了一些对开发的控制力，但事实上它让你的代码更易管理，
    更易测试，更加便携。
    </p>
    <p>
    在我们详细讨论Spring Ioc容器前，我们必须理解最基本的依赖注入设计模式以及它是怎样在面对对象编程中运用的。Spring的控制反转
    框架建立在这些好的设计模式上 - Spring Ioc容器包含了
     <span class="emphasis">
      <em>
            工厂模式
      </em>
     </span>
     和
     <span class="emphasis">
      <em>
            观察者
      </em>
     </span>
     模式，它们最主要的特点是它们让依赖注入这一模式的使用变得更加容易。
    </p>
    <div class="sect2" lang="en">
     <div class="titlepage">
      <div>
       <div>
        <h3 class="title">
         <a name="core-concepts-spring-and-ioc-di">
         </a>
         依赖反转: 依赖注入的先驱
        </h3>
       </div>
      </div>
     </div>
     <p>
      第一个关于
      <span class="bold">
       <strong>
        依赖注入
       </strong>
      </span>
      的引用出现在1994年的一篇paper中，作者是Robert C. Martin，文章名是“依赖反转原理”。
     </p>
     <p>
      在 “依赖反转原理” (
      <span class="bold">
       <strong>
        DIP
       </strong>
      </span>
      ), 作者阐述了三种垃圾代码的决定性因素：
     </p>
     <div class="orderedlist">
      <ol type="1">
       <li>
        难以修改，因为任何的改动都可能影响到系统的其他部分，牵一发而动全身。（刚性）
        【译者云：这个刚性是Rigidity，就是表示这个代码太硬了，难以改变，如果是想橡皮泥那样，很软，就
        容易修改】
       </li>
       <li>
        当你对代码做出一些改变后，一些预料之外的系统崩溃了。（易碎性）【译者云：不敢乱碰，容易崩】
       </li>
       <li>
        代码很难在别的应用中得到重用，因为代码很难从原有项目中提取出来。（不可迁徙性）
        <sup>
         [
         <a href="#ftn.d0e237" name="d0e237">
          3
         </a>
         ]
        </sup>
       </li>
      </ol>
     </div>
     <p>
     </p>
     <p>
      根据Martin的理论，内部的相互依赖导致了代码的种种问题（我们之后将他们称作
      According to Martin, interdependency causes these coding problems (we'll call them
      <span class="bold">
       <strong>
            RFI
       </strong>
      </span>
      ）【译者云：
      R是硬度（Rigidity），F是易碎性（Fragility），I是不可迁移性（Immobility）。为了修复OO代码中的
      RFI问题，DIP（依赖反转原理）【译者云：Dependency Inversion Principle】又两个基本规则：
     </p>
     <p>
      <span class="emphasis">
       <em>
        1. 高层的模块不能从内部依赖于底层的模块，并且都应该依赖于抽象类。
        1. High level modules should not depend upon low level modules, both should depend upon abstractions.
       </em>
      </span>
     </p>
     <p>
    换句话说，高级的模块 - 那些包含了你的业务逻辑和所有重要组件的模块，不应该依赖于低级的模块。
    原因是如果你想修改这些低级模块，这些低级模块本身有可能会影响你的高级模块。这就是依赖反转的核心概念
    ，之前的关于“高层模块应该从内部依赖于底层模块”证实是一种糟糕的观点。
    【译者云：所谓“抽象类”是指只声明接口，不填充具体内容的一类东西，具体到Java中就是Interface和Abstract Class。所谓“高层模块”好比汽车，“低级模块”好比汽车轮胎，一眼看过去当然是“汽车”要依赖于“轮胎”了，但是
    这里所说的是一种“内部依赖”，在一会儿的例子中，你将理解什么是“内部依赖”】
     </p>
     <p>
      <span class="emphasis">
       <em>
        2. 抽象类不能依赖于具体的实现细节，而是实现细节依赖于抽象类。
       </em>
      </span>
     </p>
     <p>
     在你开始写抽象层时 - 接口或者抽象类 - 你应该找寻一些组件中的共同点再进行。你的接口/抽象类应该服务于
     你的业务逻辑于低级模块之间。你在这些抽象层中应该略去具体的实现细节。
     【译者云：再以汽车为例，汽车是高层模块，轮胎是底层模块，那么抽象层就是连接汽车与轮胎的一个层。打个比方，
     轮胎有“滚动”的方法，但是轮胎却有好多种规格，这每种规格的轮胎都是一种具体实现，而你需要一个抽象类或是接口，去
     声明这个“轮胎”，然后每种具体的轮胎实现，都继承这个“轮胎”接口，都有一个“滚动”的方法，这样当你更换底层模块的时候，
     比如你更换了轮胎的型号，你的汽车，高层模块不需要修改任何代码。】
     </p>
     <p>
    这个简单的投票箱的程序展示了一个不满足DIP原则的，也就是一段“垃圾代码”：
     </p>
     <div class="informalexample">
      <pre class="programlisting">
                    
package org.springbyexample.vote;

public class VotingBooth {

    VoteRecorder voteRecorder = new VoteRecorder();
    
    public void vote(Candidate candidate) {
        voteRecorder.record(candidate);
    }
    
    class VoteRecorder {
        Map hVotes = new HashMap();
        
        public void record(Candidate candidate) {
            int count = 0;
            
            if (!hVotes.containsKey(candidate)){
                hVotes.put(candidate, count);
            } else {
                count = hVotes.get(candidate);
            }
            
            count++; <a name="core-concepts-section-voting-booth-example01-count"></a><img alt="1" border="0" src="images/callouts/1.gif"/>
            
            hVotes.put(candidate, count);  <a name="core-concepts-section-voting-booth-example01-hVotes-put"></a><img alt="2" border="0" src="images/callouts/2.gif"/>
            
        }
    }

}
                    
                </pre>
      <div class="calloutlist">
       <table border="0" summary="Callout list">
        <tr>
         <td align="left" valign="top" width="5%">
          <a href="#core-concepts-section-voting-booth-example01-count">
           <img alt="1" border="0" src="images/callouts/1.gif"/>
          </a>
         </td>
         <td align="left" valign="top">
          <span class="emphasis">
           <em>
            票数
           </em>
          </span>
          加一
         </td>
        </tr>
        <tr>
         <td align="left" valign="top" width="5%">
          <a href="#core-concepts-section-voting-booth-example01-hVotes-put">
           <img alt="2" border="0" src="images/callouts/2.gif"/>
          </a>
         </td>
         <td align="left" valign="top">
          把投票者和票加到
          <span class="emphasis">
           <em>
            Map
           </em>
          </span>
          里.
         </td>
        </tr>
       </table>
      </div>
     </div>
     <p>
     在这个例子中
      <span class="emphasis">
       <em>
        投票箱（VotingBooth）
       </em>
      </span>
      从内部依赖于
      <span class="emphasis">
       <em>
        投票纪录器（VoteRecorder）
       </em>
      </span>
     违反了Rule1 , 
     VoteRecorder不是抽象类，而是具体实现，违反了Rule2。
     【译者云：我们看到VoteRecorder是在VoteBooth的内部，这就是内部依赖，耦合度高】
     </p>
     <p>
    依赖反转后的代码版本看起来稍有不同。首先，我们先定义：
      <code class="code">
       VoteRecorder
      </code>
      的接口
     </p>
     <p>
     </p>
     <pre class="programlisting">
                    
package org.springbyexample.vote;

public interface VoteRecorder {

    public void record(Candidate candidate) ;

}
                    
                </pre>
     <p>
     </p>
     <p>
     然后我们的具体实现：
     </p>
     <p>
      <code class="code">
       LocalVoteRecorder
      </code>
      ，它是
      <code class="code">
       VoteRecorder
      </code>
     接口的具体实现：
     </p>
     <p>
     </p>
     <pre class="programlisting">
                    
package org.springbyexample.vote;

public class LocalVoteRecorder implements VoteRecorder {

    Map hVotes = new HashMap();
    
    public void record(Candidate candidate) {
        int count = 0;
        
        if (!hVotes.containsKey(candidate)){
            hVotes.put(candidate, count);
        } else {
            count = hVotes.get(candidate);
        }
        
        count++;
        
        hVotes.put(candidate, count);
    }
    
}
                    
                </pre>
     <p>
     </p>
     <p>
      还有
      <code class="code">
       VotingBooth
      </code>
      类：
     </p>
     <p>
     </p>
     <pre class="programlisting">
                    
package org.springbyexample.vote;

public class VotingBooth {

    VoteRecorder recorder = null;
    
    public void setVoteRecorder(VoteRecorder recorder) {
        this.recorder = recorder;
    }
    
    public void vote(Candidate candidate) {
        recorder.record(candidate);
    }

}
                    
                </pre>
     <p>
     </p>
     <p>
      至此，
      <code class="code">
       LocalVoteRecorder
      </code>
      类 – 
      <code class="code">
       VoteRecorder
      </code>
      接口的具体实现 -- 完全的从
      <code class="code">
       VotingBooth
      </code>
      中解耦。
      【译者云：现在遵循了DIP的两个原则了。】
      我们移走了所有高层模块对底层模块的内部引用。
     </p>
     <p>
    然而，这个代码的实现仍然有个问题。我们没有一个main方法（java中的入口函数）。原则上为了让我们的代码跑起来，
    我们需要一个main方法，并且我们必须要对
      <code class="code">
       LocalVoteRecorder
      </code>
      .
     </p>
     <p>
        进行实例化。主方法中的
      <code class="code">
       LocalVoteRecorder
      </code>
      使得我们不得不破坏DIP的Rule#1。
      我们增加了抽象层，修改了代码，但我们的应用仍然依赖于底层的模块。
      【译者云：DIP的两条规则十分严格，因为你的main方法是在VotingBooth里，main方法里如果创建了
      VotingRecorder的实例，那么这又构成了一种“内部引用”，范围了依赖反转的原则一。】
     </p>
    </div>
   </div>
   <div class="footnotes">
    <br/>
    <hr align="left" width="100"/>
    <div class="footnote">
     <p>
      <sup>
       [
       <a href="#d0e171" name="ftn.d0e171">
        1
       </a>
       ]
      </sup>
      A 1950's horror film featuring the big screen debut of Steve McQueen. 
				The film stars an ever-growing, all-consuming amoeba-like monster that terrorizes a small Pennsylvania  town.
     </p>
    </div>
    <div class="footnote">
     <p>
      <sup>
       [
       <a href="#d0e190" name="ftn.d0e190">
        2
       </a>
       ]
      </sup>
      Pree, W. (1994)
      <em class="citetitle">
       Meta Patterns
      </em>
      – a means for capturing the essentials of
					reusable object-oriented design.
					Springer-Verglag, proceedings of the ECOOP,
					Bologna, Italy: 150-162
     </p>
    </div>
    <div class="footnote">
     <p>
      <sup>
       [
       <a href="#d0e237" name="ftn.d0e237">
        3
       </a>
       ]
      </sup>
      <em class="citetitle">
       The Dependency Inversion Principle
      </em>
      , Martin, Robert C., .c 1994
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
      <a accesskey="p" href="part-intro.html">
       Prev
      </a>
     </td>
     <td align="center" width="20%">
      <a accesskey="u" href="part-intro.html">
       Up
      </a>
     </td>
     <td align="right" width="40%">
      <a accesskey="n" href="core-concepts-dependency-injection-to-the-rescue.html">
       Next
      </a>
     </td>
    </tr>
    <tr>
     <td align="left" valign="top" width="40%">
      Part I. Spring Introduction
     </td>
     <td align="center" width="20%">
      <a accesskey="h" href="index.html">
       Home
      </a>
     </td>
     <td align="right" valign="top" width="40%">
      2. Dependency Injection To The Rescue
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