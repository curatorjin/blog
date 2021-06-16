---
layout: post
title:  "Java反射机制"
date:   2018-8-27 19:01:50 +0800
categories: standard
---
# 反射的概念
- 一种**动态获取信息和调用对象方法**的机制
- 反射是Java中非常重要的一个机制。在运行状态中，对于任意一个类，通过反射机制都能够获得这个类的所有的属性和方法；对于任意一个对象，通过反射机制都能调用他的任意一个方法和属性。

### 反射机制的意义
- 利用反射机制，我们可以**大大增强程序的灵活性**
- 从编程过程中来看，如果说编码是一个程序员向机器输入的过程，那么运用反射机制就相当于是向机器获取的过程。反射的实质是在获取字节码文件中的相关信息。因此，从一定程度上来说，反射机制补全了对于程序流程的控制。
> 目前几乎所有框架的底层实现都利用到了反射机制

---
# 反射机制的概述和字节码对象的获取方式
- 通过对象的getClass方法来获取
    ```java
    Student s = new Student();
    Class c = s.getClass();             //需要有一个该类的对象
    ```
- 通过类名调用class()方法来获取
    ```java
    Class c = Student.getClass();       //需要知道该类的类名
    ```
- 通过Class类的forName静态方法来获取
    ```java
    Class c = Class.forName("全类名");  //只需要知道该类的全类名即可
    ```

---
# 通过反射获取构造方法并使用
- 当获取某一个类的字节码对象之后，即可通过反射获取其构造方法,方法如下
```java
Constructor[] getConstructors();       //获取该类的所有非私有的构造方法，返回Constructor数组
Constructor<?> getConstructor();       //获取该类的非私有构造方法，返回一个Constructor对象
```
- 获取了构造方法之后，可使用Constructor对象的newInstance来创建该类的对象
```java
Object newInstance();         //利用Constructor对象创建新对象
```

---
# 通过反射获取成员变量并使用
- 利用Class对象的getFields()方法来获取成员变量的地址，此方法返回的是一个Field对象
    ```java
    Field[] getFields();                            //获取对象的所有公有成员变量
    Field[] getDeclaredFields();                    //获取对象的所有成员变量
    Field getField(String fieldName);               //获取变量名为fieldName的非私有成员变量
    Field getDeclaredField(String fieldName);       //获取变量名为fieldName的成员变量
    ```
    - 此处注意，Field对象接收到的，只是对应的字段在目标对象中的存储地址，并非获取到了对象字段的具体值
- 获取指定对象的具体成员变量的值
    ```java
    field.get(newInstance);         //返回newInstance对象的field字段所对应的值
    ```
- 修改指定对象的具体成员变量的值
    ```java
    field.set(newInstance,value);               //将newInstance对象的field字段所对应的值修改为value
    ```
    - 注意，使用此方法修改成员变量时，这个变量必须为公共的，如果是非公有成员变量，可以使用Field的setAccessible()方法将其设为可修改
    ```java
    boolean isAccessible();                     //判断这个字段的值设置时是否有Java语言访问检查
    void setAccessible(boolean flag);           //将此对象的accessible标志设置为指定的值，为true则取消在修改时的Java语言访问检查
    ```

---
# 通过反射获取成员方法并使用
- 调用Class类的方法来获取成员方法
```java
Method getMethod(String methodName, Class<?>... parameterTypes);            //获取方法名为methodName的非私有成员方法
Method getDeclaredMethod(String methodName, Class<?>... parameterTypes);    //获取方法名为methodName的成员方法
Method[] getMethods();                                                      //获取该类的所有非私有方法
Method[] getDeclaredMethods();                                              //获取该类的所有成员方法，但不包括继承的方法
```
>  

- 调用Method类的方法来使用成员方法
```java
Object invoke(Object obj,Object... args);       //对带有指定参数的指定对象调用由此Method对象所表示的底层方法
```

---
