---
layout: post
title:  "注解"
date:   2018-08-27 00:48:00 +0800
tags: Java
---
# 注解的概念
- 概念
	- 给编译器或者虚拟机看的一个标识
- 作用
	- 规范代码的编写
	- **携带一些数据**

---
# 注解的属性
- 属性
	- 注解可以携带一些属性，使得被其标识的方法(变量或类)具有其他不同的功能
	- 注解支持的属性类型为:基本数据类型、字符串类型、注解类型、枚举类型、以及以上类型的一位数组
- 使用方法
	- 在注解时给其携带的属性赋值
	```java
	@Anno_name(属性名1=属性值1,属性名2=属性值2...)
	```
	- 属性的定义
	```java
	@interface Anno_name{
		属性类型 属性名() 属性的默认值;
		属性类型 属性名2();
	}
	```
- 注意事项
	- 使用注解时，不对其携带的属性进行赋值则会自动赋为默认值
	- 若属性没有默认值，则必须赋值
	- 若只有一个名为value的属性值需要赋值，则"value="可以省略
	```java
	@Anno_name(value="value")-->@Anno_name("value")
	```

---
# 修饰注解的注解
> 要用魔法打败魔法

- @Retention
	- 自定义注解的存在时机
	- 属性值:value
	```java
	RetentionPolicy.SOURCE 		//被修饰的注解仅存在于Java形态
	RetentionPolicy.CLASS 		//被修饰的注解存在到class形态
	RetentionPolicy.RUNTIME 	//被修饰的注解一直存在到运行时期
	```
- @Target
	- 自定义注解的可修饰对象
	- 属性值:value
	```java
	ElementType.TYPE 			//被修饰的注解只能用于修饰类
	ElementType.METHOD 			//被修饰的注解只能用于修饰方法
	ElementType.FIELD 			//被修饰的注解只能用于修饰修饰字段
	ElementType.PARAMETER 		//被修饰的注解只能用于修饰参数
	//由于value是枚举类型，故可以在此规定其修饰的注解的修饰范围
	```

---
# 注解的使用方法
- 核心思想:反射
```java
class.getAnnotation(Anno.class)			//获取类上的指定Anno注解,如没有改该注解则返回null
method.getAnnotation(Anno.class)		//获取方法上的指定Anno注解,如没有改该注解则返回null
field.getAnnotation(Anno.class)			//获取字段上的指定Anno注解,如没有改该注解则返回null
parameter.getAnnotation(Anno.class)		//获取参数上的指定Anno注解,如没有改该注解则返回null
annotation.属性名()						//获取注解携带的属性
```

---
