---
layout: post
title:  "接口"
date:   2019-08-02 21:23:00 +0800
tags: Java
---

# 接口的概述
- 提供方法的规则，用以让其他的类去实现
- 比抽象类还要抽象，接口中只有常量和抽象方法

---
# 接口的成员特点
- 成员变量
    - 只能是常量
    - 只能用**public static final**修饰
        - 由于是接口，无法被实例化，如果其变量要有意义，必须要有足够大的权限(**public**)
        - 由于接口没有方法体，所有如果有变量则必须是常量(**final**)
        - 要使接口中的常量能被其他类的方法直接调用，则必须要加静态修饰符(**static**)
- 成员方法
    - 只能用**public abstract**修饰
        - 从接口的定义来看，其内部的方法必须是抽象方法(**abstract**)，如果不加修饰符则默认为**abstract**
        - 接口的意义在于要让其他的类来实现其内部的方法，因此其内部方法的权限需要足够大以让其他类去接收(**public**)
        - 不支持除**public abstract**以外的修饰符

---
# 接口和类之间的各种关系
- 接口和接口
    - 继承关系  **extends**
    - 多重继承&多层继承
- 接口和类
    - 实现关系  **implement**
    - 一个类如果要实现一个接口，则必须要重写其中所有的抽象方法
    - 一个类可以实现多个接口
- 类和类
    - 继承关系  **extends**
    - 单一继承&多层继承

---
# 接口的思想
- 如果说类是用来描述事物，以事物的属性标准来划分事物的，那么接口就可以看做是从行为属性上划分事物的特殊类
- 提供了方法的规则(行为标准)

---
# 接口的优点
- 直接打破了类单一继承的局限
- 给其他的类以及接口提供了行为标准
- 降低了程序的耦合性，从而可以实现模块化开发

---
# 接口与抽象类的区别
- 成员的区别
    - 抽象类中成员变量可以是变量也可以是常量而接口中的成员变量只能是常量
    - 抽象类中可以有非抽象方法，而接口中的方法必须全部都是抽象方法
- 继承关系的区别
    - 抽象类是类，类只能单一继承
    - 接口可以多重继承

---
# 多态的概述和实现
- 父类引用指向子类对象
```java
    Animal a = new Cat();           //Cat是Animal的一个子类
```

---
# 多态成员的特点
- 除了方法引用的是子类中重写过的(如果子类重写过)，其余的一律引用的是父类的成员

---
# 多态中的向上转型和向下转型
- 当子类对象赋值给一个父类引用时，即为向上转型，多态本身就是一个向上转型的过程
- 对于一个使用了向上转型的**子类对象**，可以使用强制类型转换的格式使其转为子类引用，这个过程是向下转型
- 无论是向上转型还是向下转型，都是**子类对象**在其中进行变换
- 如果父类引用指向的是父类对象，是无法进行向下转型的
- 关键字**instanceof**
    - 用于判断一个引用是否为某个对象
```java
    Animal a = new Cat();
    System.out.println(a instanceof Cat);       //输出true
```

---
# 多态的优缺点
- 优点
    - 提高了代码的可维护性(本质是由继承所带来的)
- 缺点
    - 无法直接访问子类的成员

---
