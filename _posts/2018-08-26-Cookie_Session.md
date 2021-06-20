---
layout: post
title:  "Cookie&Session"
date:   2018-08-26 20:08:33 +0800
tags: Web
---
# Cookie
### 会话技术
- 本质：浏览器和服务器存储数据来弥补HTTP协议**无状态**的不足
- 主要分类
	- Cookie (数据保存在客户端)
	- Session (数据保存在服务器端)

---
### Cookie的技术的使用
- Cookie
	- 以头的方式进行浏览器和服务器之间的数据交换
	- 本质是一个键值对，键和值的类型都是String
- 创建
	```
	Cookie cookie = new Cookie(String name,String value);	//创建一个名称为name,值为value的Cookie对象
	```
- 服务器写回Cookie
	```
	response.addCookie(Cookie cookie);	//向客户端存储一个cookie对象，名称相同则会覆盖
	```
- 服务器获得客户端请求中携带的Cookie
	```
	Cookie[] request.getCookies()	//返回请求中携带的Cookie
	```

---
### Cookie常用API的介绍和分类
- 常用API
	```
	String getName()					//获取Cookie对象的名称
	String getValue()					//获取Cookie对象的值
	void detPath(String path)			//设置Cookie对象的有效路径
	void setMaxAge(int maxAge);			//设置Cookie对象的有效时长，以秒为单位
	void setDomain(String domain);		//设置Cookie对象的有效域名
	void setHttpOnly(boolean flag);		//设置Cookie只能被HTTP协议访问(前端document对象无法获取)，防止跨站点(xss)攻击
	```
- 分类
	- 会话级别
		- Cookie默认即为会话级别，信息保存在浏览器的内存中，关闭浏览器后就会消失
	- 持久级别
		- 使用Cookie的setMaxAge()方法设置一个有效时长，信息保存在浏览器的磁盘中，关闭浏览器后不会消失
		- **持久级别Cookie的清除**
			 1. 利用Cookie的setPath(String path)方法，设置一个和之前设置持久化cookie的path一致的Cookie对象
			 2. 调用setMaxAge(0)消除

---
# Session
### Session与Cookie的区别
- Cookie大小和个数具有限制
- Session的大小和个数没有限制

---
### Session执行原理
- 将Cookie作为一个查找服务器端数据的索引
- 实现过程
	- 首次请求
		1. 服务器端开辟空间,分配SessionID
		2. 利用Cookie传回SessionID
	- 第二次请求
		1. 服务器根据Cookie中保存的SessionID找到开辟的内存空间
- 代码范例:
    1. HttpSession session = request.getSession();
    ```
    	┕ 去找请求中Cookie的JSESSIONID的值
    		┕ 找得到:拿去JSESSIONID进行下一步
    		┕ 找不到:在服务器内存中开辟一块session区域，并给以标识(JESSIONID)存到Cookie中
    	┕ 根据JSESSIONID的值找服务器的内存中对应的session区域
    		┕ 找得到:return此session区域
    		┕ 找不到:在服务器内存中开辟一块session区域并return
    ```
    2. Object value = session.getAttribute("test");
    ```
        获取session中保存的键为test所对应的值
        无test键则返回null
    ```
    3. session.setAttribute("test","attribute");
    ```
        在session中保存值(键值对的形式)
    ```

---
### 常用API
```
HttpSession getSession(boolean flag)
//HttpServletRequest对象的方法,用于获取Session对象,传入参数为true时必然会返回一个session对象,为false时,通过JSESSIONID找不到session时则返回null
Object getAttribute()                       //获取session中保存的值
void setAttribute(String key,Object value)  //将数据以String=Object键值对的形式存入session中
boolean navigator.cookieEnabled             //JS对象的方法，用于判断用户的浏览器是否开启了Cookie
void invalidate()                   //用于销毁session对象,通常在注销功能中使用
```

---
### Session域功能
- 作用范围
	- 与JSESSIONID相同，默认为一次会话
- 创建时机
	- 通过sessionid找不到之前开辟的session区域时
- 销毁时机
	- 服务器非正常关闭，==服务器正常关闭session会序列化到硬盘==
	- session过期:(默认过期时间为30分钟)
	- 手动调用session.invalidate();

---
#### Session默认有效期的设置
- 在web.xml中可以设置该项目的Session对象的默认有效时长
```
    conf/web.xml ==> 作用在该服务器的所有项目中的session
		<session-config>
			<session-timeout>30</session-timeout>
	    </session-config>
	项目下的/web.xml ==> 设置当前项目的Session对象默认有效时长
		<session-config>
			<session-timeout>30</session-timeout>
	    </session-config>
	数字的单位为分钟
```

---
# 单点登录
- 概念
	- 分布式系统中，在一个系统登录成功以后，在其他系统间可以共享用户的登录信息
- 关键问题：**Session无法跨服务器共享**
- 解决思路
	- Session广播
		- 服务器之间通过广播的方式共享Session
		- 缺点：占用内网带宽，可能产生网络风暴，集群规模大时尤为明显
	- IP_Hash
		- 进行负载均衡时，根据IP分配访问的服务器(同一IP始终访问同一台服务器)
		- 缺点：会导致服务器的性能下降
	- 第三方中间键模拟Session
		- 通过Redis来模拟Session
		- 缺点：引入中间键，系统复杂度提高，维护更为繁琐