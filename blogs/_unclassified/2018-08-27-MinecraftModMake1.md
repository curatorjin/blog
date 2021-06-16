---
layout: post
title:  "基于FML的MinecraftMod制作学习笔记——开发环境的配置"
date:   2018-8-27 11:05:44 +0800
categories: unclassified
---
# 首先……
- 以下为个人学习Minecraft1.7.10Mod开发时的流程和一些心得，其中涉及到了一些Java的知识，在此与大家分享
- 相比我所使用的这种开发方式，现在已经有了很多的可视化Mod制作工具，很方便而且基本不需要编程知识，如果只是想轻松制作属于自己的Mod的话，可以先考虑制作工具
- 暂不提供任何整合包



# 工具及基本环境
- JDK版本：1.7
- 开发工具：IntelliJ IDEA U

---
# 基本概念
- MCP(Minecraft Coder Pack)
	- Minecraft的软件开发工具包，由于MC是闭源的，并且其源代码经过了混淆操作，变量名为无意义的文字(在后续的开发过程中会见识到的)。所以在对其进行开发的时候就要先进行反编译。而MCP是被官方默许的反向工程项目并附带反混淆。可以说MCP是Mod开发的基础
- Forge
	- MinecraftModAPI库，实现了一些最基本的功能
- FML
	- ForgeModLoader，用于加载Mod。早先的时候，还有一个叫ModLoader的Mod也实现了相同的功能，但目前FML已经成为了主要的加载工具。如今MCP基本已经弃坑了，而FML正好接替了MCP的任务。
- ForgeGradle
	- 一个封装好了的Gradle构建工具，Gradle可以看成是一个简化了的Maven工具，可以简单的直接构建好我们所需要的开发环境(个人对其的了解并不多，事实上整个开发过程对于Gradle的使用也很简单)。
- MDK
	- 即将要搭建的Mod开发环境~

---
# 配置MDK
- **开发版本**
	- Forge版本：10.13.4.1614
	- MC版本：1.7.10

- **步骤**
	1. **下载MDK**
		- 下载地址:<a>http://files.minecraftforge.net/</a>
		- 这一步很简单，找到**对应的版本**之后点Src就好(网络的话可能需要魔法)
	2. **解压文件**，在解压得到的文件夹中打开命令提示符输入
	```
	gradlew.bat setupDecompWorkspace
	```
	
		> 这一步其实就是运行gradlew.bat文件并使用setupDecompWorkspace参数
	
	3. **配置IDEA**
		编辑build.gradle文件(Notepad++打开)，在最后加上
		```
		idea { 
		    module { 
		        inheritOutputDirs = true 
		    } 
		}
		```
	保存之后，在命令窗口中执行
		```
		gradlew.bat idea genIntellijRuns
		```
		执行完毕之后，这个文件夹就已经变成了一个IDEA项目的目录了。这时打开IDEA，直接OPEN这个MDK目录就可以开始Mod的开发了~~

- **测试运行**
	- 点击Run，可以看到Minecraft Client(客户端)和Minecraft Server(服务端)，选择客户端就可以进入游戏了~~

---
		
# 可能遇到的问题……
>  主要是第二步中的gradlew.bat setupDecompWorkspace指令

- **依赖无法下载**
	- 在配置MDK开发环境的时候第二步用时最长，虽然只需要在命令窗口内执行一行代码，但在执行这一条指令时，Gradle会按照build.gradle文件中的配置信息去构建项目，类比Maven的项目构建，这一步必然会涉及到下载依赖相关jar包，一部分是在Maven中央仓库，还有一部分是在Forge的网站……因此首先要准备好**科学上网法**
- **找不到JSON文件**
	- 在下载完依赖文件之后有可能会提示**xxx.json could not be parsed**和**FileNotFoundException: Inherited json file (null) not found**之类的错误。这是由于找不到相应的JSON文件(废话)……我也没有找到正当的解决方法，不过只要**把Minecraft游戏文件中的.minecraft\assets\indexes\1.7.10.json文件放到那个对应的目录下**就可以解决这个问题了。
	- 实际上这个文件应该是在build过程中生成或是在依赖中下载到的，发生这个问题的原因我也没有深究(毕竟有一个可以凑合解决的方法)。个人推测可能是由于文件权限……
- **待发现**
	- 暂且只遇到了这几个问题，如果发现有其他的问题欢迎和我一起讨论(～￣▽￣)～