---
layout: post
title:  设计模式
categories: java
tags:  设计模式
author: kongkongye
---

* content
{:toc}

设计模式(Design Pattern)代表了**最佳实践**,通常适合**面向对象**开发时使用.
1994年出版的一本书中提到了面向对象设计原则: 对接口编程而不是对实现编程;优先使用对象组合而不是继承.




## 介绍
设计模式之间的关系:

![](/imgs/2018-03-23-design-patterns/relation.jpg)

## 六大原则
1. `开闭原则(Open Close Principle)`: 对扩展开放,对修改关闭.
2. `里氏代换原则(Liskov Substitution Principle)`: 任何基类可以出现的地方,子类一定可以出现.这是对开闭原则的补充.
3. `依赖倒转原则(Dependence Inversion Principle)`: 针对接口编程,依赖于接口而不依赖于具体实现.这是开闭原则的基础.(高层模块不依赖于低层模块,而是低层模块依赖于高层模块的抽象,这就是'反转')
4. `接口隔离原则(Interface Seregation Principle)`: 使用多个隔离的接口比使用单个的接口好,降低类之间的耦合度.
5. `迪米特法则/最少知道原则(Demeter Principle)`: 一个实体应该尽量少与其它实体发生相互作用,使功能模块相对独立.
6. `合成复用原则(Composite Reuse Principle)`: 尽量使用合成/聚合的方式,而不是继承.

## 类型
### 创建型(Creational Patterns)
* 工厂模式
* 抽象工厂模式
* 单例模式
* 建造者模式
* 原型模式(此文未做介绍)

### 结构型(Structural Patterns)
* 适配器模式
* 桥接模式
* 过滤器模式(此文未做介绍)
* 组合模式(此文未做介绍)
* 装饰器模式
* 外观模式
* 享元模式
* 代理模式

### 行为型(Behavioral Patterns)
* 责任链模式(此文未做介绍)
* 命令模式
* 解释器模式(此文未做介绍)
* 迭代器模式(此文未做介绍)
* 中介者模式
* 备忘录模式(此文未做介绍)
* 观察者模式
* 状态模式(此文未做介绍)
* 空对象模式(此文未做介绍)
* 策略模式(此文未做介绍)
* 模板模式(此文未做介绍)
* 访问者模式(此文未做介绍)

## 设计模式
### 工厂模式(Factory Pattern)
![](/imgs/2018-03-23-design-patterns/工厂模式.png)

#### 优点
1. 屏蔽实现,调用者只需要知道接口
2. 扩展性强,增加一种子类简单

#### 缺点
每增加一种产品都要增加一个具体的子类实现,并且修改工厂方法

#### 使用场景
1. 日志记录器,可以记录在本地硬盘,远程服务器等,用户可以选择记录在哪
2. 数据库访问,可以切换使用的数据库(像hibernate)
3. 设计一个连接服务器的框架,可以使用多个不同的协议

### 抽象工厂模式(Abstract Factory Pattern)
![](/imgs/2018-03-23-design-patterns/抽象工厂模式.png)

#### 概念
1. `产品等级`: 即产品的继承
2. `产品族`: 由同一个工厂生产的,不同产品等级的一组产品.

#### 优点
1. 可以保证始终使用同一个产品族的产品
2. 产品等级扩展简单

#### 缺点
产品族扩展困难

### 单例模式(Singleton Pattern)
![](/imgs/2018-03-23-design-patterns/单例模式.png)

只能有一个实例,并且由单例类自己创建

#### 优点
1. 只有一个实例,减小内存开销
2. 避免对资源的多重占用

#### 缺点
没有接口,不能继承

#### 实现
1. `懒汉式,线程不安全`: 效率高,但线程不安全.
2. `懒汉式,线程安全`: 效率较低.
3. `饿汉式`: 线程安全.类加载时就初始化,比较浪费内存.
4. `双检锁/双重校验锁`: 效率高,线程安全.
5. `登记式/静态内部类`: 效率高,线程安全.利用classloader加载机制保证初始化instance时只有一个线程.
6. `枚举`: 简单,线程安全.

### 建造者模式(Builder Pattern)
![](/imgs/2018-03-23-design-patterns/建造者模式.png)

如`StringBuilder`/`StringBuffer`

#### 概念
1. Builder: (抽象)建造者
2. ConcreteBuilder: 具体建造者(有时可以省略)
3. Director: 指挥者(有时可以省略)
4. Product: 产品

#### 优点
1. 解耦产品与创建过程
2. 易扩展
3. 便于控制细节

