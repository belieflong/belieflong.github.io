---
title: Spring框架之-入门简介
date: 2017-05-06 17:23:41
categories:
	- Java
tags:
	- SSH
---
## Spring的概念
### 简介
> spring是一个轻量级控制反转(IoC)和面向切面(AOP)的容器框架，它主要是为了解决企业应用开发的复杂性而诞生的：
目的：解决企业应用开发的复杂性
功能：使用基本的JavaBean代替EJB
范围：任何Java应用

<!-- more -->

### 起源
> Spring的存在是因为它自身有着得天独厚的优势：
- 它定位的领域是许多其他流行的framework没有的
- Spring是全面的和模块化的
- 它的设计从底部帮助你编写易于测试的代码
- Spring是潜在的一站式解决方案

### 优点
> Spring天生就存在如下的优点：
- 低侵入式设计，代码污染极低
- Write Once, Run Anywhere
- DI有效的降低了耦合度
- AOP提供了通用任务的集中管理
- ORM和DAO简化了对数据库访问
- 高度开放性，并不强制
- Spring的优点给开发带来的好处：
- 可以有效组织中间层对象
- 使用统一的配置文件
- 促进良好编程习惯，减少编程代价
- 易于单元测试
- 使EJB成为一种备选
- 为数据存取提供了一致的框架

### 特点
> 
- 方便解耦，简化开发
- AOP编程的支持
- 声明式事务的支持
- 方便程序的测试
- 方便集成各种优秀框架
- 降低JavaEE API的使用难度
- Spring的源码是经典学习范例

### Spring的核心模块
{% img /images/spring/spring_he_xing.png %}

> 
- 核心容器(Spring Core)
- 应用上下文(Spring Context)
- AOP模块(Spring AOP)
- JDBC和DAO模块(Spring DAO)
- 对象实体映射（Spring ORM）
- Web模块(Spring Web)
- MVC模块(Spring Web MVC)

## Spring之IOC

### 浅谈IOC
> IOC（Inversion of Control，控制反转）是spring的核心，贯穿始终。
所谓IOC，对于spring框架来说，就是由spring来负责控制对象的生命周期和对象间的关系：
传统开发模式：对象之间互相依赖
IOC开发模式：IOC容器安排对象之间的依赖

### 依赖注入DI
> IOC的另外的名字叫做依赖注入（Dependency Injection），所谓的依赖注入，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。
所以，依赖注入(DI)和控制反转(IOC)是从不同的角度的描述的同一件事情，就是指通过引入IOC容器，利用依赖关系注入的方式，实现对象之间的解耦

### IOC的好处
> IOC在编程过程中不会对业务对象构成很强的侵入性，使用IOC之后，对象具有更好的可实行性，可重用性和可扩展性：
- 降低组件之间的耦合度
- 提高开发效率和产品质量
- 统一标准，提高模块的复用性
- 模块具有热插拔特性

### IOC通俗的理解
> IOC控制反转：说的是创建对象实例的控制权从代码控制剥离到IOC容器控制，实际就是你在xml文件控制，侧重于原理
DI依赖注入：说的是创建对象实例时，为这个对象注入属性值或其它对象实例，侧重于实现

## Spring之AOP
### AOP的概念
> 通俗理解：面向切面编程，AOP将应用系统分为两个部分：核心业务逻辑、横向的通用逻辑（即:方面：持久化管理、事务管理、安全管理、日志管理，调试管理等等）
在Spring当中提供了面向切面编程的丰富支持：允许通过分离应用的业务逻辑与系统及的服务，进行内聚性的开发，应用对象只实现他们应该做的，也就是完成业务逻辑，并不负责其他关注点。

### AOP和OOP的关系
> **AOP**是对OOP面向对象编程有意的补充，同时AOP也是OOP的延续
**OOP**：从静态角度考虑程序结构，即：OOP对业务处理过程的中的实体、以及属性和行为进行了抽象的封装，也或得更加清晰高效果的逻辑划分，研究的是静态的领域
**AOP**：从动态角度考虑程序运行过程，即：针对业务处理过程中的切面进行提取，它所面对的是处理中的某个步骤或者阶段，研究的是静态的领域

### AOP的主要功能
> 主要是用于系统级别的功能。例如：日志记录、性能统计、安全控制、事务处理、异常处理等等

### AOP的主要意图
> - 把代码从业务逻辑代码中划分出来，通过对这些行为的分离，我们希望可以将它们独立到非指导性业务逻辑方法当中，进而改变这一行为的时候，不影响业务逻辑代码的处理。也就是说：AOP把一些常用的服务进行模块化，并且用声明的方式将这些组件使用到其他的业务组件中去，这样做的结果是，每一个业务组件，只需要关系自己的业务逻辑，而不用理解一些常用的业务组件，这样就保证了更高的内聚性。
- 使用AOP你可以将处理切面等代码注入程序，通常主程序的主要目的并不在于处理这些切面的功能，所以AOP可以有效的防止代码混乱。
- spring-framework的AOP作为一种轻型的AOP-framework，无需使用预编译器，或其他元标签，可以在JAVA程序中使用。

### AOP的价值
>AOP 专门用于处理系统中分布于各个模块中的交叉关注点的问题，在 Java EE 应用中，常常通过 AOP 来处理一些具有横切性质的系统级服务，如事务管理、安全检查、缓存、对象池管理等，AOP 已经成为一种非常常用的解决方案

