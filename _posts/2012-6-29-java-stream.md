---
layout: page
title: Stream API详解
categories: [java]
---
>熟悉Java的你一定经常见到`Stream`这个东西, 可是我发现有些同学并不是很清楚它到底是干嘛的, 看完这篇文章, 你将理解Stream究竟是干嘛的.

`Stream`翻译成中文是类似于水流的东西, 但是这样翻译其实有一些问题, 事实上它的功能和水流也扯不上什么关系。

先提需求, 再讲技术.

假如我现在有一个`List` :

`List<Integer> numbers = Arrays.asList(2, 3, 4, 5);`

>我们现在要得到一个新的List, 它的每一项都是number 的平方, 你要怎么做? 这样? 创建一个新的List, 然后写一个循环, 让其每一项都等于`numbers`对应项的平方?

再看我们有这样一个`List`:

`List<String> names = Arrays.asList("Refection", "Collection", "Stream", "Spring")`

>`List`的每一项都是一个字符串, 如果我们要得到一个新的数组, 每个元素在names里面, 但是必须是以"S"打头的, 也就是我们要得到:`[Stream, Spring]`

>再看刚才的例子, 如果我们要得到一个新的`List`, `List`里面每个元素都是`names`内部元素按照字母顺序排序得来的, 你会怎么做?

刚才这些需求都是对一个`Collection`, 也就是一个集合的每个元素进行统一操作, 而`Stream`API让我们可以轻易做到这一点, 它是Java 8中引入的.

对于需求一, 我们只需要这样做:

```
List<Integer> square = numbers.stream().map(x -> x*x).collect(Collectors.toList());
```
`.stream()`是将`List`转换成`Stream`, 你可以把`List`理解成固态的, 不可改变的, 而`Stream`则是水流, 可以任意洗牌重组.

`.map(x -> x*x)`是将原有集合中的每一个元素通过`x -> x*x`这个函数映射到新的集合中, 也就是该方法的返回值中. `x -> x*x`是`lambda`表达式, 它代表了一个函数, 其实就类似于数学中的`y=f(x)=x*x`, 如果原有的`List`是`[1, 2, 3]`, 那映射之后的`List`就是`[1, 4, 9]`, 很好理解.

后面的`.collect(...)`一会儿再说.

对于需求二, 我们直接这样:

```
List<String> startWithS = names.stream().filter(s -> s.startsWith("S")).collect(Collectors.toList());
```
`.filter(s -> s.startsWith("S"))`类似于`.map()`, 故名思意, 这是个"筛子", 将不满足条件的筛选掉, 而内部的匿名函数`s -> s.startsWith("S")`就是这个筛子, 返回`true`, 即满足条件, 返回`false`, 即不满足. `.startsWith`返回一个`Boolean`
, 用于检测字符串的开头字母.

>对于这类返回一个`Boolean`变量的匿名函数, Java中称其为`Predicate`.

需求三, 我们直接:
```
List<String> sortedNames = names.stream().sorted().collect(Collectors.toList());
```
`.sorted()`便是对原有集合排序, 返回排序后的集合.

那么对于刚才讲的这三个方法:

`.map()`、`.filter()`、`.sorted()`我们称为`Intermidate Operation`, 也就是中间操作.

那么后面的`.collect()`方法就是把被中间操作改变后的数组(此时还处于`Stream`状态), 变成正常的`List`, 那么这样的方法我们称为`Terminal Operation`, 也就是最终操作, 它的用途就是把处于"流体"状态的集合转变为正常的可直接使用的集合.

`Terminal Operation`有三种:

1. `.collect()`: 将`Stream`状态的数据结构转变为正常的数据结构, 比如`List`, `Set`, 如果你想让其返回一个`Set`, 就传入一个`Collectors.toSet()`参数即可, 别的同理.
2. `.forEach()`: 和你们经常见到的`for-each`语句是一个道理, 就是对于集合内的每个元素, 依次进行某个操作, 该函数需要传入一个匿名函数, 作为这个操作本身, 比如:
```
List number = Arrays.asList(2, 3, 4, 5);
number.stream().map(x -> x*x).forEach(y -> System.out.println(y));
```
该操作会打印出4, 8, 16, 25.
3. `.reduce()`: 该方法会将原有的集合通过某种方式"累加"到一个变量中去, 它接收两个参数, 第一个是初始值, 也就是`initial value`, 第二个是一个有两个变量的匿名函数, 匿名函数的左变量是累积的变量, 右变量是当前元素的值, 比如:
```
List number = Arrays.asList(2, 3, 4, 5);
int total = number.stream().reduce(0, (accu, i) -> accu+i);
```
匿名函数`(accu, i) -> accu+i`会对每一个元素进行操作, `accu`的值是上一次函数的返回值, 也就是累加结果.

accu = 0 i = 2 返回 2

accu = 2 i = 3 返回 5

accu = 5 i = 4 返回 9

...

最终`total`会等于集合内的所有元素之和, 也就是14.

可以写一段代码演示今天的知识点:

```
//a simple program to demonstrate the use of stream in java 
import java.util.*; 
import java.util.stream.*; 
  
class Demo 
{ 
  public static void main(String args[]) 
  { 
  
    // create a list of integers 
    List<Integer> number = Arrays.asList(2,3,4,5); 
  
    // demonstration of map method 
    List<Integer> square = number.stream().map(x -> x*x). 
                           collect(Collectors.toList()); 
    System.out.println(square); 
  
    // create a list of String 
    List<String> names = 
                Arrays.asList("Reflection","Collection","Stream"); 
  
    // demonstration of filter method 
    List<String> result = names.stream().filter(s->s.startsWith("S")). 
                          collect(Collectors.toList()); 
    System.out.println(result); 
  
    // demonstration of sorted method 
    List<String> show = 
            names.stream().sorted().collect(Collectors.toList()); 
    System.out.println(show); 
  
    // create a list of integers 
    List<Integer> numbers = Arrays.asList(2,3,4,5,2); 
  
    // collect method returns a set 
    Set<Integer> squareSet = 
         numbers.stream().map(x->x*x).collect(Collectors.toSet()); 
    System.out.println(squareSet); 
  
    // demonstration of forEach method 
    number.stream().map(x->x*x).forEach(y->System.out.println(y)); 
  
    // demonstration of reduce method 
    int even = 
       number.stream().filter(x->x%2==0).reduce(0,(ans,i)-> ans+i); 
  
    System.out.println(even); 
  } 
} 
```
输出:
```
[4, 9, 16, 25]
[Stream]
[Collection, Reflection, Stream]
[16, 4, 9, 25]
4
9
16
25
6
```
希望大家有所收获.