#### 缺点
1. 产品必须有共同点,范围有限制
2. 如内部复杂,会有很多的具体建造者

### 适配器模式(Adapter Pattern)
![](/imgs/2018-03-23-design-patterns/适配器模式.png)

作为两个不兼容的接口间的桥梁,通常用来将旧的,已经在运行中的系统兼容新的系统接口.

可分为`类适配器`(直接继承)与`对象适配器`(传入适配者对象)两种类型.

#### 概念
1. Target：目标抽象类
2. Adapter：适配器类
3. Adaptee：适配者类

就是对`适配者`进行适配,当作`目标抽象类`来用.

#### 优点
1. 让两个不兼容的类一起运行
2. 提高了类的复用
3. 灵活性好

#### 缺点
1. 过多使用会导致零乱(可以考虑重构)
2. 类适配器的目标只能是接口而不能是类,限制大

### 桥接模式(Bridge Pattern)
![](/imgs/2018-03-23-design-patterns/桥接模式.png)

用于把`抽象`与`实现`解耦.

简单的说,原来是实现直接继承抽象接口,现在解耦了,抽象与实现都可以各自按自己风格心情写代码,写好后,写个`桥`(继承抽象类,传入实现)来将它们连接在一起.

#### 概念
1. Abstraction: 抽象类
2. Bridge: 桥
3. Implementor: 实现类

#### 优点
1. 抽象与实现分离
2. 优秀的扩展能力
3. 对客户透明,隐藏细节

#### 缺点
1. 增加系统的理解与设计难度
2. 要求正确识别两个独立变化的维度,使用范围有局限

### 装饰器模式(Decorator Pattern)
![](/imgs/2018-03-23-design-patterns/装饰器模式.png)

允许向一个现有的对象添加新功能,但不改变其结构,如java内的`xxxStream`那些类.

#### 优点
1. 比继承更灵活,更动态

#### 缺点
1. 多层装饰比较复杂

### 外观模式(Facade Pattern)
![](/imgs/2018-03-23-design-patterns/外观模式.png)

一般将外观类设计为单例,并且注意不要通过外观类为子系统增加新行为,而应该直接修改子系统.

#### 优点
1. 对客户屏蔽子系统组件,更容易使用
2. 实现子系统与客户之间的松耦合

#### 缺点
1. 灵活性降低

### 享元模式(Flyweight Pattern)
1. 需要分离外部状态与内部状态,外部状态可以由外部设置
2. 它们相对独立,不互相影响
3. 外部状态应该具有固化的性质
4. 享元对象存储在Map中,用唯一标识码判断

#### 优点
1. 减少内存使用
2. 外部状态相对独立,不会影响内部状态,使享元对象可以在不同环境中被共享

#### 缺点
1. 使系统更复杂,需要分离外部状态与内部状态

### 代理模式(Proxy Pattern)
![](/imgs/2018-03-23-design-patterns/代理模式.png)

起到中介与控制的作用.
与适配器模式不同的是,它不改变接口.
与装饰器模式不同的是,它主要为了控制,而装饰主要为了增加功能.

#### 优点
1. 职责清晰
2. 高扩展性

#### 缺点
1. 实现代理需要额外的工作

### 命令模式(Command Pattern)
![](/imgs/2018-03-23-design-patterns/命令模式.png)

将请求与执行解耦

#### 概念
1. 调用者: 里面可以保存调用者的一些信息,如调用的命令历史
2. 命令: 具体的命令
3. 执行者: 实际执行操作的

#### 优点
1. 降低了系统耦合度
2. 添加新命令容易

#### 缺点
1. 会使系统有过多的具体命令类

### 中介者模式(Mediator Pattern)
![](/imgs/2018-03-23-design-patterns/中介者模式.png)

将类之间的网状结构变为星状结构

与外观模式的区别: 外观模式主要是外部单向调用内部;中介者模式主要是内部之间互相调用.

#### 优点
1. 降低类的复杂度,将一对多转化为一对一

#### 缺点
1. 中介者会很庞大

### 观察者模式(Observer Pattern)
![](/imgs/2018-03-23-design-patterns/观察者模式.png)

#### 优点
1. 观察者与被观察对象是抽象耦合的
2. 建立了一套触发机制,支持广播通信

#### 缺点
1. 如果观察目标有很多直接与间接的观察者,通知会花费大量时间
2. 如果观察者与观察目标之间有循环依赖,容易导致死循环
3. 只能让观察者知道观察目标发生了变化,而没法知道是怎么发生变化的(只知道结果,不知道过程)