### AOP的 原理剖析
> **AOP** 代理其实是由 AOP 框架动态生成的一个对象，该对象可作为目标对象使用，AOP 代理所包含的方法与目标对象的方法如下图所示：

{% img /images/spring/spring_yuan_li.png %}

> 
- 定义普通业务组件
- 定义切入点
- 定义增强处理 
- 代理对象的方法 = 增强处理 + 被代理对象的方法

### AOP的关键概念

> 以下是官方文档所给出的AOP的关键概念的解释：
切面 - Aspect
连接点 - Join Point
通知 - Advice
切入点 - Point Cut
引入 - Introduction
目标对象 - Target Object
AOP代理 - AOP Proxy
织入 - Weaving

### AOP的通俗理解

> AOP通俗的理解：
一个组件A，不关心其他常用的服务组件B，但是这个组件A使用组件B的时候，不是组件A自身去调用，而是通过配置等其他方式，
比如Spring中可以通过xml配置文件。这样就使得A压根就不需要知道服务组件B是怎样的，爱存在不存在，爱怎么存在都与A无关。
A只关心自己的业务逻辑，具体A使用B的时候，配置文件去做，与具体的A组件无关。

## Spring开发包介绍

### Spring的核心开发包的基本用途

> **Spring Core**：包含Spring框架的核心工具类，是其他组件的基本核心
**Spring Beans**：是所有应用都要用到的，它包含了访问配置文件、创建和管理Bean、以及进行控制反转、和依赖注入相关的所有类
**Spring AOP**：包含了使用Spring的AOP特性时所需要的类，利用这个jar文件，可以使用基于AOP的Spring特性。如：声明性的事务管理、日志系统的引入等等
**Spring Context**：为Spring的核心提供了大量的扩展，能够找到SpringAppliContexts特性时所需要的全部类、JNDI所需要的全部类、UI方面的用来和模版引擎,如：freemarker(用来生成输出文本的通用工具)、jasperreport(报表生成工具)集成的类,
以及校验方面的相关类。

### Spring的业务组件包（提供了各种企业级服务）

> **Spring Aspects**：提供了对了对AspectJ(面向切面的框架)的支持，以便可以方便的，将面向方面的功能集成进IDE中，比如：Eclipse、Ajdt(Eclipse基金的AspectJ是其中一个比较流行的AOP实现的插件)。
**Spring Context Support**：包含了支持缓存Cache、JCA(J2EE 连接器架构，是对J2EE标准集的重要补充)、JMX(Java管理扩展）是一个为应用程序、设备、系统等植入管理功能的框架)、邮件服务、任务计划等方面的这些所有类。
**Spring Expression**：是Spring表达式语言，Spring3.0创建了一种新的方式，用以配置对象的注入，便是Spel (Spring Expression Language (SpEL))，支持在运行时操作和查询对象语法类似于 EL 语言，但是SpEL提供了额外的功能。
**Spring Framework Bom**：它是在使用 Maven (项目对象模型(POM)，可以通过一小段描述信息来管理项目的构建，报告和文档的软件项目管理工具)时,确保所有的Spring模块，都使用统一的版本。
**Spring Instrument**：提供Spring3.0对服务器的代理接口。
**Spring Instrument Tomcat**：提供了Spring3.0对Tomcat连接池的集成。
**Spring JDBC**：包含了Spring对JDBC数据访问时，进行封装的所有类，Spring提供了两种使用JDBC API的最佳时间：
- 以JdbcTemplate为核心的基于Template JDBC的使用方式
- 是在JdbcTemplate的基础之上构建的基于操作对象的Jdbc的使用方式。
> 
**Spring JMS**：提供了对JMS 1.0和1.1的支持类，Spring的JMS抽象框架简化了JMS API的使用，并与JMS的提供者平滑的集成，org.springframework.jms.core包提供了在Spring中使用JMS的核心功能，它的模版类处理资源的创建和释放，简化了JMS的使用。
**Spring ORM**：Spring对DAO特性进行了扩展，使其支持iBatis、JDO、OJB、TopLink，因为hibernate已经独立承包，所以不包含在这个包里面了。这个JAR文件里大部分的类都需要依赖Spring-DAO.jar，所以使用这个包时，要包含进去。
**Spring OXM**：(Object-to-XML-Mapping的缩写)Spring对Object、XML的映射支持。可以让Java与Xml之间来回切换，是Spring3.0的一个新特性，OXM即是O/X-mapper，O/X映射器这个概念并不新鲜，O 代表 Object，X 代表 XML，它的目的是在Java对象和Xml文档之间相互转换。
**Spring Struts**：它提供了对Struts框架的支持，可以更方便更容易的集成Struts框架。
**Spring test**：它提供了对Junit等测试框架的简单封装，这让我们在对Spring的代码进行测试时更加方便和快捷。
**Spring tx**：即:Spring Transaction它为JDBC、Hibernate、JDO、JPA等提供的一致的声明式的编程式事务管理。
**Spring web**：包含Web应用研发时用到Spring框架时所需要的核心类，包括自动载入、WebApplicationContext特性的类、Struts和JFF集成类、文件上传的集成类、Filter类和大量辅组工具类。
**Spring webmvc**：包含了Spring mvc 框架的所有类，包括国际化、标签、视图展映的FreeMarker、jasperreport、Tiles、XSLT相关类，如果项目中使用了独立的MVC框架，则无需使用此类。
**Spring webmvc portlet**：提供了对Spring mvc的增强，支持了portlet标准