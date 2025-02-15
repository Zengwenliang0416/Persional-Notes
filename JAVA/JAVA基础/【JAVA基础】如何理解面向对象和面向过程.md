**面向过程**把问题分解成一个一个步骤，每个步骤用函数实现，依次调用即可。

我们在进行面向过程编程的时候，不需要考虑那么多，上来先定义一个函数，然后使用各种诸如if-else、for-each等方式进行代码执行。最典型的用法就是实现一个简单的算法，比如实现冒泡排序。 

**面向对象**将问题分解成一个一个步骤，对每个步骤进行相应的抽象，形成对象，通过不同对象之间的调用，组合解决问题。

就是说，在进行面向对象进行编程的时候，要把属性、行为等封装成对象，然后基于这些对象及对象的能力进行业务逻辑的实现。比如想要造一辆车，上来要先把车的各种属性定义出来，然后抽象成一个Car类。

面向对象有封装、继承、多态三大基本特征，和单一职责原则、开放封闭原则、里氏替换原则、依赖倒置原则和接口隔离原则等五大基本原则。



# 知识扩展

## 目录

[1. 目录](#目录)

[2. 面向对象的三大基本特征?](#面向对象的三大基本特征)

- [2.1 封装](#封装)

- [2.2 继承](#继承)

- [2.3 多态](#多态)

[3. 继承和实现](#继承和实现)

- [3.1 为什么Java不支持多继承？](#为什么java不支持多继承)

[4. 面向对象的五大基本原则？](#面向对象的五大基本原则)

- - [- 单一职责原则：一个类最好只做一件事](#单一职责原则一个类最好只做一件事)

- - [- 开放封闭原则：对扩展开放、对修改封闭](#开放封闭原则对扩展开放对修改封闭)

- - [- 里氏替换原则：子类必须能够替换其基类](#里氏替换原则子类必须能够替换其基类)

- - [- 依赖倒置原则：程序要依赖于抽象接口，而不是具体的实现](#依赖倒置原则程序要依赖于抽象接口而不是具体的实现)

- - [- 接口隔离原则：使用多个小的专门的接口，而不要使用一个大的总接口](#接口隔离原则使用多个小的专门的接口而不要使用一个大的总接口)



## 面向对象的三大基本特征?

三大基本特征：封装、继承、多态。

### 封装

封装就是把现实世界中的客观事物抽象成一个Java类，然后在类中存放属性和方法。如封装一个`汽车`类，其中包含了`发动机`、`轮胎` 、`底盘`等属性，并且有`启动`、`前进`等方法。

### 继承

像现实世界中儿子可以继承父亲的财产、样貌、行为等一样，编程世界中也有继承，继承的主要目的就是为了复用。子类可以继承父类，这样就可以把父类的属性和方法继承过来。

如Dog类可以继承Animal类，继承过来`嘴巴`、`颜色`等属性， `吃东西`、`奔跑`等行为。



### 多态

多态是指在父类中定义的方法被子类继承之后，可以通过重写，使得父类和子类具有不同的实现，这使得同一个方法在父类及其各个子类中具有不同含义。

## 继承和实现

在Java中，接口可以继承接口，抽象类可以实现接口，抽象类也可以继承具体类。普通类可以实现接口，普通类也可以继承抽象类和普通类。

Java支持多实现，但是只支持单继承。即一个类可以实现多个接口，但是不能继承多个类。



### 为什么Java不支持多继承？





## 面向对象的五大基本原则？ 

五大基本原则：单一职责原则（Single-Responsibility Principle）、开放封闭原则（Open-Closed principle）、Liskov替换原则（Liskov-Substituion Principle）、依赖倒置原则（Dependency-Inversion Principle）和 接口隔离原则（Interface-Segregation Principle）。

#### 单一职责原则：一个类最好只做一件事

#### 开放封闭原则：对扩展开放、对修改封闭

#### 里氏替换原则：子类必须能够替换其基类

#### 依赖倒置原则：程序要依赖于抽象接口，而不是具体的实现

#### 接口隔离原则：使用多个小的专门的接口，而不要使用一个大的总接口