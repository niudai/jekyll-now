---
layout: page
title: 设计模式 - 工厂模式(Factory Pattern)
categories: [design]
---
在面向对象语言中, 我们要创造一个实例, 往往要这样:

```
Instance instance = new Instance();
```

这是很明显的, 但是在实际的操作中, 实例的创建并非如此容易, 我们拿现实世界来举例。

试想一个汽车生产线，一个汽车的生产，能够简单的一句：

```
Car car = new Car（）;
```

就搞定了吗？

显然不是，我们需要很多信息来决定我们生产的汽车是哪种汽车。

假如我们现在能够生产四种汽车，分别是Benz，BMW，Lexus，Honda，这四种汽车本身作为汽车，肯定是继承了Car类的。比如：

```
Class Benz extends Car {
      ....
}
```
Car类包含了汽车所具备的基本功能，比如：

drive（）方法等，而Benz则在Car的基础上增加了更具体的内容，比如车前面的奔驰标志，更豪华的内饰等等。

当生产需求下达前，你并不知道你要创造哪种汽车，我们必须根据客户的需求来创造特定的汽车，那你肯定觉得很简单，只要这样做就行：

```
  String demands = 用户需求输入
  if （demands == “Benz”） {
    Car benz = new Benz（）；
  } else if （demands == “BMW”） {
    Car bwm = new BMW（）；
  } ...
```

这样写其实没什么问题，但是我们希望把这段代码封装起来，变成一个“工厂”，这个“工厂”作为一个单独的类，它有“生产"方法，而且需要传入用户需求。

我们这样：

```
  Class CarFactory {
    public create(String carType) {
      if （carType == “Benz”） {
        return new Benz()；
      } else if （carType == “BMW”） {
        return new BMW()；
      } else if (carType == "Lexus") {
        return new Lexus();
      } else if (carType == "Honda") {
        return new Honda();
      } else {
        return null;
      }
    }
  }
```

上面的代码很好理解，所以为了制造汽车，我们只需：

```
  CarFactory carFactory = new CarFactory();
  String demands = 用户需求输入
  Car car = carFactory.create(demands);
```

注意上方的三行代码是用户侧（Client-side），也就是说，这个汽车工厂人家已经给你造好了，身为用户的你直接创造一个汽车工厂实例，直接拿过来用就好，这样看来是不是比刚才未封装的方式好用的多（对于用户侧来讲）。三行代码便按照用户的需求创造了一个汽车，但是却没有出现任何”new“的字眼，非常舒服。

那把问题搞得再复杂一些，其实工厂里面也可以有子工厂哦。

比如现在用户的需求不是简单的一个汽车品牌了，而是一台私人定制汽车，用户的需求包含了一个详细的内饰配置清单，还有轮胎的配置清单。

这两个清单其实就是两个实例，我们这样去写：

```
  InteriorConf interiorConf = 用户传入的内饰配置
  WheelConf wheelConf = 用户传入的轮胎配置
```

那么原先的工厂就显得太鸡肋了，无法完成定制级别的汽车制造，那么我们可以做两个子工厂，分别是内饰工厂和轮胎工厂:

```
  Class InteriorFactory {
    public create(InteriorConf interiorConf) {
      ...
      // 根据配置文件，返回特定的内饰
      return interior；
    }
  }
  Class WheelFactory {
    public create(WheelConf wheelConf) {
    // 根据配置文件，返回特定型号和配置的轮胎
    return wheel；
  }
```

然后既然是子工厂，那么它们应该被添加到我们的总工厂：CarFactory中：

```
  Class CarFactory {
    InteriorFactory interiorFactory = new InteriorFactory(); // 内饰子工厂
    WheelFactory wheelFactory = new WheelFactory(); // 轮胎子工厂
    public create(InteriorConf interiorConf, WheelFactory wheelConf) {
      Wheel wheel = wheelFactory(factoryConf); // 用轮胎子工厂做出轮胎
      Interior interior = interiorFactory(interiorConf); // 用内饰子工厂做出内饰
      ...
      return specifiedCar // 返回具体的定制车型
    }
    public create(String carType) {
      if （carType == “Benz”） {
        return new Benz()；
      } else if （carType == “BMW”） {
        return new BMW()；
      } else if (carType == "Lexus") {
        return new Lexus();
      } else if (carType == "Honda") {
        return new Honda();
      } else {
        return null;
      }
    }
  }
```

所以当你想像一个产品线那样，根据特定需求创建出特定实例时，就使用工厂模式，避免new的使用，把工厂封装好，思路清晰，便于使用。