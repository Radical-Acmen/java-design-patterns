---
layout: pattern
title: Adapter
folder: adapter
permalink: /patterns/adapter/
categories: Structural
tags:
 - Java
 - Gang Of Four
 - Difficulty-Beginner
---

![image](03_adapter.png)

## 也被称为
包装纸

## 意图
将类的接口转换为客户端的另一个接口
期望。适配器让班级一起工作，否则不能因为
不兼容的接口。

## 说明

真实世界的例子

>请考虑您的存储卡中有一些照片，并且需要将它们传输到您的计算机上。为了传输它们，您需要一些与计算机端口兼容的适配器，以便您可以将存储卡连接到计算机。在这种情况下，读卡器是一个适配器。
>另一个例子是着名的电源适配器;一个三脚插头不能连接到双叉插座上，需要使用一个电源适配器，使其与双叉插座兼容。
>又一个例子是翻译者将一个人所说的话翻译成另一个人

用简单的话来说

>适配器模式可让您将适配器中另外的不兼容对象包装在一起，以使其与另一个类兼容。

维基百科说

>在软件工程中，适配器模式是一种软件设计模式，它允许将现有类的接口用作另一个接口。它通常用于使现有类与其他类一起工作而不修改其源代码。

**编程示例**

考虑一个只能使用划艇的船长，根本不能航行。

首先我们有界面`RowingBoat`和`FishingBoat`

```java
public interface RowingBoat {
  void row();
}

public class FishingBoat {
  private static final Logger LOGGER = LoggerFactory.getLogger(FishingBoat.class);
  public void sail() {
    LOGGER.info("The fishing boat is sailing");
  }
}
```

And captain expects an implementation of `RowingBoat` interface to be able to move

```java
public class Captain implements RowingBoat {

  private RowingBoat rowingBoat;

  public Captain(RowingBoat rowingBoat) {
    this.rowingBoat = rowingBoat;
  }

  @Override
  public void row() {
    rowingBoat.row();
  }
}
```

现在让我们说，海盗来了，我们的船长需要逃跑，但只有渔船可用。 我们需要创建一个适配器，允许船长用他的划船技能来操作渔船。

```java
public class FishingBoatAdapter implements RowingBoat {

  private static final Logger LOGGER = LoggerFactory.getLogger(FishingBoatAdapter.class);

  private FishingBoat boat;

  public FishingBoatAdapter() {
    boat = new FishingBoat();
  }

  @Override
  public void row() {
    boat.sail();
  }
}
```

现在“船长”可以用“渔船”逃出海盗。

```java
Captain captain = new Captain(new FishingBoatAdapter());
captain.row();
```

## 适用性
使用适配器模式时

* 你想使用一个现有的类，它的接口不符合你所需要的
* 你想创建一个可重用的类，与不相关或不可预见的类进行合作，也就是说，不需要兼容接口的类
* 您需要使用几个现有的子类，但是通过继承每个子类来调整它们的接口是不切实际的。对象适配器可以调整其父类的接口。
* 大多数使用第三方库的应用程序使用适配器作为应用程序和第三方库之间的中间层，以将应用程序与库分离。如果必须使用另一个库，则只需要用于新库的适配器而不必更改应用程序代码。

## 后果：
类和对象适配器有不同的权衡。类适配器

* 通过承诺一个具体的适应类来适应目标。因此，当我们想调整一个类及其所有子类时，类适配器将不起作用。
* 让我们的Adapter重写一些Adaptee的行为，因为Adapter是Adaptee的一个子类。
* 只引入一个对象，并且不需要额外的指针间接寻找适配器。

一个对象适配器

让我们一个适配器与许多适配器一起工作 - 即适配器本身及其所有子类（如果有的话）。适配器也可以一次为所有的适配器添加功能。
* 使覆盖`Adaptee`行为变得更加困难。这将需要子类`Adaptee`和使适配器指的是子类而不是适配器本身。


## 示例

* [java.util.Arrays#asList()](http://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#asList%28T...%29)
* [java.util.Collections#list()](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#list-java.util.Enumeration-)
* [java.util.Collections#enumeration()](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#enumeration-java.util.Collection-)
* [javax.xml.bind.annotation.adapters.XMLAdapter](http://docs.oracle.com/javase/8/docs/api/javax/xml/bind/annotation/adapters/XmlAdapter.html#marshal-BoundType-)


## 参考

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [J2EE Design Patterns](http://www.amazon.com/J2EE-Design-Patterns-William-Crawford/dp/0596004273/ref=sr_1_2)
