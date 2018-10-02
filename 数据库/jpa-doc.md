# Spring Data Jpa 文档

标签（空格分隔）： JPA Spring

---

Spring Data JPA - 参考文档
======================

Oliver  
Gierke Thomas Darimont  
Christoph Strobl  
Mark Paluch  
杰伊布莱恩特  
版本 2.1.0.M3,2018-05-17

©2008-2018原作者。

本文件副本可供您自行使用并分发给其他人，前提是您不收取任何此类副本的费用，并进一步规定每份副本均包含此版权声明，无论是以印刷版还是电子版分发。

目录

*   [前言](#preface)
    *   [1.项目元数据](#project)
    *   [2.新的＆值得注意的](#new-features)
        *   [2.1。Spring Data JPA 1.11中的新特性](#new-features.1-11-0)
        *   [2.2。Spring Data JPA 1.10中的新特性](#new-features.1-10-0)
    *   [3.依赖性](#dependencies)
        *   [3.1。Spring Boot的依赖管理](#dependencies.spring-boot)
        *   [3.2。Spring框架](#dependencies.spring-framework)
    *   [4.使用Spring数据存储库](#repositories)
        *   [4.1。核心概念](#repositories.core-concepts)
        *   [4.2。查询方法](#repositories.query-methods)
        *   [4.3。定义存储库接口](#repositories.definition)
            *   [4.3.1。微调储存库定义](#repositories.definition-tuning)
            *   [4.3.2。仓库方法的空处理](#repositories.nullability)
            *   [4.3.3。将存储库与多个Spring数据模块一起使用](#repositories.multiple-modules)
        *   [4.4。定义查询方法](#repositories.query-methods.details)
            *   [4.4.1。查询查询策略](#repositories.query-methods.query-lookup-strategies)
            *   [4.4.2。查询创建](#repositories.query-methods.query-creation)
            *   [4.4.3。属性表达式](#repositories.query-methods.query-property-expressions)
            *   [4.4.4。特殊参数处理](#repositories.special-parameters)
            *   [4.4.5。限制查询结果](#repositories.limit-query-result)
            *   [4.4.6。流式查询结果](#repositories.query-streaming)
            *   [4.4.7。异步查询结果](#repositories.query-async)
        *   [4.5。创建存储库实例](#repositories.create-instances)
            *   [4.5.1。XML配置](#repositories.create-instances.spring)
            *   [4.5.2。JavaConfig](#repositories.create-instances.java-config)
            *   [4.5.3。独立使用](#repositories.create-instances.standalone)
        *   [4.6。Spring数据仓库的自定义实现](#repositories.custom-implementations)
            *   [4.6.1。定制个人存储库](#repositories.single-repository-behavior)
            *   [4.6.2。自定义基础知识库](#repositories.customize-base-repository)
        *   [4.7。从聚合根发布事件](#core.domain-events)
        *   [4.8。Spring数据扩展](#core.extensions)
            *   [4.8.1。Querydsl扩展](#core.extensions.querydsl)
            *   [4.8.2。Web支持](#core.web)
            *   [4.8.3。存储库Poppop](#core.repository-populators)
*   [参考文档](#reference)
    *   [5\. JPA存储库](#jpa.repositories)
        *   [5.1。介绍](#jpa.introduction)
            *   [5.1.1。Spring命名空间](#jpa.namespace)
            *   [5.1.2。基于注释的配置](#jpa.java-config)
        *   [5.2。坚持实体](#jpa.entity-persistence)
            *   [5.2.1。保存实体](#jpa.entity-persistence.saving-entites)
        *   [5.3。查询方法](#jpa.query-methods)
            *   [5.3.1。查询查询策略](#jpa.sample-app.finders.strategies)
            *   [5.3.2。查询创建](#jpa.query-methods.query-creation)
            *   [5.3.3。使用JPA命名查询](#jpa.query-methods.named-queries)
            *   [5.3.4。运用`@Query`](#jpa.query-methods.at-query)
            *   [5.3.5。使用排序](#jpa.query-methods.sorting)
            *   [5.3.6。使用命名参数](#jpa.named-parameters)
            *   [5.3.7。使用SpEL表达式](#jpa.query.spel-expressions)
            *   [5.3.8。修改查询](#jpa.modifying-queries)
            *   [5.3.9。应用查询提示](#jpa.query-hints)
            *   [5.3.10。配置提取和LoadGraphs](#jpa.entity-graph)
            *   [5.3.11。预测](#projections)
        *   [5.4。存储过程](#jpa.stored-procedures)
        *   [5.5。产品规格](#specifications)
        *   [5.6。按实例查询](#query-by-example)
            *   [5.6.1。介绍](#query-by-example.introduction)
            *   [5.6.2。用法](#query-by-example.usage)
            *   [5.6.3。示例匹配器](#query-by-example.matchers)
            *   [5.6.4。执行一个例子](#query-by-example.execution)
        *   [5.7。事务性](#transactions)
            *   [5.7.1。事务查询方法](#transactional-query-methods)
        *   [5.8。锁定](#locking)
        *   [5.9。审计](#auditing)
            *   [5.9.1。基本](#auditing.basics)
            *   [5.9.2。JPA审计](#jpa.auditing)
        *   [5.10。其他注意事项](#jpa.misc)
            *   [5.10.1。使用`JpaContext`在自定义实现](#jpa.misc.jpa-context)
            *   [5.10.2。合并持久性单元](#jpa.misc.merging-persistence-units)
            *   [5.10.3。CDI集成](#jpd.misc.cdi-integration)
*   [附录](#appendix)
    *   [附录A：命名空间参考](#repositories.namespace-reference)
        *   [该`<repositories />`元素](#populator.namespace-dao-config)
    *   [附录B：Poppers命名空间参考](#populator.namespace-reference)
        *   [<populator />元素](#namespace-dao-config)
    *   [附录C：存储库查询关键字](#repository-query-keywords)
        *   [支持的查询关键字](#_supported_query_keywords)
    *   [附录D：存储库查询返回类型](#repository-query-return-types)
        *   [支持的查询返回类型](#_supported_query_return_types)
    *   [附录E：常见问题](#faq)
        *   [共同](#_common)
        *   [基础设施](#_infrastructure)
        *   [审计](#_auditing)
    *   [附录F：术语表](#glossary)

[](#preface)前言
==============

Spring Data JPA为Java持久性API（JPA）提供存储库支持。它简化了需要访问JPA数据源的应用程序的开发。

[](#project)1.项目元数据
-------------------

*   版本控制 \- [http://github.com/spring-projects/spring-data-jpa](https://github.com/spring-projects/spring-data-jpa)
    
*   Bugtracker - [https://jira.spring.io/browse/DATAJPA](https://jira.spring.io/browse/DATAJPA)
    
*   发行版本库 \- [https://repo.spring.io/libs-release](https://repo.spring.io/libs-release)
    
*   里程碑存储库 \- [https://repo.spring.io/libs-milestone](https://repo.spring.io/libs-milestone)
    
*   快照存储库 \- [https://repo.spring.io/libs-snapshot](https://repo.spring.io/libs-snapshot)
    

[](#new-features)2.新的＆值得注意的
---------------------------

### [](#new-features.1-11-0)2.1。Spring Data JPA 1.11中的新特性

Spring Data JPA 1.11增加了以下功能：

*   改进与Hibernate 5.2的兼容性。
    
*   [通过示例](#query-by-example)支持任意匹配模式。
    
*   分页查询执行优化。
    
*   支持`exists`存储库查询派生中的投影。
    

### [](#new-features.1-10-0)2.2。Spring Data JPA 1.10中的新特性

Spring Data JPA 1.10增加了以下功能：

*   支持存储库查询方法中的[投影](#projections)。
    
*   [通过示例](#query-by-example)支持[查询](#query-by-example)。
    
*   以下注解已启用的基础上组成的注释：`@EntityGraph`，`@Lock`，`@Modifying`，`@Query`，`@QueryHints`，和`@Procedure`。
    
*   支持`Contains`集合表达式的关键字。
    
*   `AttributeConverter`为实现`ZoneId`JSR-310和ThreeTenBP的。
    
*   升级到Querydsl 4，Hibernate 5，OpenJPA 2.4和EclipseLink 2.6.1。
    

[](#dependencies)3.依赖性
----------------------

由于各个Spring Data模块的初始日期不同，它们中的大多数都带有不同的主版本号和次版本号。寻找兼容版本的最简单方法是依靠我们随定义的兼容版本提供的Spring Data Release BOM。在Maven项目中，您将在`<dependencyManagement />`POM 的部分声明这种依赖关系，如下所示：

示例1.使用Spring Data发行版BOM

    <dependencyManagement>
      <dependencies>
        <dependency>
          <groupId>org.springframework.data</groupId>
          <artifactId>spring-data-releasetrain</artifactId>
          <version>${release-train}</version>
          <scope>import</scope>
          <type>pom</type>
        </dependency>
      </dependencies>
    </dependencyManagement>

目前的发行版本是`Lovelace-M3`。列车名称按字母顺序上升，目前可用的列车在[此处](https://github.com/spring-projects/spring-data-commons/wiki/Release-planning)列出。版本名称遵循以下模式：`${name}-${release}`，其中发布可以是下列之一：

*   `BUILD-SNAPSHOT`：当前快照
    
*   `M1`，`M2`等等：里程碑
    
*   `RC1`，`RC2`等等：发布候选人
    
*   `RELEASE`：GA版本
    
*   `SR1`，`SR2`等等：服务版本
    

在我们的[Spring Data示例存储库中](https://github.com/spring-projects/spring-data-examples/tree/master/bom)可以找到使用BOM的一个工作示例。有了这个，你可以在块中声明你想使用的Spring数据模块而不需要版本`<dependencies />`，如下所示：

例2.声明一个依赖到Spring Data模块

    <dependencies>
      <dependency>
        <groupId>org.springframework.data</groupId>
        <artifactId>spring-data-jpa</artifactId>
      </dependency>
    <dependencies>

### [](#dependencies.spring-boot)3.1。Spring Boot的依赖管理

Spring Boot为您选择最新版本的Spring Data模块。如果您仍想升级到较新版本，请将该属性配置为您要使用`spring-data-releasetrain.version`的[火车名称和迭代](#dependencies.train-names)。

### [](#dependencies.spring-framework)3.2。Spring框架

当前版本的Spring Data模块需要版本5.0.6.RELEASE或更高版本的Spring Framework。这些模块也可能与该次要版本的旧版错误修复版本一起工作。但是，强烈建议使用该代中的最新版本。

[](#repositories)4.使用Spring数据存储库
--------------------------------

Spring Data存储库抽象的目标是显着减少为各种持久性存储实现数据访问层所需的样板代码数量。

_Spring数据存储库文档和你的模块_

本章介绍Spring Data存储库的核心概念和接口。本章中的信息来自Spring Data Commons模块。它使用Java持久性API（JPA）模块的配置和代码示例。您应该将XML名称空间声明和要扩展的类型调整为您使用的特定模块的等同项。“ [命名空间参考](#repositories.namespace-reference) ”涵盖了所有支持存储库API的Spring Data模块支持的XML配置。“ [存储库查询关键字](#repository-query-keywords) ”一般涵盖了存储库抽象支持的查询方法关键字。有关模块特定功能的详细信息，请参阅本文档的该模块章节。

### [](#repositories.core-concepts)4.1。核心概念

Spring Data存储库抽象中的中心接口是`Repository`。它需要管理域类以及域类的ID类型作为类型参数。该接口主要作为标记接口来捕获要使用的类型，并帮助您发现扩展该接口的接口。该`CrudRepository`规定对于正在管理的实体类复杂的CRUD功能。

例3\. `CrudRepository`接口

    public interface CrudRepository<T, ID extends Serializable>
      extends Repository<T, ID> {
    
      <S extends T> S save(S entity);      (1)
    
      Optional<T> findById(ID primaryKey); (2)
    
      Iterable<T> findAll();               (3)
    
      long count();                        (4)
    
      void delete(T entity);               (5)
    
      boolean existsById(ID primaryKey);   (6)
    
      // … more functionality omitted.
    }

**1**

保存给定的实体。

**2**

返回由给定ID标识的实体。

**3**

返回所有实体。

**4**

返回实体的数量。

**五**

删除给定的实体。

**6**

指示是否存在具有给定ID的实体。

我们还提供持久性技术特定抽象，如`JpaRepository`或`MongoRepository`。这些接口扩展`CrudRepository`并公开了持久化技术的基本功能，以及相当通用的持久化技术无关接口，例如`CrudRepository`。

除此之外`CrudRepository`，还有一个`PagingAndSortingRepository`抽象增加了其他方法来简化对实体的分页访问：

示例4\. `PagingAndSortingRepository`接口

    public interface PagingAndSortingRepository<T, ID extends Serializable>
      extends CrudRepository<T, ID> {
    
      Iterable<T> findAll(Sort sort);
    
      Page<T> findAll(Pageable pageable);
    }

要访问`User`页面大小为20 的第二页，您可以执行以下操作：

    PagingAndSortingRepository<User, Long> repository = // … get access to a bean
    Page<User> users = repository.findAll(new PageRequest(1, 20));

除了查询方法外，count和delete查询的查询派生都是可用的。以下列表显示派生计数查询的接口定义：

示例5.派生计数查询

    interface UserRepository extends CrudRepository<User, Long> {
    
      long countByLastname(String lastname);
    }

以下列表显示派生删除查询的接口定义：

示例6.派生删除查询

    interface UserRepository extends CrudRepository<User, Long> {
    
      long deleteByLastname(String lastname);
    
      List<User> removeByLastname(String lastname);
    }

### [](#repositories.query-methods)4.2。查询方法

标准CRUD功能存储库通常会在底层数据存储上进行查询。使用Spring Data，声明这些查询变成了一个四步过程：

1.  声明一个扩展Repository或其子接口的接口，并将其键入它应该处理的域类和ID类型，如以下示例所示：
    
        interface PersonRepository extends Repository<Person, Long> { … }
    
2.  在接口上声明查询方法。
    
        interface PersonRepository extends Repository<Person, Long> {
          List<Person> findByLastname(String lastname);
        }
    
3.  设置Spring以使用[JavaConfig](#repositories.create-instances.java-config)或[XML配置](#repositories.create-instances)为这些接口创建代理实例。
    
    1.  要使用Java配置，请创建类似于以下的类：
        
            import org.springframework.data.jpa.repository.config.EnableJpaRepositories;
            
            @EnableJpaRepositories
            class Config {}
        
    2.  要使用XML配置，请定义一个类似于以下的bean：
        
            <?xml version="1.0" encoding="UTF-8"?>
            <beans xmlns="http://www.springframework.org/schema/beans"
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xmlns:jpa="http://www.springframework.org/schema/data/jpa"
               xsi:schemaLocation="http://www.springframework.org/schema/beans
                 http://www.springframework.org/schema/beans/spring-beans.xsd
                 http://www.springframework.org/schema/data/jpa
                 http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">
            
               <jpa:repositories base-package="com.acme.repositories"/>
            
            </beans>
        
    
    这个例子中使用了JPA命名空间。如果您对任何其他商店使用存储库抽象，则需要将其更改为商店模块的相应名称空间声明。换句话说，你应该交换`jpa`赞成，例如`mongodb`。
    
    +另请注意，JavaConfig变体不会显式配置包，因为缺省情况下会使用注释类的包。要定制要扫描的软件包，请使用`basePackage…`特定于数据存储库的`@Enable${store}Repositories`注释的一个属性。
    
4.  注入资源库实例并使用它，如以下示例所示：
    
        class SomeClient {
        
          private final PersonRepository repository;
        
          SomeClient(PersonRepository repository) {
            this.repository = repository;
          }
        
          void doSomething() {
            List<Person> persons = repository.findByLastname("Matthews");
          }
        }
    

以下部分详细解释每一步：

*   [定义存储库接口](#repositories.definition)
    
*   [定义查询方法](#repositories.query-methods.details)
    
*   [创建存储库实例](#repositories.create-instances)
    
*   [Spring数据仓库的自定义实现](#repositories.custom-implementations)
    

### [](#repositories.definition)4.3。定义存储库接口

首先，定义一个域类特定的存储库接口。该接口必须扩展`Repository`并键入域类和ID类型。如果您想公开该域类型的CRUD方法，请扩展`CrudRepository`而不是`Repository`。

#### [](#repositories.definition-tuning)4.3.1。微调储存库定义

通常情况下，你的资料库接口扩展`Repository`，`CrudRepository`或`PagingAndSortingRepository`。或者，如果您不想扩展Spring Data接口，也可以使用注释库接口进行注释`@RepositoryDefinition`。扩展`CrudRepository`公开了一套完整的方法来操纵你的实体。如果您想选择暴露的方法，请将要公开的方法复制`CrudRepository`到您的域存储库中。

这样做可以让您在提供的Spring Data Repositories功能之上定义自己的抽象。

以下示例显示如何选择性地公开CRUD方法（`findById`以及`save`在这种情况下）：

示例7.选择性地暴露CRUD方法

    @NoRepositoryBean
    interface MyBaseRepository<T, ID extends Serializable> extends Repository<T, ID> {
    
      Optional<T> findById(ID id);
    
      <S extends T> S save(S entity);
    }
    
    interface UserRepository extends MyBaseRepository<User, Long> {
      User findByEmailAddress(EmailAddress emailAddress);
    }

在前面的例子，你定义为所有站点库一个共同的基础界面和暴露`findById(…)`，以及`save(…)`。这些方法被发送到基础信息库实现你所选择的由Spring提供的数据（例如，如果使用JPA商店，该实现是`SimpleJpaRepository`），因为它们匹配中的方法签名`CrudRepository`。因此，`UserRepository`现在可以保存用户，通过ID查找单个用户，并触发查询以`Users`通过电子邮件地址查找。

中间存储库接口用注释`@NoRepositoryBean`。确保将该注释添加到Spring Data不应在运行时为其创建实例的所有存储库接口。

#### [](#repositories.nullability)4.3.2。仓库方法的空处理

从Spring Data 2.0开始，返回单个聚合实例的存储库CRUD方法使用Java 8 `Optional`来指示潜在的缺失值。除此之外，Spring Data支持在查询方法上返回以下包装类型：

*   `com.google.common.base.Optional`
    
*   `scala.Option`
    
*   `io.vavr.control.Option`
    
*   `javaslang.control.Option` （由于Javaslang已被弃用）
    

或者，查询方法可以选择不使用包装类型。然后通过返回来指示没有查询结果`null`。存储库方法返回集合，集合备选方案，包装器和流保证永远不会返回`null`，而是相应的空表示。有关详细信息，请参阅“ [存储库查询返回类型](#repository-query-return-types) ”。

##### [](#repositories.nullability.annotations)可空性注释

您可以使用[Spring Framework的可空性注释](https://docs.spring.io/spring/docs/5.0.6.RELEASE/spring-framework-reference/core.html#null-safety)来表示存储库方法的可空约束。它们提供了一个工具友好的方法，并`null`在运行期间进行选择性检查，如下所示：

*   [`@NonNullApi`](https://docs.spring.io/spring/docs/5.0.6.RELEASE/javadoc-api/org/springframework/lang/NonNullApi.html)：在包级别上用于声明参数和返回值的默认行为是不接受或生成`null`值。
    
*   [`@NonNull`](https://docs.spring.io/spring/docs/5.0.6.RELEASE/javadoc-api/org/springframework/lang/NonNull.html)：用于参数或返回值，不能是`null` （参数不需要，返回值`@NonNullApi`适用）。
    
*   [`@Nullable`](https://docs.spring.io/spring/docs/5.0.6.RELEASE/javadoc-api/org/springframework/lang/Nullable.html)：用于可以是的参数或返回值`null`。
    

Spring注释使用[JSR 305](https://jcp.org/en/jsr/detail?id=305)注释进行元注释（一种休眠但广泛传播的JSR）。JSR 305元注释让工具供应商（如[IDEA](https://www.jetbrains.com/help/idea/nullable-and-notnull-annotations.html)，[Eclipse](http://help.eclipse.org/oxygen/index.jsp?topic=/org.eclipse.jdt.doc.user/tasks/task-using_external_null_annotations.htm)和[Kotlin）](https://kotlinlang.org/docs/reference/java-interop.html#null-safety-and-platform-types)以通用方式提供空安全支持，而无需为Spring注释提供硬编码支持。要启用对查询方法的可空约束的运行时检查，您需要使用Spring的`@NonNullApi`in 激活包级别的非可空性`package-info.java`，如以下示例所示：

示例8.在中声明不可为空 `package-info.java`

    @org.springframework.lang.NonNullApi
    package com.acme;

一旦存在非空默认值，存储库查询方法调用将在运行时验证可空性约束。如果查询执行结果违反了定义的约束，则会引发异常。当方法返回时，会发生这种情况，`null`但声明为非空（存储库所在的包上定义了注释的默认值）。如果您想再次选择可空结果，请选择性地使用`@Nullable`单个方法。使用本节开始提到的结果包装类型将继续按预期工作：将空结果转换为表示不存在的值。

以下示例显示了刚刚描述的许多技术：

例子9.使用不同的可空性约束

    package com.acme;                                                       (1)
    
    import org.springframework.lang.Nullable;
    
    interface UserRepository extends Repository<User, Long> {
    
      User getByEmailAddress(EmailAddress emailAddress);                    (2)
    
      @Nullable
      User findByEmailAddress(@Nullable EmailAddress emailAdress);          (3)
    
      Optional<User> findOptionalByEmailAddress(EmailAddress emailAddress); (4)
    }

**1**

存储库驻留在我们为其定义非空行为的包（或子包）中。

**2**

`EmptyResultDataAccessException`当执行的查询不产生结果时抛出一个。`IllegalArgumentException`当`emailAddress`交给方法时抛出一个`null`。

**3**

`null`当执行的查询不会产生结果时返回。也接受`null`作为的价值`emailAddress`。

**4**

`Optional.empty()`当执行的查询不会产生结果时返回。`IllegalArgumentException`当`emailAddress`交给方法时抛出一个`null`。

##### [](#repositories.nullability.kotlin)基于Kotlin的知识库中的可空性

Kotlin定义了可用于语言的可[空性约束](https://kotlinlang.org/docs/reference/null-safety.html)。Kotlin代码编译为字节码，该字节码不通过方法签名表示可空约束，而是通过编译后的元数据表示。确保`kotlin-reflect`在项目中包含JAR，以便对Kotlin的可空性限制进行反省。Spring Data存储库使用语言机制来定义这些约束以应用相同的运行时检查，如下所示：

例10.在Kotlin存储库上使用可空性约束

    interface UserRepository : Repository<User, String> {
    
      fun findByUsername(username: String): User     (1)
    
      fun findByFirstname(firstname: String?): User? (2)
    }

**1**

该方法将参数和结果定义为不可空（Kotlin默认值）。Kotlin编译器拒绝传递`null`给方法的方法调用。如果查询执行产生空结果，`EmptyResultDataAccessException`则抛出。

**2**

该方法接受`null`的`firstname`参数，并返回`null`，如果查询执行不产生结果。

#### [](#repositories.multiple-modules)4.3.3。将存储库与多个Spring数据模块一起使用

在应用程序中使用独特的Spring Data模块使事情变得简单，因为定义范围中的所有存储库接口都绑定到Spring Data模块。有时，应用程序需要使用多个Spring Data模块。在这种情况下，存储库定义必须区分持久性技术。当它在类路径中检测到多个存储库工厂时，Spring Data会进入严格的存储库配置模式。严格配置使用存储库或域类上的详细信息来决定存储库定义的Spring Data模块绑定：

1.  如果存储库定义[扩展了特定于模块的存储库](#repositories.multiple-modules.types)，那么它是特定Spring Data模块的有效候选者。
    
2.  如果域类[使用特定于模块的类型注释进行注释](#repositories.multiple-modules.annotations)，则它是特定的Spring Data模块的有效候选者。Spring Data模块接受第三方注释（比如JPA `@Entity`）或者提供他们自己的注解（例如`@Document`Spring Data MongoDB和Spring Data Elasticsearch）。
    

以下示例显示使用模块特定接口（本例中为JPA）的存储库：

示例11.使用模块特定接口的存储库定义

    interface MyRepository extends JpaRepository<User, Long> { }
    
    @NoRepositoryBean
    interface MyBaseRepository<T, ID extends Serializable> extends JpaRepository<T, ID> {
      …
    }
    
    interface UserRepository extends MyBaseRepository<User, Long> {
      …
    }

`MyRepository`并在其类型层次中进行`UserRepository`扩展`JpaRepository`。它们是Spring Data JPA模块的有效候选者。

以下示例显示使用通用接口的存储库：

示例12.使用通用接口的存储库定义

    interface AmbiguousRepository extends Repository<User, Long> {
     …
    }
    
    @NoRepositoryBean
    interface MyBaseRepository<T, ID extends Serializable> extends CrudRepository<T, ID> {
      …
    }
    
    interface AmbiguousUserRepository extends MyBaseRepository<User, Long> {
      …
    }

`AmbiguousRepository`和`AmbiguousUserRepository`仅延伸`Repository`，并`CrudRepository`在他们的类型层次。虽然在使用独特的Spring Data模块时这非常好，但多个模块无法区分这些存储库应绑定到哪个特定的Spring Data。

以下示例显示了使用带注释的域类的存储库：

示例13.使用带注释的域类的存储库定义

    interface PersonRepository extends Repository<Person, Long> {
     …
    }
    
    @Entity
    class Person {
      …
    }
    
    interface UserRepository extends Repository<User, Long> {
     …
    }
    
    @Document
    class User {
      …
    }

`PersonRepository`引用`Person`，它是用JPA `@Entity`注解注释的，所以这个存储库显然属于Spring Data JPA。`UserRepository`引用`User`，它是用Spring Data MongoDB的`@Document`注解注释的。

以下错误示例显示了使用具有混合注释的域类的存储库：

示例14.使用具有混合注释的域类的存储库定义

    interface JpaPersonRepository extends Repository<Person, Long> {
     …
    }
    
    interface MongoDBPersonRepository extends Repository<Person, Long> {
     …
    }
    
    @Entity
    @Document
    class Person {
      …
    }

此示例显示了使用JPA和Spring Data MongoDB注释的域类。它定义了两个存储库，`JpaPersonRepository`并且`MongoDBPersonRepository`。一个用于JPA，另一个用于MongoDB的使用。Spring Data不再能够区分存储库，导致未定义的行为。

[存储库类型细节](#repositories.multiple-modules.types)和[区分域类注释](#repositories.multiple-modules.annotations)用于严格的存储库配置，以识别特定的Spring Data模块的存储库候选项。可以在相同的域类型上使用多个持久性技术特定的注释，并且允许跨多个持久性技术重用域类型。但是，Spring Data不再可以确定绑定存储库的唯一模块。

区分存储库的最后一种方法是通过确定存储库基础包的范围。基本软件包定义了扫描存储库接口定义的起点，这意味着存储库定义位于相应的软件包中。默认情况下，注释驱动的配置使用配置类的包。[基于XML的配置中](#repositories.create-instances.spring)的[基础包](#repositories.create-instances.spring)是强制性的。

以下示例显示基本包的注释驱动配置：

示例15.基础包的注释驱动配置

    @EnableJpaRepositories(basePackages = "com.acme.repositories.jpa")
    @EnableMongoRepositories(basePackages = "com.acme.repositories.mongo")
    interface Configuration { }

### [](#repositories.query-methods.details)4.4。定义查询方法

存储库代理有两种方法可以从方法名称派生特定于存储的查询：

*   通过直接从方法名称派生查询。
    
*   通过使用手动定义的查询。
    

可用选项取决于实际商店。但是，必须有一个策略来决定创建什么实际查询。下一节介绍可用的选项。

#### [](#repositories.query-methods.query-lookup-strategies)4.4.1。查询查询策略

以下策略可用于存储库基础结构来解析查询。使用XML配置，您可以通过`query-lookup-strategy`属性在名称空间配置策略。对于Java配置，您可以使用注释的`queryLookupStrategy`属性`Enable${store}Repositories`。某些策略可能不支持特定的数据存储。

*   `CREATE`尝试从查询方法名称构造特定于商店的查询。一般的方法是从方法名称中移除一组已知的前缀，并解析该方法的其余部分。您可以在“ [查询创建](#repositories.query-methods.query-creation) ”中阅读有关查询构建的更多信息。
    
*   `USE_DECLARED_QUERY`尝试查找已声明的查询，并在找不到某个查询时引发异常。查询可以通过某处的注释或其他方式声明。查阅特定商店的文档以查找该商店​​的可用选项。如果存储库基础结构在引导时未找到该方法的已声明查询，则会失败。
    
*   `CREATE_IF_NOT_FOUND`（默认）组合`CREATE`和`USE_DECLARED_QUERY`。它首先查找已声明的查询，并且如果未找到已声明的查询，则会创建一个自定义的基于方法名称的查询。这是默认的查找策略，因此，如果您没有明确配置任何内容，就会使用它。它允许通过方法名称进行快速查询定义，还可以根据需要引入已声明的查询来自定义这些查询。
    

#### [](#repositories.query-methods.query-creation)4.4.2。查询创建

构建到Spring Data存储库基础结构中的查询构建器机制对构建存储库实体上的约束查询非常有用。该机制条前缀`find…By`，`read…By`，`query…By`，`count…By`，和`get…By`从所述方法和开始分析它的其余部分。引入子句可以包含更多的表达式，例如`Distinct`在要创建的查询上设置不同的标志。但是，第一个`By`用作分隔符以指示实际标准的开始。在非常基本的层面上，您可以定义实体属性的条件并将它们与`And`和连接起来`Or`。以下示例显示如何创建多个查询：

示例16.从方法名称创建查询

    interface PersonRepository extends Repository<User, Long> {
    
      List<Person> findByEmailAddressAndLastname(EmailAddress emailAddress, String lastname);
    
      // Enables the distinct flag for the query
      List<Person> findDistinctPeopleByLastnameOrFirstname(String lastname, String firstname);
      List<Person> findPeopleDistinctByLastnameOrFirstname(String lastname, String firstname);
    
      // Enabling ignoring case for an individual property
      List<Person> findByLastnameIgnoreCase(String lastname);
      // Enabling ignoring case for all suitable properties
      List<Person> findByLastnameAndFirstnameAllIgnoreCase(String lastname, String firstname);
    
      // Enabling static ORDER BY for a query
      List<Person> findByLastnameOrderByFirstnameAsc(String lastname);
      List<Person> findByLastnameOrderByFirstnameDesc(String lastname);
    }

解析方法的实际结果取决于您为其创建查询的持久性存储。但是，有一些一般事情需要注意：

*   表达式通常是属性遍历和可以连接的运算符。您可以使用组合属性表达式`AND`和`OR`。您还可以得到这样的运营商为支撑`Between`，`LessThan`，`GreaterThan`，和`Like`该属性的表达式。受支持的操作员可能因数据存储而异，因此请参阅相应部分的参考文档。
    
*   方法解析器支持`IgnoreCase`为单个属性（例如，`findByLastnameIgnoreCase(…)`）或支持忽略大小写的类型的所有属性（通常为`String`实例 \- 例如`findByLastnameAndFirstnameAllIgnoreCase(…)`）设置标志。支持忽略情况的方式可能因商店而异，因此请参阅参考文档中的相关部分以获取特定于商店的查询方法。
    
*   您可以通过`OrderBy`向引用属性的查询方法附加子句并提供排序方向（`Asc`或`Desc`）来应用静态排序。要创建支持动态排序的查询方法，请参阅“ [特殊参数处理](#repositories.special-parameters) ”。
    

#### [](#repositories.query-methods.query-property-expressions)4.4.3。属性表达式

属性表达式只能引用被管实体的直接属性，如上例所示。在查询创建时，您已经确保解析的属性是托管域类的属性。但是，您也可以通过遍历嵌套属性来定义约束。考虑以下方法签名：

    List<Person> findByAddressZipCode(ZipCode zipCode);

假设a `Person`有一个`Address`with `ZipCode`。在这种情况下，该方法创建属性遍历`x.address.zipCode`。解析算法首先将整个part（`AddressZipCode`）作为属性进行解释，然后检查该域名是否具有该名称（未添加大小）。如果算法成功，则使用该属性。如果不是的话，该算法将来自右侧的骆驼案件部分的来源拆分为头部和尾部，并尝试找到相应的属性 \- 在我们的示例中`AddressZip`和`Code`。如果算法找到具有该头部的属性，它将采用尾部并从该处继续构建树，然后按照刚刚描述的方式分割尾部。如果第一次分割不匹配，则算法将分割点移到左侧（`Address`，`ZipCode`）并继续。

虽然这应该适用于大多数情况，但算法可能会选择错误的属性。假设这个`Person`类也有一个`addressZip`属性。该算法将在第一轮拆分中匹配，选择错误的属性，并失败（因为`addressZip`可能没有`code`属性的类型）。

为了解决这个歧义，你可以`\_`在你的方法名称中使用手动定义遍历点。所以我们的方法名称如下所示：

    List<Person> findByAddress_ZipCode(ZipCode zipCode);

因为我们将下划线字符视为保留字符，所以我们强烈建议遵循以下标准Java命名约定（即，不使用属性名称中的下划线，而是使用驼峰大小写代替）。

#### [](#repositories.special-parameters)4.4.4。特殊参数处理

要处理查询中的参数，请定义方法参数，如前面的示例中所示。除此之外，基础设施承认某些特定的类型，如`Pageable`和`Sort`，动态地应用分页和排序，以查询。以下示例演示了这些功能：

例子17\. 在查询方法中使用`Pageable`，`Slice`和`Sort`

    Page<User> findByLastname(String lastname, Pageable pageable);
    
    Slice<User> findByLastname(String lastname, Pageable pageable);
    
    List<User> findByLastname(String lastname, Sort sort);
    
    List<User> findByLastname(String lastname, Pageable pageable);

第一种方法可让您将`org.springframework.data.domain.Pageable`实例传递给查询方法，以动态地将分页添加到静态定义的查询中。A `Page`知道可用元素和页面的总数。它通过基础设施触发计数查询来计算总数。由于这可能很昂贵（取决于所使用的商店），您可以返回一个`Slice`。A `Slice`只知道下一个`Slice`是否可用，这在走过更大的结果集时可能足够了。

排序选项也通过`Pageable`实例处理。如果您只需要排序，请`org.springframework.data.domain.Sort`在您的方法中添加一个参数。正如你所看到的，返回`List`也是可能的。在这种情况下，`Page`不会创建构建实际实例所需的附加元数据（这反过来就意味着不会发出本来需要的附加计数查询）。相反，它限制查询只查找给定范围的实体。

要找出您为整个查询获得的页数，您必须触发额外的计数查询。默认情况下，此查询来自您实际触发的查询。

#### [](#repositories.limit-query-result)4.4.5。限制查询结果

查询方法的结果可以通过使用`first`或`top`关键字来限制，这些关键字可以互换使用。一个可选的数值可以附加到`top`或`first`指定要返回的最大结果大小。如果该号码被忽略，则假定结果大小为1。以下示例显示如何限制查询大小：

示例18.使用`Top`和限制查询的结果大小`First`

    User findFirstByOrderByLastnameAsc();
    
    User findTopByOrderByAgeDesc();
    
    Page<User> queryFirst10ByLastname(String lastname, Pageable pageable);
    
    Slice<User> findTop3ByLastname(String lastname, Pageable pageable);
    
    List<User> findFirst10ByLastname(String lastname, Sort sort);
    
    List<User> findTop10ByLastname(String lastname, Pageable pageable);

限制表达式也支持`Distinct`关键字。此外，对于将结果集限制为一个实例的查询，支持将结果封装到`Optional`关键字中。

如果将分页或切片应用于限制查询分页（以及计算可用的页面数量），则将其应用于有限的结果中。

通过使用`Sort`参数限制结果与动态排序结合使用，可以表达“K”最小以及“K”最大元素的查询方法。

#### [](#repositories.query-streaming)4.4.6。流式查询结果

查询方法的结果可以通过使用Java 8 `Stream<T>`作为返回类型来递增处理。而不是将查询结果封装在`Stream`数据存储区中 \- 使用特定的方法来执行流式处理，如以下示例所示：

示例19.使用Java 8对查询的结果进行流式处理 `Stream<T>`

    @Query("select u from User u")
    Stream<User> findAllByCustomQueryAndStream();
    
    Stream<User> readAllByFirstnameNotNull();
    
    @Query("select u from User u")
    Stream<User> streamAllPaged(Pageable pageable);

甲`Stream`潜在包装底层数据存储专用资源，因此必须在使用之后被关闭。您可以`Stream`通过使用该`close()`方法或使用Java 7 `try-with-resources`块手动关闭，如以下示例所示：

示例20.使用`Stream<T>`try-with-resources块中的结果

    try (Stream<User> stream = repository.findAllByCustomQueryAndStream()) {
      stream.forEach(…);
    }

并非所有的Spring Data模块当前都支持`Stream<T>`作为返回类型。

#### [](#repositories.query-async)4.4.7。异步查询结果

通过使用[Spring的异步方法执行功能，](https://docs.spring.io/spring/docs/5.0.6.RELEASE/spring-framework-reference/integration.html#scheduling)可以异步运行存储库查询。这意味着该方法在调用时立即返回，而实际查询执行发生在已提交给Spring的任务中`TaskExecutor`。异步查询执行与反应式查询执行不同，不应混用。有关被动支持的更多详细信息，请参阅商店专用文档。以下示例显示了一些异步查询：

    @Async
    Future<User> findByFirstname(String firstname);               (1)
    
    @Async
    CompletableFuture<User> findOneByFirstname(String firstname); (2)
    
    @Async
    ListenableFuture<User> findOneByLastname(String lastname);    (3)

**1**

使用`java.util.concurrent.Future`作为返回类型。

**2**

使用Java 8 `java.util.concurrent.CompletableFuture`作为返回类型。

**3**

使用a `org.springframework.util.concurrent.ListenableFuture`作为返回类型。

### [](#repositories.create-instances)4.5。创建存储库实例

在本节中，您将为定义的存储库接口创建实例和bean定义。一种方法是使用每个支持存储库机制的Spring Data模块附带的Spring命名空间，尽管我们通常推荐使用Java配置。

#### [](#repositories.create-instances.spring)4.5.1。XML配置

每个Spring Data模块都包含一个`repositories`元素，可让您定义Spring为您扫描的基本包，如以下示例所示：

示例21.通过XML启用Spring Data存储库

    <?xml version="1.0" encoding="UTF-8"?>
    <beans:beans xmlns:beans="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns="http://www.springframework.org/schema/data/jpa"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/data/jpa
        http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">
    
      <repositories base-package="com.acme.repositories" />
    
    </beans:beans>

在前面的例子中，Spring被指示扫描`com.acme.repositories`及其所有子包以查找扩展接口`Repository`或其子接口之一。对于找到的每个接口，基础设施都会注册持久性技术专用的，`FactoryBean`以创建处理调用查询方法的适当代理。每个bean都是在从接口名称派生的bean名称下注册的，因此`UserRepository`将在其下注册一个接口`userRepository`。该`base-package`属性允许使用通配符，以便您可以定义扫描软件包的模式。

##### [](#_using_filters)使用过滤器

默认情况下，基础架构将拾取扩展`Repository`位于已配置基础包下的持久性技术特定子接口的每个接口，并为其创建一个bean实例。但是，您可能需要更细致地控制哪些接口具有为其创建的bean实例。要做到这一点，使用`<include-filter />`和`<exclude-filter />`内部元素`<repositories />`的元素。语义与Spring的上下文命名空间中的元素完全等价。有关详细信息，请参阅这些元素的[Spring参考文档](https://docs.spring.io/spring/docs/5.0.6.RELEASE/spring-framework-reference/core.html#beans-scanning-filters)。

例如，要将某些接口从实例化中排除为存储库Bean，可以使用以下配置：

例22.使用排除过滤器元素

    <repositories base-package="com.acme.repositories">
      <context:exclude-filter type="regex" expression=".*SomeRepository" />
    </repositories>

前面的示例排除了所有以`SomeRepository`实例化结束的接口。

#### [](#repositories.create-instances.java-config)4.5.2。JavaConfig

存储库基础结构也可以通过`@Enable${store}Repositories`在JavaConfig类上使用特定于商店的注释来触发。有关Spring容器的基于Java的配置的介绍，请参阅[Spring参考文档中的JavaConfig](https://docs.spring.io/spring/docs/5.0.6.RELEASE/spring-framework-reference/core.html#beans-java)。

启用S​​pring Data存储库的示例配置类似于以下内容：

示例23.基于示例注释的存储库配置

    @Configuration
    @EnableJpaRepositories("com.acme.repositories")
    class ApplicationConfiguration {
    
      @Bean
      EntityManagerFactory entityManagerFactory() {
        // …
      }
    }

前面的示例使用JPA特定的注释，它将根据您实际使用的商店模块进行更改。这同样适用于`EntityManagerFactory`bean 的定义。请参阅包含特定于商店的配置的章节。

#### [](#repositories.create-instances.standalone)4.5.3。独立使用

您还可以在Spring容器之外使用存储库基础结构 - 例如，在CDI环境中。你的类路径中仍然需要一些Spring库，但是，通常你也可以通过编程来设置库。提供存储库支持的Spring Data模块提供了一个特定`RepositoryFactory`于您可以使用的持久性技术，如下所示：

示例24.存储库工厂的独立使用

    RepositoryFactorySupport factory = … // Instantiate factory here
    UserRepository repository = factory.getRepository(UserRepository.class);

### [](#repositories.custom-implementations)4.6。Spring数据仓库的自定义实现

本节涵盖存储库自定义以及片段如何形成组合存储库。

当查询方法需要不同的行为或无法通过查询派生实现时，则需要提供自定义实现。Spring Data存储库允许您提供自定义存储库代码并将其与通用CRUD抽象和查询方法功能集成。

#### [](#repositories.single-repository-behavior)4.6.1。定制个人存储库

要使用自定义功能丰富存储库，必须首先为自定义功能定义片段接口和实现，如以下示例所示：

示例25.自定义存储库功能的接口

    interface CustomizedUserRepository {
      void someCustomMethod(User user);
    }

然后，您可以让您的存储库接口另外从分段接口扩展，如以下示例所示：

示例26.实现定制存储库功能

    class CustomizedUserRepositoryImpl implements CustomizedUserRepository {
    
      public void someCustomMethod(User user) {
        // Your custom implementation
      }
    }

与片段接口相对应的类名称中最重要的部分是`Impl`后缀。

实现本身不依赖于Spring Data，可以是普通的Spring bean。因此，您可以使用标准的依赖注入行为来向其他bean（例如a `JdbcTemplate`）注入引用，参与方面等等。

您可以让存储库接口扩展片段接口，如以下示例所示：

示例27.对存储库接口的更改

    interface UserRepository extends CrudRepository<User, Long>, CustomizedUserRepository {
    
      // Declare query methods here
    }

使用存储库接口扩展分段接口将CRUD和自定义功能结合起来，并将其提供给客户端。

Spring数据存储库通过使用构成存储库组合的片段来实现。片段是基础知识库，功能方面（如[QueryDsl](#core.extensions.querydsl)）以及自定义接口及其实现。每次将接口添加到存储库接口时，都会通过添加片段来增强组合。每个Spring Data模块提供基础知识库和存储库方面实现。

以下示例显示了自定义接口及其实现：

示例28.碎片及其实现

    interface HumanRepository {
      void someHumanMethod(User user);
    }
    
    class HumanRepositoryImpl implements HumanRepository {
    
      public void someHumanMethod(User user) {
        // Your custom implementation
      }
    }
    
    interface ContactRepository {
    
      void someContactMethod(User user);
    
      User anotherContactMethod(User user);
    }
    
    class ContactRepositoryImpl implements ContactRepository {
    
      public void someContactMethod(User user) {
        // Your custom implementation
      }
    
      public User anotherContactMethod(User user) {
        // Your custom implementation
      }
    }

以下示例显示了扩展自定义存储库的界面`CrudRepository`：

示例29.您的存储库接口的更改

    interface UserRepository extends CrudRepository<User, Long>, HumanRepository, ContactRepository {
    
      // Declare query methods here
    }

存储库可能由多个自定义实现组成，这些自定义实现按其声明的顺序导入。自定义实现具有比基本实现和存储库方面更高的优先级。这种排序使您可以覆盖基本存储库和方面方法，并在两个片段提供相同的方法签名时解决歧义。存储库片段不限于在单个存储库接口中使用。多个存储库可能会使用片段接口，让您可以在不同存储库之间重复使用自定义设置。

以下示例显示了存储库片段及其实现：

例子30.片段覆盖 `save(…)`

    interface CustomizedSave<T> {
      <S extends T> S save(S entity);
    }
    
    class CustomizedSaveImpl<T> implements CustomizedSave<T> {
    
      public <S extends T> S save(S entity) {
        // Your custom implementation
      }
    }

以下示例显示使用上述存储库片段的存储库：

示例31.定制的存储库接口

    interface UserRepository extends CrudRepository<User, Long>, CustomizedSave<User> {
    }
    
    interface PersonRepository extends CrudRepository<Person, Long>, CustomizedSave<Person> {
    }

##### [](#_configuration)组态

如果使用名称空间配置，则存储库基础结构会尝试通过扫描其找到存储库的包下的类来自动检测自定义实施片段。这些类需要遵循将名称空间元素的`repository-impl-postfix`属性附加到分段接口名称的命名约定。这个后缀默认为`Impl`。以下示例显示了使用默认后缀和为后缀设置自定义值的存储库的存储库：

示例32.配置示例

    <repositories base-package="com.acme.repository" />
    
    <repositories base-package="com.acme.repository" repository-impl-postfix="MyPostfix" />

上例中的第一个配置尝试查找调用的类`com.acme.repository.CustomizedUserRepositoryImpl`以充当自定义存储库实现。第二个例子试图查找`com.acme.repository.CustomizedUserRepositoryMyPostfix`。

###### [](#repositories.single-repository-behaviour.ambiguity)解决歧义

如果在不同的包中找到具有匹配类名的多个实现，则Spring Data使用这些bean名来标识要使用哪一个。

鉴于`CustomizedUserRepository`前面所示的以下两个自定义实现，将使用第一个实现。它的bean名称是`customizedUserRepositoryImpl`，它匹配fragment接口（`CustomizedUserRepository`）加上后缀`Impl`。

例子33.解析实现

    package com.acme.impl.one;
    
    class CustomizedUserRepositoryImpl implements CustomizedUserRepository {
    
      // Your custom implementation
    }
    
    package com.acme.impl.two;
    
    @Component("specialCustomImpl")
    class CustomizedUserRepositoryImpl implements CustomizedUserRepository {
    
      // Your custom implementation
    }

如果使用注释`UserRepository`接口`@Component("specialCustom")`，那么bean名称加上，`Impl`然后与为存储库实现定义的名称相匹配`com.acme.impl.two`，并使用它来代替第一个。

###### [](#repositories.manual-wiring)手动接线

如果您的自定义实现仅使用基于注释的配置和自动装配，则上述方法显示效果良好，因为它被视为任何其他Spring bean。如果你的实现片段bean需要特殊的布线，你可以声明这个bean并根据[前面的章节中](#repositories.single-repository-behaviour.ambiguity)描述的约定来命名它。基础架构然后通过名称引用手动定义的bean定义，而不是自己创建一个。以下示例显示如何手动连接自定义实现：

例34.自定义实现的手动连线

    <repositories base-package="com.acme.repository" />
    
    <beans:bean id="userRepositoryImpl" class="…">
      <!-- further configuration -->
    </beans:bean>

#### [](#repositories.customize-base-repository)4.6.2。自定义基础知识库

上[一节中](#repositories.manual-wiring)描述的方法需要在定制基本存储库行为时定制每个存储库接口，以便所有存储库都受到影响。为了改变所有存储库的行为，可以创建一个扩展持久性技术特定存储库基类的实现。然后，该类将作为存储库代理的自定义基类，如以下示例所示：

示例35.定制存储库基类

    class MyRepositoryImpl<T, ID extends Serializable>
      extends SimpleJpaRepository<T, ID> {
    
      private final EntityManager entityManager;
    
      MyRepositoryImpl(JpaEntityInformation entityInformation,
                              EntityManager entityManager) {
        super(entityInformation, entityManager);
    
        // Keep the EntityManager around to used from the newly introduced methods.
        this.entityManager = entityManager;
      }
    
      @Transactional
      public <S extends T> S save(S entity) {
        // implementation goes here
      }
    }

该类需要具有特定于存储库的工厂实现使用的超类的构造函数。如果存储库基类具有多个构造函数，请覆盖采用`EntityInformation`加特定于存储库的基础结构对象（如一个`EntityManager`或模板类）的构造函数。

最后一步是让Spring Data基础设施知道定制的存储库基类。在Java配置中，您可以使用注释的`repositoryBaseClass`属性来完成此操作`@Enable${store}Repositories`，如以下示例所示：

示例36.使用JavaConfig配置定制存储库基类

    @Configuration
    @EnableJpaRepositories(repositoryBaseClass = MyRepositoryImpl.class)
    class ApplicationConfiguration { … }

XML名称空间中提供了相应的属性，如以下示例所示：

示例37.使用XML配置定制存储库基类

    <repositories base-package="com.acme.repository"
         base-class="….MyRepositoryImpl" />

### [](#core.domain-events)4.7。从聚合根发布事件

由存储库管理的实体是聚合根。在Domain-Driven Design应用程序中，这些聚合根通常会发布域事件。Spring Data提供了一个注释，称为`@DomainEvents`可用于聚合根方法的注释，以使该出版物尽可能地简单，如以下示例所示：

例子38.从聚合根暴露域事件

    class AnAggregateRoot {
    
        @DomainEvents (1)
        Collection<Object> domainEvents() {
            // … return events you want to get published here
        }
    
        @AfterDomainEventPublication (2)
        void callbackMethod() {
           // … potentially clean up domain events list
        }
    }

**1**

使用该方法`@DomainEvents`可以返回单个事件实例或事件集合。它不能有任何争论。

**2**

所有事件发布后，我们都有注解的方法`@AfterDomainEventPublication`。它可用于潜在地清理要发布的事件列表（以及其他用途）。

每次调用Spring Data存储库的`save(…)`方法时，都会调用这些方法。

### [](#core.extensions)4.8。Spring数据扩展

本部分记录了一组Spring数据扩展，这些扩展使Spring Data在各种环境下的使用成为可能。目前，大部分的整合都是针对Spring MVC。

#### [](#core.extensions.querydsl)4.8.1。Querydsl扩展

[Querydsl](http://www.querydsl.com/)是一个框架，可以通过其流畅的API构建静态类型的SQL式查询。

几个Spring数据模块提供了与Querydsl的集成`QuerydslPredicateExecutor`，如以下示例所示：

例子39\. QuerydslPredicateExecutor接口

    public interface QuerydslPredicateExecutor<T> {
    
      Optional<T> findById(Predicate predicate);  (1)
    
      Iterable<T> findAll(Predicate predicate);   (2)
    
      long count(Predicate predicate);            (3)
    
      boolean exists(Predicate predicate);        (4)
    
      // … more functionality omitted.
    }

**1**

查找并返回与之匹配的单个实体`Predicate`。

**2**

查找并返回与之匹配的所有实体`Predicate`。

**3**

返回匹配的实体数量`Predicate`。

**4**

返回是否`Predicate`存在匹配的实体。

要使用Querydsl支持，请`QuerydslPredicateExecutor`在存储库接口上进行扩展，如以下示例所示

示例40.存储库上的Querydsl集成

    interface UserRepository extends CrudRepository<User, Long>, QuerydslPredicateExecutor<User> {
    }

前面的示例允许您使用Querydsl `Predicate`实例编写类型安全查询，如以下示例中所示：

    Predicate predicate = user.firstname.equalsIgnoreCase("dave")
        .and(user.lastname.startsWithIgnoreCase("mathews"));
    
    userRepository.findAll(predicate);

#### [](#core.web)4.8.2。Web支持

本节包含Spring Data Web支持的文档，因为它在Spring Data Commons的当前（及更高版本）中实现。由于新引入的支持改变了很多东西，因此我们在[
web.legacy
中](#web.legacy)保留了以前行为的文档。

支持存储库编程模型的Spring Data模块提供各种Web支持。Web相关组件需要将Spring MVC JAR放在类路径中。其中一些甚至提供与[Spring HATEOAS的](https://github.com/SpringSource/spring-hateoas)集成。通常，通过`@EnableSpringDataWebSupport`在JavaConfig配置类中使用注释来启用集成支持，如以下示例所示：

示例41.启用Spring Data Web支持

    @Configuration
    @EnableWebMvc
    @EnableSpringDataWebSupport
    class WebConfiguration {}

该`@EnableSpringDataWebSupport`批注注册几个组件，我们将在一个位讨论。它也会在类路径中检测到Spring HATEOAS，并为其注册集成组件。

另外，如果你使用XML配置，注册一个`SpringDataWebConfiguration`或者`HateoasAwareSpringDataWebConfiguration`作为Spring bean，如下例（for `SpringDataWebConfiguration`）所示：

例子42.在XML中启用Spring Data web支持

    <bean class="org.springframework.data.web.config.SpringDataWebConfiguration" />
    
    <!-- If you use Spring HATEOAS, register this one *instead* of the former -->
    <bean class="org.springframework.data.web.config.HateoasAwareSpringDataWebConfiguration" />

##### [](#core.web.basic)基本的Web支持

[上一节中](#core.web)显示的配置注册了一些基本组件：

*   A [`DomainClassConverter`](#core.web.basic.domain-class-converter)让Spring MVC从请求参数或路径变量中解析由存储库管理的域类的实例。
    
*   [`HandlerMethodArgumentResolver`](#core.web.basic.paging-and-sorting)实现让Spring MVC的决心`Pageable`和`Sort`实例从请求参数。
    

###### [](#core.web.basic.domain-class-converter)`DomainClassConverter`

将`DomainClassConverter`让你在Spring MVC中的控制器方法签名使用域类型直接，让你不用通过储存手动查找的情况下，如在下面的例子：

例子43.在方法签名中使用域类型的Spring MVC控制器

    @Controller
    @RequestMapping("/users")
    class UserController {
    
      @RequestMapping("/{id}")
      String showUserForm(@PathVariable("id") User user, Model model) {
    
        model.addAttribute("user", user);
        return "userForm";
      }
    }

如您所见，该方法`User`直接接收实例，不需要进一步查找。通过让Spring MVC首先将路径变量转换为`id`域类的类型，并最终通过调用`findById(…)`为域类型注册的存储库实例来访问实例，可以解决该实例。

目前，存储库必须实施`CrudRepository`才有资格被发现以进行转换。

###### [](#core.web.basic.paging-and-sorting)用于Pageable和Sort的HandlerMethodArgumentResolvers

[上一节中](#core.web.basic.domain-class-converter)显示的配置代码片段也会注册一个`PageableHandlerMethodArgumentResolver`以及一个实例`SortHandlerMethodArgumentResolver`。注册启用`Pageable`并`Sort`作为有效的控制器方法参数，如以下示例所示：

示例44.使用Pageable作为控制器方法参数

    @Controller
    @RequestMapping("/users")
    class UserController {
    
      private final UserRepository repository;
    
      UserController(UserRepository repository) {
        this.repository = repository;
      }
    
      @RequestMapping
      String showUsers(Model model, Pageable pageable) {
    
        model.addAttribute("users", repository.findAll(pageable));
        return "users";
      }
    }

前面的方法签名会导致Spring MVC尝试`Pageable`使用以下默认配置从请求参数派生实例：

表1.针对`Pageable`实例评估的请求参数  

`page`

您想要检索的页面。0索引，默认为0。

`size`

您要检索的页面大小。默认为20。

`sort`

应该按格式排序的属性`property,property(,ASC|DESC)`。默认排序方向是升序。`sort`如果您想切换方向，请使用多个参数 \- 例如`?sort=firstname&sort=lastname,asc`。

要定制这种行为，分别注册实现`PageableHandlerMethodArgumentResolverCustomizer`接口或`SortHandlerMethodArgumentResolverCustomizer`接口的bean 。它的`customize()`方法被调用，让你改变设置，如下例所示：

    @Bean SortHandlerMethodArgumentResolverCustomizer sortCustomizer() {
        return s -> s.setPropertyDelimiter("<-->");
    }

如果设置现有属性`MethodArgumentResolver`不足以达到您的目的，请扩展其中一个`SpringDataWebConfiguration`或启用HATEOAS的等效项，覆盖`pageableResolver()`或`sortResolver()`方法，然后导入您的自定义配置文件，而不是使用`@Enable`注释。

如果您需要从请求中解析多个`Pageable`或`Sort`实例（例如，针对多个表），则可以使用Spring的`@Qualifier`注释区分一个。然后请求参数必须以前缀`${qualifier}_`。以下示例显示了生成的方法签名：

    String showUsers(Model model,
          @Qualifier("thing1") Pageable first,
          @Qualifier("thing2") Pageable second) { … }

你有填充`thing1_page`和`thing2_page`等。

`Pageable`传递给方法的默认值等于a，`new PageRequest(0, 20)`但可以使用参数`@PageableDefault`上的注释进行自定义`Pageable`。

##### [](#core.web.pageables)超媒体支持Pageables

Spring HATEOAS附带一个表示模型class（`PagedResources`），它允许`Page`使用必要的`Page`元数据丰富实例的内容以及让客户端轻松导航页面的链接。将页面转换为a `PagedResources`由Spring HATEOAS `ResourceAssembler`接口的实现完成，该接口称为`PagedResourcesAssembler`。以下示例显示如何使用a `PagedResourcesAssembler`作为控制器方法参数：

示例45.使用PagedResourcesAssembler作为控制器方法参数

    @Controller
    class PersonController {
    
      @Autowired PersonRepository repository;
    
      @RequestMapping(value = "/persons", method = RequestMethod.GET)
      HttpEntity<PagedResources<Person>> persons(Pageable pageable,
        PagedResourcesAssembler assembler) {
    
        Page<Person> persons = repository.findAll(pageable);
        return new ResponseEntity<>(assembler.toResources(persons), HttpStatus.OK);
      }
    }

如上例所示启用配置，可以将`PagedResourcesAssembler`其用作控制器方法参数。调用`toResources(…)`它有以下效果：

*   该内容`Page`成为该`PagedResources`实例的内容。
    
*   该`PagedResources`对象获得一个`PageMetadata`附加的实例，并使用来自`Page`和底层的信息填充该对象`PageRequest`。
    
*   将`PagedResources`可能会`prev`和`next`连接链路，根据页面的状态。链接指向方法映射到的URI。添加到该方法中的分页参数与该设置相匹配，`PageableHandlerMethodArgumentResolver`以确保以后可以解析链接。
    

假设我们在数据库中有30个Person实例。您现在可以触发请求（）并查看与以下内容类似的输出：`GET [http://localhost:8080/persons](http://localhost:8080/persons)`

    { "links" : [ { "rel" : "next",
                    "href" : "http://localhost:8080/persons?page=1&size=20 }
      ],
      "content" : [
         … // 20 Person instances rendered here
      ],
      "pageMetadata" : {
        "size" : 20,
        "totalElements" : 30,
        "totalPages" : 2,
        "number" : 0
      }
    }

您会看到汇编程序生成了正确的URI，并且还选取了缺省配置将参数解析`Pageable`为一个即将到来的请求。这意味着，如果您更改该配置，链接将自动遵守更改。默认情况下，汇编程序指向它所调用的控制器方法，但可以通过交付自定义`Link`来作为基础来构建分页链接，从而重载该`PagedResourcesAssembler.toResource(…)`方法。

##### [](#core.web.binding)Web数据绑定支持

通过使用[JSONPath](http://goessner.net/articles/JsonPath/)表达式（需要[Jayway JsonPath](https://github.com/json-path/JsonPath)或[XPath](https://www.w3.org/TR/xpath-31/)表达式（需要[XmlBeam](https://xmlbeam.org/)）），Spring数据投影（在[Projections](#projections)中进行了介绍）可用于绑定传入的请求负载，如以下示例所示：[](http://goessner.net/articles/JsonPath/)[](https://github.com/json-path/JsonPath)[](https://www.w3.org/TR/xpath-31/)[](https://xmlbeam.org/)

示例46.使用JSONPath或XPath表达式的HTTP负载绑定

    @ProjectedPayload
    public interface UserPayload {
    
      @XBRead("//firstname")
      @JsonPath("$..firstname")
      String getFirstname();
    
      @XBRead("/lastname")
      @JsonPath({ "$.lastname", "$.user.lastname" })
      String getLastname();
    }

上例中显示的类型可以用作Spring MVC处理方法参数，或者通过使用`ParameterizedTypeReference`其中一个`RestTemplate`方法。前面的方法声明将尝试`firstname`在给定文档中的任何位置查找。该`lastname`XML查询是对输入文档的顶层进行。它的JSON变体`lastname`首先尝试顶层，但如果前一层没有返回值，也会尝试`lastname`嵌套在`user`子文档中。这样，源文档结构的变化可以轻松地被缓解，而无需客户端调用公开的方法（通常是基于类的有效载荷绑定的缺点）。

如投影中所述支持嵌套[投影](#projections)。如果该方法返回一个复杂的非接口类型，`ObjectMapper`则使用Jackson 来映射最终值。

对于Spring MVC，必要的转换器一旦`@EnableSpringDataWebSupport`处于活动状态就会自动注册，并且所需的依赖关系在类路径中可用。用于`RestTemplate`，注册`ProjectingJackson2HttpMessageConverter`（JSON）或`XmlBeamHttpMessageConverter`手动。

有关更多信息，请参阅规范的[Spring Data Examples存储库中](https://github.com/spring-projects/spring-data-examples)的[web投影示例](https://github.com/spring-projects/spring-data-examples/tree/master/web/projection)。[](https://github.com/spring-projects/spring-data-examples)

##### [](#core.web.type-safe)Querydsl Web支持

对于具有[QueryDSL](http://www.querydsl.com/)集成的商店，可以从包含在`Request`查询字符串中的属性派生查询。

考虑以下查询字符串：

    ?firstname=Dave&lastname=Matthews

给定`User`前面例子中的对象，查询字符串可以通过使用`QuerydslPredicateArgumentResolver`。解析为下列值。

    QUser.user.firstname.eq("Dave").and(QUser.user.lastname.eq("Matthews"))

该功能会自动启用，以及`@EnableSpringDataWebSupport`在类路径中找到Querydsl时。

向`@QuerydslPredicate`方法签名中添加a 提供了一个`Predicate`可立即使用的方法，可以使用该方法运行`QuerydslPredicateExecutor`。

类型信息通常从方法的返回类型中解析出来。由于该信息不一定与域类型匹配，因此使用该`root`属性可能是一个好主意`QuerydslPredicate`。

以下示例显示了如何`@QuerydslPredicate`在方法签名中使用：

    @Controller
    class UserController {
    
      @Autowired UserRepository repository;
    
      @RequestMapping(value = "/", method = RequestMethod.GET)
      String index(Model model, @QuerydslPredicate(root = User.class) Predicate predicate,    (1)
              Pageable pageable, @RequestParam MultiValueMap<String, String> parameters) {
    
        model.addAttribute("users", repository.findAll(predicate, pageable));
    
        return "index";
      }
    }

**1**

解析查询字符串参数匹配`Predicate`的`User`。

默认绑定如下：

*   `Object`在简单的属性上`eq`。
    
*   `Object`关于集合像属性一样`contains`。
    
*   `Collection`在简单的属性上`in`。
    

这些绑定可以通过Java 8 的`bindings`属性`@QuerydslPredicate`或通过使用Java 8 `default methods`并将该`QuerydslBinderCustomizer`方法添加到存储库接口来定制。

    interface UserRepository extends CrudRepository<User, String>,
                                     QuerydslPredicateExecutor<User>,                (1)
                                     QuerydslBinderCustomizer<QUser> {               (2)
    
      @Override
      default void customize(QuerydslBindings bindings, QUser user) {
    
        bindings.bind(user.username).first((path, value) -> path.contains(value))    (3)
        bindings.bind(String.class)
          .first((StringPath path, String value) -> path.containsIgnoreCase(value)); (4)
        bindings.excluding(user.password);                                           (5)
      }
    }

**1**

`QuerydslPredicateExecutor`提供对特定查找方法的访问`Predicate`。

**2**

`QuerydslBinderCustomizer`在仓库界面上定义的是自动拾取和快捷方式`@QuerydslPredicate(bindings=…​)`。

**3**

将该`username`属性的绑定定义为简单`contains`绑定。

**4**

将`String`属性的默认绑定定义为不区分大小写的`contains`匹配。

**五**

`password`从`Predicate`解决方案中排除财产。

#### [](#core.repository-populators)4.8.3。存储库Poppop

如果您使用Spring JDBC模块，那么您可能很熟悉`DataSource`使用SQL脚本填充的支持。尽管存储库级别没有使用SQL作为数据定义语言，但类似的抽象是可用的，因为它必须是独立于存储的。因此，populators支持XML（通过Spring的OXM抽象）和JSON（通过Jackson）来定义数据来填充存储库。

假设您拥有`data.json`包含以下内容的文件：

例子47.在JSON中定义的数据

    [ { "_class" : "com.acme.Person",
     "firstname" : "Dave",
      "lastname" : "Matthews" },
      { "_class" : "com.acme.Person",
     "firstname" : "Carter",
      "lastname" : "Beauford" } ]

您可以使用Spring Data Commons中提供的存储库名称空间的populator元素来填充存储库。要将前面的数据填充到PersonRepository中，请声明类似于以下内容的populator：

示例48.声明Jackson存储库加载器

    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:repository="http://www.springframework.org/schema/data/repository"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/data/repository
        http://www.springframework.org/schema/data/repository/spring-repository.xsd">
    
      <repository:jackson2-populator locations="classpath:data.json" />
    
    </beans>

前面的声明导致`data.json`文件被Jackson读取和反序列化`ObjectMapper`。

通过检查`\_class`JSON文档的属性来确定JSON对象被解组的类型。基础结构最终选择适当的存储库来处理反序列化的对象。

要改为使用XML定义存储库应该填充的数据，可以使用该`unmarshaller-populator`元素。您将其配置为使用Spring OXM中提供的XML编组器之一。有关详细信息，请参阅[Spring参考文档](https://docs.spring.io/spring/docs/5.0.6.RELEASE/spring-framework-reference/data-access.html#oxm)。以下示例显示如何使用JAXB解组存储器加载器：

例49.声明一个反编组存储器加载器（使用JAXB）

    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:repository="http://www.springframework.org/schema/data/repository"
      xmlns:oxm="http://www.springframework.org/schema/oxm"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/data/repository
        http://www.springframework.org/schema/data/repository/spring-repository.xsd
        http://www.springframework.org/schema/oxm
        http://www.springframework.org/schema/oxm/spring-oxm.xsd">
    
      <repository:unmarshaller-populator locations="classpath:data.json"
        unmarshaller-ref="unmarshaller" />
    
      <oxm:jaxb2-marshaller contextPath="com.acme" />
    
    </beans>

[](#reference)参考文档
==================

[](#jpa.repositories)5\. JPA存储库
-------------------------------

本章指出了JPA存储库支持的特点。这基于“ [使用Spring数据存储库](#repositories) ”中介绍的核心存储库支持。确保你对这里解释的基本概念有充分的理解。

### [](#jpa.introduction)5.1。介绍

本节通过以下任一介绍了配置Spring Data JPA的基础知识：

*   “ [Spring命名空间](#jpa.namespace) ”（XML配置）
    
*   “ [基于注释的配置](#jpa.java-config) ”（Java配置）
    

#### [](#jpa.namespace)5.1.1。Spring命名空间

Spring Data的JPA模块包含一个允许定义存储库bean的自定义名称空间。它还包含特定于JPA的某些功能和元素属性。通常，可以使用该`repositories`元素来设置JPA存储库，如以下示例所示：

示例50.使用名称空间设置JPA存储库

    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:jpa="http://www.springframework.org/schema/data/jpa"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/data/jpa
        http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">
    
      <jpa:repositories base-package="com.acme.repositories" />
    
    </beans>

使用该`repositories`元素查找Spring Data存储库，如“ [创建存储库实例](#repositories.create-instances) ”中所述。除此之外，它还为所有注释的bean激活持久性异常转换`@Repository`，让JPA持久性提供者抛出的异常转换为Spring的`DataAccessException`层次结构。

##### [](#_custom_namespace_attributes)自定义命名空间属性

除了`repositories`元素的默认属性外，JPA命名空间还提供了额外的属性，让您可以更加详细地控制存储库的设置：

表2\. `repositories`元素的自定义JPA特定属性  

`entity-manager-factory-ref`

显式`EntityManagerFactory`地将要与`repositories`元素检测到的存储库配合使用。通常`EntityManagerFactory`在应用程序中使用多个bean时使用。如果未配置，春数据自动查找了`EntityManagerFactory`名为豆`entityManagerFactory`中`ApplicationContext`。

`transaction-manager-ref`

显式`PlatformTransactionManager`地将要与`repositories`元素检测到的存储库配合使用。通常只有`EntityManagerFactory`在配置了多个事务管理器或bean 时才需要。默认为`PlatformTransactionManager`在当前内部定义的单个`ApplicationContext`。

如果没有明确的定义， Spring Data JPA需要一个`PlatformTransactionManager`名为bean的bean 。 `transactionManager``transaction-manager-ref`

#### [](#jpa.java-config)5.1.2。基于注释的配置

Spring Data JPA存储库支持不仅可以通过XML命名空间激活，还可以通过使用JavaConfig注释来激活，如以下示例所示：

例子51\. Spring Data JPA存储库使用JavaConfig

    @Configuration
    @EnableJpaRepositories
    @EnableTransactionManagement
    class ApplicationConfig {
    
      @Bean
      public DataSource dataSource() {
    
        EmbeddedDatabaseBuilder builder = new EmbeddedDatabaseBuilder();
        return builder.setType(EmbeddedDatabaseType.HSQL).build();
      }
    
      @Bean
      public LocalContainerEntityManagerFactoryBean entityManagerFactory() {
    
        HibernateJpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
        vendorAdapter.setGenerateDdl(true);
    
        LocalContainerEntityManagerFactoryBean factory = new LocalContainerEntityManagerFactoryBean();
        factory.setJpaVendorAdapter(vendorAdapter);
        factory.setPackagesToScan("com.acme.domain");
        factory.setDataSource(dataSource());
        return factory;
      }
    
      @Bean
      public PlatformTransactionManager transactionManager(EntityManagerFactory entityManagerFactory) {
    
        JpaTransactionManager txManager = new JpaTransactionManager();
        txManager.setEntityManagerFactory(entityManagerFactory);
        return txManager;
      }
    }

您必须创建`LocalContainerEntityManagerFactoryBean`而不是`EntityManagerFactory`直接创建，因为除创建之外，前者还参与异常转换机制`EntityManagerFactory`。

上面的配置类使用`EmbeddedDatabaseBuilder`API的设置嵌入式HSQL数据库`spring-jdbc`。Spring Data然后设置一个`EntityManagerFactory`并使用Hibernate作为示例持久性提供者。这里声明的最后一个基础结构组件是`JpaTransactionManager`。最后，该示例通过使用`@EnableJpaRepositories`注释来激活Spring Data JPA存储库，注释本质上与XML名称空间具有相同的属性。如果没有配置基础软件包，则使用配置类所在的软件包。

### [](#jpa.entity-persistence)5.2。坚持实体

本节介绍如何使用Spring Data JPA持久（保存）实体。

#### [](#jpa.entity-persistence.saving-entites)5.2.1。保存实体

保存实体可以使用该`CrudRepository.save(…)`方法执行。它通过使用底层JPA来坚持或合并给定的实体`EntityManager`。如果实体还没有被保存，Spring Data JPA会通过调用该`entityManager.persist(…)`方法来保存该实体。否则，它会调用该`entityManager.merge(…)`方法。

##### [](#_entity_state_detection_strategies)实体状态检测策略

Spring Data JPA提供了以下策略来检测实体是否是新的：

*   Id-属性检查（**默认**）：默认情况下，Spring Data JPA检查给定实体的标识属性。如果标识符属性是`null`，则该实体被假定为新的。否则，它被认为不是新的。
    
*   实现`Persistable`：如果实体实现`Persistable`，Spring Data JPA将新检测委托给`isNew(…)`实体的方法。有关详细信息，请参阅[JavaDoc](https://docs.spring.io/spring-data/data-commons/docs/current/api/index.html?org/springframework/data/domain/Persistable.html)。
    
*   实现`EntityInformation`：您可以通过创建子类并相应地重写该方法来自定义实现中`EntityInformation`使用的抽象。然后您必须将自定义实现注册为Spring bean。请注意，这应该很少有必要。有关详细信息，请参阅[JavaDoc](https://docs.spring.io/spring-data/data-jpa/docs/current/api/index.html?org/springframework/data/jpa/repository/support/JpaRepositoryFactory.html)。`SimpleJpaRepository``JpaRepositoryFactory``getEntityInformation(…)``JpaRepositoryFactory`[](https://docs.spring.io/spring-data/data-jpa/docs/current/api/index.html?org/springframework/data/jpa/repository/support/JpaRepositoryFactory.html)
    

### [](#jpa.query-methods)5.3。查询方法

本节介绍使用Spring Data JPA创建查询的各种方法。

#### [](#jpa.sample-app.finders.strategies)5.3.1。查询查询策略

JPA模块支持手动将查询定义为字符串或从方法名称派生。

##### [](#_declared_queries)宣布的查询

尽管获取从方法名派生的查询非常方便，但可能会遇到这样的情况，即方法名解析器不支持要使用的关键字，或者方法名称会不必要地变得难看。所以，你可以通过命名约定使用JPA命名查询（请参阅[使用JPA命名查询](#jpa.query-methods.named-queries)了解更多信息）或相当具有注解你的查询方法`@Query`（请参阅[使用`@Query`](#jpa.query-methods.at-query)的详细信息）。

#### [](#jpa.query-methods.query-creation)5.3.2。查询创建

通常，JPA的查询创建机制按“ [查询方法](#repositories.query-methods) ”中的描述工作。以下示例显示了JPA查询方法转换为的内容：

示例52.从方法名称创建查询

公共接口UserRepository扩展了Repository <User，Long> {
 List <User> findByEmailAddressAndLastname（String emailAddress，String lastname）; }

我们使用JPA标准API从这个创建了一个查询，但实际上，这转换成以下查询：`select u from User u where u.emailAddress = ?1 and u.lastname = ?2`。Spring Data JPA执行属性检查并遍历嵌套属性，如“ [属性表达式](#repositories.query-methods.query-property-expressions) ”中所述。

下表描述了JPA支持的关键字以及包含该关键字的方法转换为：

表3.方法名称中支持的关键字  

关键词

样品

JPQL片段

`And`

`findByLastnameAndFirstname`

`… where x.lastname = ?1 and x.firstname = ?2`

`Or`

`findByLastnameOrFirstname`

`… where x.lastname = ?1 or x.firstname = ?2`

`Is,Equals`

`findByFirstname`，`findByFirstnameIs`，`findByFirstnameEquals`

`… where x.firstname = ?1`

`Between`

`findByStartDateBetween`

`… where x.startDate between ?1 and ?2`

`LessThan`

`findByAgeLessThan`

`… where x.age < ?1`

`LessThanEqual`

`findByAgeLessThanEqual`

`… where x.age <= ?1`

`GreaterThan`

`findByAgeGreaterThan`

`… where x.age > ?1`

`GreaterThanEqual`

`findByAgeGreaterThanEqual`

`… where x.age >= ?1`

`After`

`findByStartDateAfter`

`… where x.startDate > ?1`

`Before`

`findByStartDateBefore`

`… where x.startDate < ?1`

`IsNull`

`findByAgeIsNull`

`… where x.age is null`

`IsNotNull,NotNull`

`findByAge(Is)NotNull`

`… where x.age not null`

`Like`

`findByFirstnameLike`

`… where x.firstname like ?1`

`NotLike`

`findByFirstnameNotLike`

`… where x.firstname not like ?1`

`StartingWith`

`findByFirstnameStartingWith`

`… where x.firstname like ?1`（参数绑定附加`%`）

`EndingWith`

`findByFirstnameEndingWith`

`… where x.firstname like ?1`（参数与预先绑定`%`）

`Containing`

`findByFirstnameContaining`

`… where x.firstname like ?1`（参数绑定`%`）

`OrderBy`

`findByAgeOrderByLastnameDesc`

`… where x.age = ?1 order by x.lastname desc`

`Not`

`findByLastnameNot`

`… where x.lastname <> ?1`

`In`

`findByAgeIn(Collection<Age> ages)`

`… where x.age in ?1`

`NotIn`

`findByAgeNotIn(Collection<Age> ages)`

`… where x.age not in ?1`

`True`

`findByActiveTrue()`

`… where x.active = true`

`False`

`findByActiveFalse()`

`… where x.active = false`

`IgnoreCase`

`findByFirstnameIgnoreCase`

`… where UPPER(x.firstame) = UPPER(?1)`

`In`并且`NotIn`还可以将任何子类`Collection`作为参数以及数组或可变参数。对于同一逻辑运算符的其他语法版本，请选中“ [存储库查询关键字](#repository-query-keywords) ”。

#### [](#jpa.query-methods.named-queries)5.3.3。使用JPA命名查询

这些示例使用`<named-query />`元素和`@NamedQuery`注释。这些配置元素的查询必须在JPA查询语言中定义。当然，你可以使用`<named-native-query />`或`@NamedNativeQuery`过。通过这些元素，您可以通过失去数据库平台独立性来在本机SQL中定义查询。

##### [](#_xml_named_query_definition)XML命名查询定义

要使用XML配置，请将必要的`<named-query />`元素添加到`orm.xml`位于`META-INF`类路径文件夹中的JPA配置文件中。自动调用命名查询是通过使用某种已定义的命名约定来启用的。有关更多详情，请参阅下文。

例53\. XML命名查询配置

    <named-query name="User.findByLastname">
      <query>select u from User u where u.lastname = ?1</query>
    </named-query>

该查询有一个特殊名称，用于在运行时解析它。

##### [](#_annotation_based_configuration)基于注释的配置

基于注解的配置具有不需要编辑另一个配置文件的优点，降低了维护工作量。您需要为每个新的查询声明重新编译您的域类，从而为此付出代价。

示例54.基于注释的命名查询配置

    @Entity
    @NamedQuery(name = "User.findByEmailAddress",
      query = "select u from User u where u.emailAddress = ?1")
    public class User {
    
    }

##### [](#_declaring_interfaces)声明接口

要允许执行这些命名查询，请指定`UserRepository`如下：

示例55\. UserRepository中的查询方法声明

    public interface UserRepository extends JpaRepository<User, Long> {
    
      List<User> findByLastname(String lastname);
    
      User findByEmailAddress(String emailAddress);
    }

Spring Data尝试将对这些方法的调用解析为命名查询，从配置的域类的简单名称开始，接着用点分隔方法名称。因此，前面的示例将使用examlpe中定义的命名查询，而不是尝试从方法名称创建查询。

#### [](#jpa.query-methods.at-query)5.3.4。运用`@Query`

使用命名查询来声明实体查询是一种有效的方法，对于少量查询来说工作正常。由于查询本身与执行它们的Java方法绑定，因此可以通过使用Spring Data JPA `@Query`注释直接绑定它们，而不是将它们注释到域类。这将持久性特定信息从域类中释放出来，并将查询共同定位到存储库接口。

查询注释到查询方法的查询优先于使用`@NamedQuery`或声明的查询定义的查询`orm.xml`。

以下示例显示了使用`@Query`注释创建的查询：

例56.使用查询方法声明查询 `@Query`

    public interface UserRepository extends JpaRepository<User, Long> {
    
      @Query("select u from User u where u.emailAddress = ?1")
      User findByEmailAddress(String emailAddress);
    }

##### [](#_using_advanced_code_like_code_expressions)使用高级`LIKE`表达式

创建的手动定义查询的查询执行机制`@Query`允许`LIKE`在查询定义内定义高级表达式，如以下示例所示：

例子57\. `like`@Query中的高级表达式

    public interface UserRepository extends JpaRepository<User, Long> {
    
      @Query("select u from User u where u.firstname like %?1")
      List<User> findByFirstnameEndsWith(String firstname);
    }

在前面的示例中，可以识别`LIKE`分隔符（`%`），并将查询转换为有效的JPQL查询（删除`%`）。在查询执行后，传递给方法调用的参数将获得先前识别的`LIKE`模式的增强。

##### [](#_native_queries)原生查询

该`@Query`注释允许通过设定运行的原生查询`nativeQuery`标志设置为true，如图以下示例：

示例58.使用@Query在查询方法中声明本机查询

    public interface UserRepository extends JpaRepository<User, Long> {
    
      @Query(value = "SELECT * FROM USERS WHERE EMAIL_ADDRESS = ?1", nativeQuery = true)
      User findByEmailAddress(String emailAddress);
    }

Spring Data JPA当前不支持对本机查询进行动态排序，因为它必须处理已声明的实际查询，对于本机SQL而言，它无法可靠地进行操作。但是，您可以通过自己指定计数查询来使用本机查询进行分页，如以下示例所示：

示例59.通过使用，在查询方法中声明本机计数查询以进行分页 `@Query`

    public interface UserRepository extends JpaRepository<User, Long> {
    
      @Query(value = "SELECT * FROM USERS WHERE LASTNAME = ?1",
        countQuery = "SELECT count(*) FROM USERS WHERE LASTNAME = ?1",
        nativeQuery = true)
      Page<User> findByLastname(String lastname, Pageable pageable);
    }

通过将`.count`后缀添加到查询副本中，类似的方法也适用于命名的本机查询。不过，您可能需要为计数查询注册结果集映射。

#### [](#jpa.query-methods.sorting)5.3.5。使用排序

排序可以通过提供`PageRequest`或`Sort`直接使用来完成。`Order`实例中实际使用的属性`Sort`需要与您的域模型匹配，这意味着它们需要解析为查询中使用的属性或别名。JPQL将其定义为状态字段路径表达式。

使用任何不可引用的路径表达式会导致一个`Exception`。

但是，`Sort`一起使用[`@Query`](#jpa.query-methods.at-query)可以让您潜入`Order`包含`ORDER BY`子句中的函数的未经路径检查的实例中。这是可能的，因为`Order`它附加到给定的查询字符串。默认情况下，Spring Data JPA拒绝`Order`包含函数调用的任何实例，但可以`JpaSort.unsafe`用来添加潜在的不安全排序。

以下示例使用`Sort`和`JpaSort`，包括一个不安全的选项`JpaSort`：

例子60.使用`Sort`和`JpaSort`

    public interface UserRepository extends JpaRepository<User, Long> {
    
      @Query("select u from User u where u.lastname like ?1%")
      List<User> findByAndSort(String lastname, Sort sort);
    
      @Query("select u.id, LENGTH(u.firstname) as fn_len from User u where u.lastname like ?1%")
      List<Object[]> findByAsArrayAndSort(String lastname, Sort sort);
    }
    
    repo.findByAndSort("lannister", new Sort("firstname"));               (1)
    repo.findByAndSort("stark", new Sort("LENGTH(firstname)"));           (2)
    repo.findByAndSort("targaryen", JpaSort.unsafe("LENGTH(firstname)")); (3)
    repo.findByAsArrayAndSort("bolton", new Sort("fn_len"));              (4)

**1**

有效`Sort`表达式指向域模型中的属性。

**2**

无效的`Sort`包含函数调用。例外。

**3**

`Sort`包含明确_不安全的_ 有效`Order`。

**4**

`Sort`指向别名函数的有效表达式。

#### [](#jpa.named-parameters)5.3.6。使用命名参数

默认情况下，Spring Data JPA使用基于位置的参数绑定，如前面所有示例中所述。当对参数位置进行重构时，这使得查询方法有点容易出错。要解决此问题，可以使用`@Param`注释为方法参数提供具体名称，并在查询中绑定名称，如以下示例中所示：

例子61.使用命名参数

    public interface UserRepository extends JpaRepository<User, Long> {
    
      @Query("select u from User u where u.firstname = :firstname or u.lastname = :lastname")
      User findByLastnameOrFirstname(@Param("lastname") String lastname,
                                     @Param("firstname") String firstname);
    }

方法参数根据在定义的查询中的顺序进行切换。

从版本4开始，Spring完全支持基于`-parameters`编译器标志的Java 8参数名称发现。通过在构建中使用此标志作为调试信息的替代方法，可以省略`@Param`命名参数的注释。

#### [](#jpa.query.spel-expressions)5.3.7。使用SpEL表达式

从Spring Data JPA 1.4版开始，我们支持在使用定义的手动定义的查询中使用受限制的SpEL模板表达式`@Query`。在查询执行后，这些表达式将针对一组预定义的变量进行评估。Spring Data JPA支持一个叫做变量`entityName`。它的用法是`select x from #{#entityName} x`。它插入`entityName`与给定存储库关联的域类型。该`entityName`解决如下：如果域类型已设置的name属性`@Entity`的注释，它被使用。否则，使用域类型的简单类名称。

以下示例演示`#{#entityName}`了查询字符串中表达式的一种用例，您希望使用查询方法和手动定义的查询来定义存储库接口：

示例62.在存储库查询方法中使用SpEL表达式 - entityName

    @Entity
    public class User {
    
      @Id
      @GeneratedValue
      Long id;
    
      String lastname;
    }
    
    public interface UserRepository extends JpaRepository<User,Long> {
    
      @Query("select u from #{#entityName} u where u.lastname = ?1")
      List<User> findByLastname(String lastname);
    }

为避免在`@Query`注释的查询字符串中陈述实际的实体名称，可以使用该`#{#entityName}`变量。

该`entityName`可以通过使用定制`@Entity`的注释。`orm.xml`SpEL表达式不支持自定义。

当然，您可以`User`直接在查询声明中使用，但这也需要您更改查询。该类引用`#entityName`将`User`类的潜在未来重新映射转换为不同的实体名称（例如，通过使用`@Entity(name = "MyUser")`。

`#{#entityName}`查询字符串中表达式的另一个用例是，如果要为具体的域类型定义具有专用存储库接口的通用存储库接口。为了不重复定义具体接口上的​​自定义查询方法，可以`@Query`在通用资源库接口中的注释的查询字符串中使用实体名称表达式，如以下示例所示：

例63.在存储库查询方法中使用SpEL表达式 - 具有继承性的entityName

    @MappedSuperclass
    public abstract class AbstractMappedType {
      …
      String attribute
    }
    
    @Entity
    public class ConcreteType extends AbstractMappedType { … }
    
    @NoRepositoryBean
    public interface MappedTypeRepository<T extends AbstractMappedType>
      extends Repository<T, Long> {
    
      @Query("select t from #{#entityName} t where t.attribute = ?1")
      List<T> findAllByAttribute(String attribute);
    }
    
    public interface ConcreteRepository
      extends MappedTypeRepository<ConcreteType> { … }

在前面的例子中，`MappedTypeRepository`接口是扩展了几个域类型的公共父接口`AbstractMappedType`。它还定义了`findAllByAttribute(…)`可用于专用存储库接口实例的通用方法。如果您现在调用`findByAllAttribute(…)`上`ConcreteRepository`，查询变得`select t from ConcreteType t where t.attribute = ?1`。

#### [](#jpa.modifying-queries)5.3.8。修改查询

所有前面的部分都描述了如何声明查询来访问给定实体或实体集合。您可以使用“ [自定义Spring数据存储库实现](#repositories.custom-implementations) ”中描述的工具来添加自定义修改行为。由于此方法对于全面的自定义功能是可行的，因此您可以通过注释查询方法来修改仅需要参数绑定的查询`@Modifying`，如以下示例所示：

例64.声明操作查询

    @Modifying
    @Query("update User u set u.firstname = ?1 where u.lastname = ?2")
    int setFixedFirstnameFor(String firstname, String lastname);

这样做会触发将注释到方法的查询作为更新查询，而不是选择查询。由于在`EntityManager`修改查询执行后可能包含过时的实体，因此我们不会自动将其清除（请参阅[JavaDoc](https://docs.oracle.com/javaee/7/api/javax/persistence/EntityManager.html) of `EntityManager.clear()`的详细信息），因为这会有效地删除所有未更新的更改，这些更改仍在挂起`EntityManager`。如果您希望`EntityManager`自动清除，可以将`@Modifying`注释的`clearAutomatically`属性设置为`true`。

##### [](#jpa.modifying-queries.derived-delete)派生删除查询

Spring Data JPA还支持导出的删除查询，可以避免显式声明JPQL查询，如以下示例所示：

例65.使用派生的删除查询

    interface UserRepository extends Repository<User, Long> {
    
      void deleteByRoleId(long roleId);
    
      @Modifying
      @Query("delete from User u where user.role.id = ?1")
      void deleteInBulkByRoleId(long roleId);
    }

虽然这个`deleteByRoleId(…)`方法看起来基本上和它产生了相同的结果`deleteInBulkByRoleId(…)`，但是这两个方法声明在执行方式上存在着重要的区别。顾名思义，后一种方法针对数据库发出单个JPQL查询（在注释中定义的查询）。这意味着即使是当前加载的实例`User`也没有看到调用的生命周期回调。

为了确保实际调用生命周期查询，调用`deleteByRoleId(…)`执行查询，然后逐个删除返回的实例，以便持久性提供者可以实际调用`@PreRemove`这些实体的回调。

实际上，派生删除查询是执行查询然后调用`CrudRepository.delete(Iterable<User> users)`结果并保持行为与其他`delete(…)`方法的实现同步的快捷方式`CrudRepository`。

#### [](#jpa.query-hints)5.3.9。应用查询提示

要将JPA查询提示应用于存储库接口中声明的查询，可以使用`@QueryHints`注释。它需要一个JPA `@QueryHint`批注数组和一个布尔标志来禁用应用于应用分页时触发的附加计数查询的提示，如以下示例所示：

示例66.将QueryHints与存储库方法一起使用

    public interface UserRepository extends Repository<User, Long> {
    
      @QueryHints(value = { @QueryHint(name = "name", value = "value")},
                  forCounting = false)
      Page<User> findByLastname(String lastname, Pageable pageable);
    }

上述声明将应用`@QueryHint`为实际查询配置的值，但省略将其应用于触发的计数查询以计算总页数。

#### [](#jpa.entity-graph)5.3.10。配置提取和LoadGraphs

JPA 2.1规范引入了对指定Fetch和LoadGraphs的支持，我们也通过`@EntityGraph`注释支持它，它允许您引用`@NamedEntityGraph`定义。您可以在实体上使用该注释来配置生成的查询的提取计划。获取的类型（`Fetch`或`Load`）可以使用注释中的`type`属性进行配置`@EntityGraph`。请参阅JPA 2.1规范3.7.4以供进一步参考。

以下示例显示如何在实体上定义命名实体图：

例67.在实体上定义一个命名实体图。

    @Entity
    @NamedEntityGraph(name = "GroupInfo.detail",
      attributeNodes = @NamedAttributeNode("members"))
    public class GroupInfo {
    
      // default fetch mode is lazy.
      @ManyToMany
      List<GroupMember> members = new ArrayList<GroupMember>();
    
      …
    }

以下示例显示如何引用存储库查询方法上的命名实体图：

示例68.引用存储库查询方法上的命名实体图定义。

    @Repository
    public interface GroupRepository extends CrudRepository<GroupInfo, String> {
    
      @EntityGraph(value = "GroupInfo.detail", type = EntityGraphType.LOAD)
      GroupInfo getByGroupName(String name);
    
    }

也可以通过使用来定义临时实体图`@EntityGraph`。提供`attributePaths`的内容`EntityGraph`不需要显式添加`@NamedEntityGraph`到您的域类型就可以翻译成相应的内容，如以下示例所示：

示例69.在存储库查询方法上使用AD-HOC实体图定义。

    @Repository
    public interface GroupRepository extends CrudRepository<GroupInfo, String> {
    
      @EntityGraph(attributePaths = { "members" })
      GroupInfo getByGroupName(String name);
    
    }

#### [](#projections)5.3.11。预测

Spring Data查询方法通常会返回存储库管理的聚合根的一个或多个实例。但是，有时可能需要根据这些类型的某些属性创建投影。Spring Data允许对专用返回类型进行建模，以更有选择地检索托管集合的部分视图。

设想一个存储库和聚合根类型，例如以下示例：

示例70.样本聚合和存储库

    class Person {
    
      @Id UUID id;
      String firstname, lastname;
      Address address;
    
      static class Address {
        String zipCode, city, street;
      }
    }
    
    interface PersonRepository extends Repository<Person, UUID> {
    
      Collection<Person> findByLastname(String lastname);
    }

现在想象一下，我们只想检索人的姓名属性。Spring Data提供了什么手段来实现这一目标？本章的其余部分回答了这个问题。

##### [](#projections.interfaces)基于接口的投影

将查询结果仅限于名称属性的最简单方法是声明一个接口，该接口公开要读取的属性的访问器方法，如以下示例所示：

示例71.用于检索属性子集的投影界面

    interface NamesOnly {
    
      String getFirstname();
      String getLastname();
    }

这里重要的一点是，这里定义的属性完全匹配聚合根中的属性。这样做可以添加查询方法，如下所示：

示例72.使用基于接口的投影和查询方法的存储库

    interface PersonRepository extends Repository<Person, UUID> {
    
      Collection<NamesOnly> findByLastname(String lastname);
    }

查询执行引擎在运行时为每个返回的元素创建该接口的代理实例，并将调用转发给目标对象的公开方法。

可以递归地使用投影。如果您还想包含一些`Address`信息，请为其创建一个投影界面，并从声明中返回该界面`getAddress()`，如以下示例所示：

示例73.用于检索属性子集的投影界面

    interface PersonSummary {
    
      String getFirstname();
      String getLastname();
      AddressSummary getAddress();
    
      interface AddressSummary {
        String getCity();
      }
    }

在方法调用中，`address`获取目标实例的属性，并依次将其包装到投影代理中。

###### [](#projections.interfaces.closed)已关闭的投影

其访问器方法全部匹配目标聚合的属性的投影接口被认为是闭合投影。下面的例子（我们在本章前面也使用过）是一个封闭的投影：

例74.一个封闭的投影

    interface NamesOnly {
    
      String getFirstname();
      String getLastname();
    }

如果您使用封闭投影，Spring Data可以优化查询执行，因为我们知道支持投影代理所需的所有属性。有关更多详细信息，请参阅参考文档中特定于模块的部分。

###### [](#projections.interfaces.open)打开预测

投影接口中的访问器方法也可用于通过使用`@Value`注释来计算新值，如以下示例所示：

例子75.一个公开的投影

    interface NamesOnly {
    
      @Value("#{target.firstname + ' ' + target.lastname}")
      String getFullName();
      …
    }

支持投影的聚合根在`target`变量中可用。投影界面使用`@Value`是一个开放的投影。在这种情况下，Spring Data不能应用查询执行优化，因为SpEL表达式可以使用聚合根的任何属性。

使用的表达式`@Value`不应该太复杂 \- 你想避免在`String`变量中编程。对于非常简单的表达式，一个选项可能会采取默认方法（在Java 8中引入），如以下示例所示：

例76.一个投影界面使用默认方法来定制逻辑

    interface NamesOnly {
    
      String getFirstname();
      String getLastname();
    
      default String getFullName() {
        return getFirstname.concat(" ").concat(getLastname());
      }
    }

这种方法要求您能够纯粹基于投影界面上公开的其他访问器方法来实现逻辑。第二种更灵活的选择是在Spring bean中实现自定义逻辑，然后从SpEL表达式中调用它，如以下示例所示：

示例77.示例Person对象

    @Component
    class MyBean {
    
      String getFullName(Person person) {
        …
      }
    }
    
    interface NamesOnly {
    
      @Value("#{@myBean.getFullName(target)}")
      String getFullName();
      …
    }

注意SpEL表达式如何引用`myBean`并调用`getFullName(…)`方法并将投影目标作为方法参数转发。SpEL表达评估支持的方法也可以使用方法参数，然后可以从表达式中引用方法参数。方法参数可通过`Object`名为的数组获得`args`。以下示例显示如何从`args`数组中获取方法参数：

示例78.示例Person对象

    interface NamesOnly {
    
      @Value("#{args[0] + ' ' + target.firstname + '!'}")
      String getSalutation(String prefix);
    }

同样，对于更复杂的表达式，您应该使用Spring bean并让表达式调用一个方法，[如前所述](#projections.interfaces.open.bean-reference)。

##### [](#projections.dtos)基于类别的预测（DTO）

定义投影的另一种方法是使用值类型DTO（数据传输对象），它们为应该检索的字段保存属性。这些DTO类型的使用方式与投影界面的使用方式完全相同，只是没有代理发生，也不能应用嵌套投影。

如果商店通过限制要加载的字段来优化查询执行，则要从所公开的构造函数的参数名称中确定要加载的字段。

以下示例显示了投影DTO：

例79.一个投影DTO

    class NamesOnly {
    
      private final String firstname, lastname;
    
      NamesOnly(String firstname, String lastname) {
    
        this.firstname = firstname;
        this.lastname = lastname;
      }
    
      String getFirstname() {
        return this.firstname;
      }
    
      String getLastname() {
        return this.lastname;
      }
    
      // equals(…) and hashCode() implementations
    }

避免投影DTO的样板代码

你可以通过使用[Project Lombok](https://projectlombok.org)来显着简化DTO的代码，该[项目](https://projectlombok.org)提供了一个`@Value`注释（不要与`@Value`前面的界面示例中显示的Spring 注释混淆）。如果您使用Project Lombok的`@Value`注释，则前面显示的示例DTO将变为以下内容：

    @Value
    class NamesOnly {
        String firstname, lastname;
    }

字段`private final`默认情况下，该类公开一个构造函数，该构造函数接受所有字段并自动获取`equals(…)`并`hashCode()`实现方法。

##### [](#projection.dynamic)动态投影

到目前为止，我们已经使用投影类型作为集合的返回类型或元素类型。但是，您可能需要选择在调用时使用的类型（这会使其变为动态）。要应用动态投影，请使用查询方法，如下例所示：

示例80.使用动态投影参数的存储库

    interface PersonRepository extends Repository<Person, UUID> {
    
      <T> Collection<T> findByLastname(String lastname, Class<T> type);
    }

这样，可以使用该方法按原样或使用投影来获取聚合，如以下示例所示：

示例81.使用具有动态投影的存储库

    void someMethod(PersonRepository people) {
    
      Collection<Person> aggregates =
        people.findByLastname("Matthews", Person.class);
    
      Collection<NamesOnly> aggregates =
        people.findByLastname("Matthews", NamesOnly.class);
    }

### [](#jpa.stored-procedures)5.4。存储过程

JPA 2.1规范引入了使用JPA标准查询API调用存储过程的支持。我们引入了`@Procedure`在存储库方法中声明存储过程元数据的注释。

下面的示例使用以下过程：

例82\. `plus1inout`HSQL DB 中的过程定义。

    /;
    DROP procedure IF EXISTS plus1inout
    /;
    CREATE procedure plus1inout (IN arg int, OUT res int)
    BEGIN ATOMIC
     set res = arg + 1;
    END
    /;

存储过程的元数据可以通过`NamedStoredProcedureQuery`在实体类型上使用注释来配置。

例83.在实体上存储过程元数据定义。

    @Entity
    @NamedStoredProcedureQuery(name = "User.plus1", procedureName = "plus1inout", parameters = {
      @StoredProcedureParameter(mode = ParameterMode.IN, name = "arg", type = Integer.class),
      @StoredProcedureParameter(mode = ParameterMode.OUT, name = "res", type = Integer.class) })
    public class User {}

您可以通过多种方式从存储库方法中引用存储过程。要调用的存储过程既可以使用注释的`value`or `procedureName`属性直接定义，也可以使用该属性`@Procedure`间接定义`name`。如果没有配置名称，则使用存储库方法的名称作为回退。

以下示例显示如何引用明确映射的过程：

示例84：在数据库中引用具有名称“plus1inout”的显式映射过程。

    @Procedure("plus1inout")
    Integer explicitlyNamedPlus1inout(Integer arg);

以下示例显示如何使用`procedureName`别名引用隐式映射的过程：

示例85.通过`procedureName`别名在数据库中引用名为“plus1inout”的隐式映射过程。

    @Procedure(procedureName = "plus1inout")
    Integer plus1inout(Integer arg);

以下示例显示如何在以下位置引用显式映射的命名过程`EntityManager`：

示例86.引用明确映射的命名存储过程“User.plus1IO” `EntityManager`。

    @Procedure(name = "User.plus1IO")
    Integer entityAnnotatedCustomNamedProcedurePlus1IO(@Param("arg") Integer arg);

以下示例显示如何`EntityManager`使用方法名称引用隐式命名的存储过程：

示例87\. `EntityManager`通过使用方法名称引用隐式映射的命名存储过程“User.plus1” 。

    @Procedure
    Integer plus1(@Param("arg") Integer arg);

### [](#specifications)5.5。产品规格

JPA 2引入了可用于以编程方式构建查询的标准API。通过编写一个`criteria`，您可以为域类定义查询的where子句。再回过头来看，这些标准可以被看作是由JPA标准API约束描述的实体的谓词。

Spring Data JPA采用Eric Evans的书“Domain Driven Design”中的规范概念，遵循相同的语义，并提供API来定义JPA标准API的这些规范。为了支持规范，您可以使用`JpaSpecificationExecutor`接口扩展存储库接口，如下所示：

    public interface CustomerRepository extends CrudRepository<Customer, Long>, JpaSpecificationExecutor {
     …
    }

额外的接口有方法让您以各种方式执行规范。例如，该`findAll`方法返回所有符合规范的实体，如以下示例所示：

    List<T> findAll(Specification<T> spec);

的`Specification`接口被定义为如下：

    public interface Specification<T> {
      Predicate toPredicate(Root<T> root, CriteriaQuery<?> query,
                CriteriaBuilder builder);
    }

可以使用规范轻松地在实体上构建一组可扩展的谓词，然后可以将它们组合使用，`JpaRepository`而无需为每个需要的组合声明查询（方法），如以下示例所示：

示例88.客户的规范

    public class CustomerSpecs {
    
      public static Specification<Customer> isLongTermCustomer() {
        return new Specification<Customer>() {
          public Predicate toPredicate(Root<Customer> root, CriteriaQuery<?> query,
                CriteriaBuilder builder) {
    
             LocalDate date = new LocalDate().minusYears(2);
             return builder.lessThan(root.get(_Customer.createdAt), date);
          }
        };
      }
    
      public static Specification<Customer> hasSalesOfMoreThan(MontaryAmount value) {
        return new Specification<Customer>() {
          public Predicate toPredicate(Root<T> root, CriteriaQuery<?> query,
                CriteriaBuilder builder) {
    
             // build query here
          }
        };
      }
    }

诚然，样板的数量有待改进（Java 8关闭可能最终会减少这些空间），但客户端变得更好，您将在本节后面看到。该`_Customer`类型是使用JPA Metamodel生成器生成的元模型类型（例如，请参阅[Hibernate实现的文档](http://docs.jboss.org/hibernate/jpamodelgen/1.0/reference/en-US/html_single/#whatisit)）。所以表达式，`_Customer.createdAt`假定`Customer`有一个`createdAt`类型的属性`Date`。除此之外，我们已经在业务需求抽象层次上表达了一些标准并创建了可执行文件`Specifications`。所以客户可能会使用a `Specification`如下：

例89.使用一个简单的规范

    List<Customer> customers = customerRepository.findAll(isLongTermCustomer());

为什么不为这种数据访问创建查询？使用单个`Specification`查询声明不会获得比普通查询声明更多的好处。规范的力量真正发挥出来，当你把它们组合起来创造新的`Specification`物体。您可以通过`Specifications`我们提供的帮助器类来实现此目的，以构建类似于以下内容的表达式：

例90.组合的规格

    MonetaryAmount amount = new MonetaryAmount(200.0, Currencies.DOLLAR);
    List<Customer> customers = customerRepository.findAll(
      where(isLongTermCustomer()).or(hasSalesOfMoreThan(amount)));

`Specifications`提供了一些“胶合代码”方法来链接和组合`Specification`实例。这些方法允许您通过创建新的`Specification`实现并将它们与现有的实现相结合来扩展数据访问层。

### [](#query-by-example)5.6。按实例查询

#### [](#query-by-example.introduction)5.6.1。介绍

本章提供了对示例查询的介绍，并说明了如何使用它。

按实例查询（QBE）是一种用户界面友好的查询技术。它允许动态查询创建，并且不要求您编写包含字段名称的查询。事实上，按示例查询不需要您通过使用特定于商店的查询语言编写查询。

#### [](#query-by-example.usage)5.6.2。用法

按示例查询API由三部分组成：

*   探测器：具有填充字段的域对象的实际示例。
    
*   `ExampleMatcher`：提供`ExampleMatcher`有关如何匹配特定字段的详细信息。它可以在多个示例中重用。
    
*   `Example`：一个`Example`由探针和`ExampleMatcher`。它用于创建查询。
    

按实例查询非常适合多种用例：

*   用一组静态或动态约束查询数据存储。
    
*   频繁重构域对象，而不用担心打破现有查询。
    
*   独立于底层数据存储API工作。
    

按示例查询也有一些限制：

*   不支持嵌套或分组属性约束，例如`firstname = ?0 or (firstname = ?1 and lastname = ?2)`。
    
*   仅支持字符串的开始/包含/结束/正则表达式匹配以及其他属性类型的精确匹配。
    

在开始使用示例查询之前，您需要有一个域对象。要开始，请为您的存储库创建一个接口，如以下示例所示：

示例91.示例Person对象

    public class Person {
    
      @Id
      private String id;
      private String firstname;
      private String lastname;
      private Address address;
    
      // … getters and setters omitted
    }

上例显示了一个简单的域对象。你可以用它来创建一个`Example`。默认情况下，具有`null`值的字段将被忽略，并且字符串将通过使用特定于商店的默认值进行匹配。示例可以通过使用`of`工厂方法或使用来构建[`ExampleMatcher`](#query-by-example.matchers)。`Example`是不可变的。以下清单显示了一个简单的示例：

例92.简单的例子

    Person person = new Person();                         (1)
    person.setFirstname("Dave");                          (2)
    
    Example<Person> example = Example.of(person);         (3)

**1**

创建一个域对象的新实例。

**2**

设置要查询的属性。

**3**

创建`Example`。

理想情况下，示例将使用存储库执行。为此，请让您的存储库接口扩展`QueryByExampleExecutor<T>`。以下清单显示了`QueryByExampleExecutor`界面的摘录：

例93\. `QueryByExampleExecutor`

    public interface QueryByExampleExecutor<T> {
    
      <S extends T> S findOne(Example<S> example);
    
      <S extends T> Iterable<S> findAll(Example<S> example);
    
      // … more functionality omitted.
    }

#### [](#query-by-example.matchers)5.6.3。示例匹配器

示例不限于默认设置。您可以通过使用`ExampleMatcher`，为字符串匹配，空值处理和特定于属性的设置指定您自己的缺省值，如以下示例所示：

示例94.具有定制匹配的示例匹配器

    Person person = new Person();                          (1)
    person.setFirstname("Dave");                           (2)
    
    ExampleMatcher matcher = ExampleMatcher.matching()     (3)
      .withIgnorePaths("lastname")                         (4)
      .withIncludeNullValues()                             (5)
      .withStringMatcherEnding();                          (6)
    
    Example<Person> example = Example.of(person, matcher); (7)

**1**

创建一个域对象的新实例。

**2**

设置属性。

**3**

创建一个`ExampleMatcher`期望所有值匹配的值。即使没有进一步的配置，它也可以在此阶段使用。

**4**

构建一个新的`ExampleMatcher`来忽略`lastname`属性路径。

**五**

构造一个新的`ExampleMatcher`来忽略`lastname`属性路径并包含空值。

**6**

构造一个新的`ExampleMatcher`来忽略`lastname`属性路径，包含空值，并执行后缀字符串匹配。

**7**

`Example`根据域对象和配置创建一个新的`ExampleMatcher`。

默认情况下，`ExampleMatcher`期望探针上设置的所有值匹配。如果你想得到匹配隐式定义的任何谓词的结果，请使用`ExampleMatcher.matchingAny()`。

您可以为单个属性指定行为（例如“firstname”和“lastname”，或者对于嵌套属性，“address.city”）。您可以使用匹配选项和区分大小写来调整它，如以下示例所示：

例子95.配置匹配器选项

    ExampleMatcher matcher = ExampleMatcher.matching()
      .withMatcher("firstname", endsWith())
      .withMatcher("lastname", startsWith().ignoreCase());
    }

另一种配置匹配器选项的方法是使用lambdas（在Java 8中引入）。这种方法创建了一个回调，要求实现者修改匹配器。您无需返回匹配器，因为配置选项在匹配器实例中保存。以下示例显示使用lambdas的匹配器：

示例96.使用lambdas配置匹配器选项

    ExampleMatcher matcher = ExampleMatcher.matching()
      .withMatcher("firstname", match -> match.endsWith())
      .withMatcher("firstname", match -> match.startsWith());
    }

通过`Example`使用配置的合并视图创建的查询。默认匹配设置可以在`ExampleMatcher`级别上设置，而单独的设置可以应用于特定的属性路径。设置的设置`ExampleMatcher`将由属性路径设置继承，除非它们是明确定义的。属性修补程序上的设置优先于默认设置。下表介绍了各种`ExampleMatcher`设置的范围：

表4\. `ExampleMatcher`设置的范围  

设置

范围

空操作

`ExampleMatcher`

字符串匹配

`ExampleMatcher` 和财产路径

忽略属性

属性路径

区分大小写

`ExampleMatcher` 和财产路径

价值转化

属性路径

#### [](#query-by-example.execution)5.6.4。执行一个例子

在Spring Data JPA中，您可以将示例查询与存储库一起使用，如以下示例所示：

示例97.使用存储库的示例查询

    public interface PersonRepository extends JpaRepository<Person, String> { … }
    
    public class PersonService {
    
      @Autowired PersonRepository personRepository;
    
      public List<Person> findPeople(Person probe) {
        return personRepository.findAll(Example.of(probe));
      }
    }

目前，只有`SingularAttribute`属性可以用于属性匹配。

属性说明符接受属性名称（如`firstname`和`lastname`）。您可以通过链接属性与点（`address.city`）进行导航。您还可以使用匹配选项和区分大小写来调整它。

下表显示了`StringMatcher`您可以使用的各种选项以及在名为的字段上使用它们的结果`firstname`：

表5\. `StringMatcher`选项  

匹配

逻辑结果

`DEFAULT` （区分大小写）

`firstname = ?0`

`DEFAULT` （不区分大小写）

`LOWER(firstname) = LOWER(?0)`

`EXACT` （区分大小写）

`firstname = ?0`

`EXACT` （不区分大小写）

`LOWER(firstname) = LOWER(?0)`

`STARTING` （区分大小写）

`firstname like ?0 + '%'`

`STARTING` （不区分大小写）

`LOWER(firstname) like LOWER(?0) + '%'`

`ENDING` （区分大小写）

`firstname like '%' + ?0`

`ENDING` （不区分大小写）

`LOWER(firstname) like '%' + LOWER(?0)`

`CONTAINING` （区分大小写）

`firstname like '%' + ?0 + '%'`

`CONTAINING` （不区分大小写）

`LOWER(firstname) like '%' + LOWER(?0) + '%'`

### [](#transactions)5.7。事务性

默认情况下，存储库实例上的CRUD方法是事务性的。对于读操作，事务配置`readOnly`标志设置为`true`。所有其他人都配置为纯文本，`@Transactional`以便应用默认事务配置。有关详细信息，请参阅JavaDoc [`SimpleJpaRepository`](https://docs.spring.io/spring-data/data-jpa/docs/current/api/index.html?org/springframework/data/jpa/repository/support/SimpleJpaRepository.html)。如果您需要调整存储库中声明的某个方法的事务配置，请在存储库接口中重新声明该方法，如下所示：

示例98\. CRUD的自定义事务配置

    public interface UserRepository extends CrudRepository<User, Long> {
    
      @Override
      @Transactional(timeout = 10)
      public List<User> findAll();
    
      // Further query method declarations
    }

这样做会导致`findAll()`方法以10秒的超时运行并且没有`readOnly`标志。

另一种改变事务行为的方式是使用一个（通常）覆盖多个存储库的外观或服务实现。其目的是为非CRUD操作定义事务边界。以下示例显示如何为多个存储库使用这种外观：

示例99.使用Facade为多个存储库调用定义事务

    @Service
    class UserManagementImpl implements UserManagement {
    
      private final UserRepository userRepository;
      private final RoleRepository roleRepository;
    
      @Autowired
      public UserManagementImpl(UserRepository userRepository,
        RoleRepository roleRepository) {
        this.userRepository = userRepository;
        this.roleRepository = roleRepository;
      }
    
      @Transactional
      public void addRoleToAllUsers(String roleName) {
    
        Role role = roleRepository.findByName(roleName);
    
        for (User user : userRepository.findAll()) {
          user.addRole(role);
          userRepository.save(user);
        }
    }

这个例子导致调用`addRoleToAllUsers(…)`在一个事务内部运行（参与现有的或创建一个新的，如果没有运行的话）。然后忽略存储库中的事务配置，因为外部事务配置确定了实际使用的配置。请注意，您必须激活`<tx:annotation-driven />`或`@EnableTransactionManagement`显式使用才能获得基于注释的外墙配置。本示例假定您使用组件扫描。

#### [](#transactional-query-methods)5.7.1。事务查询方法

要让您的查询方法成为事务性的，请`@Transactional`在您定义的存储库接口上使用，如以下示例所示：

示例100.在查询方法中使用@Transactional

    @Transactional(readOnly = true)
    public interface UserRepository extends JpaRepository<User, Long> {
    
      List<User> findByLastname(String lastname);
    
      @Modifying
      @Transactional
      @Query("delete from User u where u.active = false")
      void deleteInactiveUsers();
    }

通常情况下，您希望`readOnly`标志被设置为`true`，因为大多数查询方法只能读取数据。与此相反，`deleteInactiveUsers()`使用`@Modifying`注释并覆盖事务配置。因此，该方法运行`readOnly`标志设置为`false`。

您可以将事务用于只读查询，并通过设置`readOnly`标志来标记它们。但是，这样做并不能检查您是否触发操作查询（尽管某些数据库在只读事务中拒绝`INSERT`和`UPDATE`声明）。`readOnly`相反，将该标志作为提示传播到基础JDBC驱动程序以进行性能优化。此外，Spring对底层的JPA提供者进行一些优化。例如，当与Hibernate一起使用时，刷新模式被设置为`NEVER`当您将事务配置为时`readOnly`，这将导致Hibernate跳过脏检查（对大型对象树显着改进）。

### [](#locking)5.8。锁定

要指定要使用的锁定模式，可以`@Lock`在查询方法上使用注释，如以下示例所示：

例101.定义查询方法的锁定元数据

    interface UserRepository extends Repository<User, Long> {
    
      // Plain query method
      @Lock(LockModeType.READ)
      List<User> findByLastname(String lastname);
    }

这个方法声明将导致触发查询中配备了`LockModeType`的`READ`。您还可以通过在存储库接口中重新声明它们并添加`@Lock`注释来为CRUD方法定义锁定，如以下示例所示：

示例102.在CRUD方法上定义锁定元数据

    interface UserRepository extends Repository<User, Long> {
    
      // Redeclaration of a CRUD method
      @Lock(LockModeType.READ);
      List<User> findAll();
    }

### [](#auditing)5.9。审计

#### [](#auditing.basics)5.9.1。基本

Spring Data提供复杂的支持以透明地跟踪谁创建或更改实体以及发生更改的时间。为了从该功能中受益，您必须为实体类配备审计元数据，这些元数据可以使用注释或通过实现接口来定义。

##### [](#auditing.annotations)基于注释的审计元数据

我们提供`@CreatedBy`和`@LastModifiedBy`捕捉谁创建或修改的实体以及用户`@CreatedDate`和`@LastModifiedDate`捕捉时的变化发生了。

例103.被审计单位

    class Customer {
    
      @CreatedBy
      private User user;
    
      @CreatedDate
      private DateTime createdDate;
    
      // … further properties omitted
    }

正如您所看到的，注释可以选择性地应用，具体取决于您要捕获的信息。更改时间捕捉注释可以在类型乔达，时间，性质使用`DateTime`，遗留Java `Date`和`Calendar`，JDK8日期和时间类型，以及`long`或`Long`。

##### [](#auditing.interfaces)基于接口的审计元数据

如果您不想使用注释来定义审计元数据，则可以让您的域类实现该`Auditable`界面。它公开了所有审计属性的setter方法。

还有一个便利的基类，`AbstractAuditable`您可以扩展该基类以避免需要手动实现接口方法。这样做会增加域类与Spring Data的耦合，这可能是您想要避免的。通常，定义审计元数据的基于注释的方式是首选，因为它侵入性更小，更灵活。

##### [](#auditing.auditor-aware)`AuditorAware`

如果您使用`@CreatedBy`或者`@LastModifiedBy`，审计基础设施需要知道当前的委托人。为此，我们提供一个`AuditorAware<T>`SPI接口，您必须实施该接口，以告知基础架构当前用户或系统与应用程序进行交互的人员。泛型`T`定义了哪些类型的属性注释`@CreatedBy`或`@LastModifiedBy`必须是。

以下示例显示了使用Spring Security `Authentication`对象的接口的实现：

例104.基于Spring Security的AuditorAware的实现

    class SpringSecurityAuditorAware implements AuditorAware<User> {
    
      public User getCurrentAuditor() {
    
        Authentication authentication = SecurityContextHolder.getContext().getAuthentication();
    
        if (authentication == null || !authentication.isAuthenticated()) {
          return null;
        }
    
        return ((MyUserDetails) authentication.getPrincipal()).getUser();
      }
    }

该实现访问`Authentication`Spring Security提供的对象，并查找`UserDetails`您在`UserDetailsService`实现中创建的自定义实例。我们在这里假设你正在通过`UserDetails`实现暴露域用户，但是根据`Authentication`找到的，你也可以从任何地方查看它。：leveloffset：-1

#### [](#jpa.auditing)5.9.2。JPA审计

##### [](#jpa.auditing.configuration)一般审计配置

Spring Data JPA附带一个实体监听器，可用于触发捕获审计信息。首先，您必须`AuditingEntityListener`在`orm.xml`文件内的持久性上下文中注册要用于所有实体的对象，如以下示例所示：

示例105.审计配置orm.xml

    <persistence-unit-metadata>
      <persistence-unit-defaults>
        <entity-listeners>
          <entity-listener class="….data.jpa.domain.support.AuditingEntityListener" />
        </entity-listeners>
      </persistence-unit-defaults>
    </persistence-unit-metadata>

您还可以`AuditingEntityListener`使用`@EntityListeners`注释在每个实体的基础上启用，如下所示：

    @Entity
    @EntityListeners(AuditingEntityListener.class)
    public class MyEntity {
    
    }

审计功能需要`spring-aspects.jar`位于类路径中。

通过`orm.xml`适当修改并`spring-aspects.jar`在类路径中，激活审计功能就是将Spring Data JPA `auditing`命名空间元素添加到您的配置中，如下所示：

示例106.使用XML配置激活审计

    <jpa:auditing auditor-aware-ref="yourAuditorAwareBean" />

从Spring Data JPA 1.5开始，您可以通过使用注释注释配置类来启用审计`@EnableJpaAuditing`。您仍然必须修改该`orm.xml`文件并`spring-aspects.jar`在类路径中进行。以下示例显示如何使用`@EnableJpaAuditing`注释：

示例107.使用Java配置激活审计

    @Configuration
    @EnableJpaAuditing
    class Config {
    
      @Bean
      public AuditorAware<AuditableUser> auditorProvider() {
        return new AuditorAwareImpl();
      }
    }

如果您`AuditorAware`向该类型公开了一个类型的bean `ApplicationContext`，则审计基础结构会自动将其选中并使用它来确定要在域类型上设置的当前用户。如果您有多个注册的实现`ApplicationContext`，您可以通过显式设置`auditorAwareRef`属性来选择要使用的实现`@EnableJpaAuditing`。

### [](#jpa.misc)5.10。其他注意事项

#### [](#jpa.misc.jpa-context)5.10.1。使用`JpaContext`在自定义实现

在处理多个`EntityManager`实例和[自定义存储库实现时](#repositories.custom-implementations)，您需要将正确的连接`EntityManager`到存储库实现类。您可以通过`EntityManager`在`@PersistenceContext`注释中明确命名或者如果`EntityManager`是`@Autowired`，通过使用来实现`@Qualifier`。

从Spring Data JPA 1.9开始，Spring Data JPA包含一个名为的类`JpaContext`，它允许您`EntityManager`通过托管域类获取，假设它只由`EntityManager`应用程序中的一个实例管理。以下示例显示如何`JpaContext`在自定义存储库中使用：

示例108\. `JpaContext`在定制存储库实现中使用

    class UserRepositoryImpl implements UserRepositoryCustom {
    
      private final EntityManager em;
    
      @Autowired
      public UserRepositoryImpl(JpaContext context) {
        this.em = context.getEntityManagerByManagedType(User.class);
      }
    
      …
    }

这种方法的优点是，如果域类型被分配给不同的持久性单元，则不必触摸存储库来改变对持久性单元的引用。

#### [](#jpa.misc.merging-persistence-units)5.10.2。合并持久性单元

Spring支持多个持久化单元。然而，有时候，您可能希望模块化应用程序，但仍要确保所有这些模块都在单个持久性单元中运行。为了实现这种行为，Spring Data JPA提供了一个`PersistenceUnitManager`基于名称自动合并持久性单元的实现，如下例所示：

例109.使用MergingPersistenceUnitmanager

    <bean class="….LocalContainerEntityManagerFactoryBean">
      <property name="persistenceUnitManager">
        <bean class="….MergingPersistenceUnitManager" />
      </property>
    </bean>

##### [](#jpa.misc.entity-scanning)类路径扫描@Entity类和JPA映射文件

简单的JPA设置需要列出所有注解映射的实体类`orm.xml`。这同样适用于XML映射文件。Spring Data JPA提供了一个`ClasspathScanningPersistenceUnitPostProcessor`可以获取配置的基础包并可选择使用映射文件名模式。然后，它会扫描给定的包中用`@Entity`or 注释的类`@MappedSuperclass`，并加载与文件名模式匹配的配置文件，并将它们传递给JPA配置。后处理器必须配置如下：

例子110.使用ClasspathScanningPersistenceUnitPostProcessor

    <bean class="….LocalContainerEntityManagerFactoryBean">
      <property name="persistenceUnitPostProcessors">
        <list>
          <bean class="org.springframework.data.jpa.support.ClasspathScanningPersistenceUnitPostProcessor">
            <constructor-arg value="com.acme.domain" />
            <property name="mappingFileNamePattern" value="**/*Mapping.xml" />
          </bean>
        </list>
      </property>
    </bean>

从Spring 3.1开始，可直接配置要扫描的软件包`LocalContainerEntityManagerFactoryBean`以启用实体类的类路径扫描。有关详细信息，请参阅[JavaDoc](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.html#setPackagesToScan(java.lang.String...))。

#### [](#jpd.misc.cdi-integration)5.10.3。CDI集成

存储库接口的实例通常由容器创建，对于Spring而言，在使用Spring Data时，Spring是最自然的选择。Spring为创建bean实例提供了复杂的支持，如[创建存储库实例中所述](#repositories.create-instances)。从版本1.1.0开始，Spring Data JPA附带一个自定义CDI扩展，允许在CDI环境中使用存储库抽象。该扩展是JAR的一部分。要激活它，请在您的类路径中包含Spring Data JPA JAR。

您现在可以通过为`EntityManagerFactory`and 执行CDI Producer来设置基础架构`EntityManager`，如以下示例所示：

    class EntityManagerFactoryProducer {
    
      @Produces
      @ApplicationScoped
      public EntityManagerFactory createEntityManagerFactory() {
        return Persistence.createEntityManagerFactory("my-presistence-unit");
      }
    
      public void close(@Disposes EntityManagerFactory entityManagerFactory) {
        entityManagerFactory.close();
      }
    
      @Produces
      @RequestScoped
      public EntityManager createEntityManager(EntityManagerFactory entityManagerFactory) {
        return entityManagerFactory.createEntityManager();
      }
    
      public void close(@Disposes EntityManager entityManager) {
        entityManager.close();
      }
    }

必要的设置可能因JavaEE环境而异。你可能只需要重新声明`EntityManager`一个CDI bean就可以了，如下所示：

    class CdiConfig {
    
      @Produces
      @RequestScoped
      @PersistenceContext
      public EntityManager entityManager;
    }

在前面的示例中，容器必须能够创建JPA `EntityManagers`本身。所有配置都会将JPA重新导出`EntityManager`为CDI bean。

Spring Data JPA CDI扩展将所有可用的`EntityManager`实例选为CDI bean，并在容器请求存储库类型的bean时为Spring Data存储库创建代理。因此，获取Spring Data存储库的一个实例是声明一个`@Injected`属性的问题，如下例所示：

    class RepositoryClient {
    
      @Inject
      PersonRepository repository;
    
      public void businessMethod() {
        List<Person> people = repository.findAll();
      }
    }

[](#appendix)附录
===============

[](#repositories.namespace-reference)附录A：命名空间参考
-----------------------------------------------

### [](#populator.namespace-dao-config)该`<repositories />`元素

该`<repositories />`元素触发了Spring Data存储库基础设施的设置。最重要的属性是`base-package`，它定义了用于扫描Spring数据存储库接口的包。请参阅“ [XML配置](#repositories.create-instances.spring) ”。下表描述了该`<repositories />`元素的属性：

表6.属性  

名称

描述

`base-package`

定义要`*Repository`在自动检测模式下扩展的存储库接口的扫描包（实际接口由特定的Spring Data模块确定）。扫描配置软件包下面的所有软件包。通配符是允许的。

`repository-impl-postfix`

定义后缀以自动检测自定义存储库实现。名称以配置的后缀结尾的类被视为候选。默认为`Impl`。

`query-lookup-strategy`

确定用于创建查找器查询的策略。有关详细信息，请参阅“ [查询查找策略](#repositories.query-methods.query-lookup-strategies) ”。默认为`create-if-not-found`。

`named-queries-location`

定义搜索包含外部定义的查询的属性文件的位置。

`consider-nested-repositories`

是否应该考虑嵌套的存储库接口定义。默认为`false`。

[](#populator.namespace-reference)附录B：Poppers命名空间参考
---------------------------------------------------

### [](#namespace-dao-config)<populator />元素

该`<populator />`元素允许通过Spring Data存储库基础结构填充数据存储。
[1](#_footnote_1 "查看脚注。")


表7.属性  

名称

描述

`locations`

在哪里可以找到要从存储库中读取对象的文件。

[](#repository-query-keywords)附录C：存储库查询关键字
------------------------------------------

### [](#_supported_query_keywords)支持的查询关键字

下表列出了Spring Data存储库查询派生机制通常支持的关键字。但是，请参阅特定商店的文档以获取支持的关键字的确切列表，因为此处列出的某些关键字可能在特定商店中不受支持。

表8.查询关键字  

逻辑关键字

关键字表达

`AND`

`And`

`OR`

`Or`

`AFTER`

`After`， `IsAfter`

`BEFORE`

`Before`， `IsBefore`

`CONTAINING`

`Containing`，`IsContaining`，`Contains`

`BETWEEN`

`Between`， `IsBetween`

`ENDING_WITH`

`EndingWith`，`IsEndingWith`，`EndsWith`

`EXISTS`

`Exists`

`FALSE`

`False`， `IsFalse`

`GREATER_THAN`

`GreaterThan`， `IsGreaterThan`

`GREATER_THAN_EQUALS`

`GreaterThanEqual`， `IsGreaterThanEqual`

`IN`

`In`， `IsIn`

`IS`

`Is`，，`Equals`（或没有关键字）

`IS_EMPTY`

`IsEmpty`， `Empty`

`IS_NOT_EMPTY`

`IsNotEmpty`， `NotEmpty`

`IS_NOT_NULL`

`NotNull`， `IsNotNull`

`IS_NULL`

`Null`， `IsNull`

`LESS_THAN`

`LessThan`， `IsLessThan`

`LESS_THAN_EQUAL`

`LessThanEqual`， `IsLessThanEqual`

`LIKE`

`Like`， `IsLike`

`NEAR`

`Near`， `IsNear`

`NOT`

`Not`， `IsNot`

`NOT_IN`

`NotIn`， `IsNotIn`

`NOT_LIKE`

`NotLike`， `IsNotLike`

`REGEX`

`Regex`，`MatchesRegex`，`Matches`

`STARTING_WITH`

`StartingWith`，`IsStartingWith`，`StartsWith`

`TRUE`

`True`， `IsTrue`

`WITHIN`

`Within`， `IsWithin`

[](#repository-query-return-types)附录D：存储库查询返回类型
-----------------------------------------------

### [](#_supported_query_return_types)支持的查询返回类型

下表列出了Spring Data存储库通常支持的返回类型。但是，请参阅特定于商店的文档以获取受支持的返回类型的确切列表，因为此处列出的某些类型可能在特定商店中不受支持。

地理空间类型（如`GeoResult`，`GeoResults`，和`GeoPage`）是仅对支持地理空间查询数据存储可用。

表9.查询返回类型  

返回类型

描述

`void`

表示没有返回值。

基元

Java基元。

包装类型

Java包装类型。

`T`

一个独特的实体。期望查询方法最多返回一个结果。如果没有找到结果，`null`则返回。多个结果触发一个`IncorrectResultSizeDataAccessException`。

`Iterator<T>`

一个`Iterator`。

`Collection<T>`

一`Collection`。

`List<T>`

一`List`。

`Optional<T>`

Java 8或番石榴`Optional`。期望查询方法最多返回一个结果。如果没有找到结果，`Optional.empty()`或者`Optional.absent()`返回。多个结果触发一个`IncorrectResultSizeDataAccessException`。

`Option<T>`

Scala或Javalang `Option`类型。语义上与`Optional`前面描述的Java 8相同。

`Stream<T>`

Java 8 `Stream`。

`Future<T>`

一`Future`。期望一个方法被注释`@Async`并且要求启用Spring的异步方法执行能力。

`CompletableFuture<T>`

Java 8 `CompletableFuture`。期望一个方法被注释`@Async`并且要求启用Spring的异步方法执行能力。

`ListenableFuture`

一`org.springframework.util.concurrent.ListenableFuture`。期望一个方法被注释`@Async`并且要求启用Spring的异步方法执行能力。

`Slice`

大小的数据块，指示是否有更多数据可用。需要一个`Pageable`方法参数。

`Page<T>`

A `Slice`附加信息，如结果总数。需要一个`Pageable`方法参数。

`GeoResult<T>`

带有附加信息的结果输入，例如到参考位置的距离。

`GeoResults<T>`

`GeoResult<T>`附加信息列表，例如参考位置的平均距离。

`GeoPage<T>`

甲`Page`带`GeoResult<T>`，如到参考位置的平均距离。

`Mono<T>`

`Mono`使用反应性储存库发射零个或一个元素的项目反应器。期望查询方法最多返回一个结果。如果没有找到结果，`Mono.empty()`则返回。多个结果触发一个`IncorrectResultSizeDataAccessException`。

`Flux<T>`

项目反应堆`Flux`使用反应性储存库发射零个，一个或多个元素。返回的查询`Flux`可以发出无数个元素。

`Single<T>`

RxJava `Single`使用反应性仓库发射单个元素。期望查询方法最多返回一个结果。如果没有找到结果，`Mono.empty()`则返回。多个结果触发一个`IncorrectResultSizeDataAccessException`。

`Maybe<T>`

一个RxJava `Maybe`使用被动存储库发射零个或一个元素。期望查询方法最多返回一个结果。如果没有找到结果，`Mono.empty()`则返回。多个结果触发一个`IncorrectResultSizeDataAccessException`。

`Flowable<T>`

一个RxJava `Flowable`使用被动存储库发射零个，一个或多个元素。返回的查询`Flowable`可以发出无数个元素。

[](#faq)附录E：常见问题
----------------

### [](#_common)共同

1.  _我想获得关于哪些方法在内部调用的更详细的日志记录信息`JpaRepository`（例如）。我如何获得它们？_
    
    您可以使用`CustomizableTraceInterceptor`Spring提供的，如以下示例所示：
    
        <bean id="customizableTraceInterceptor" class="
          org.springframework.aop.interceptor.CustomizableTraceInterceptor">
          <property name="enterMessage" value="Entering $[methodName]($[arguments])"/>
          <property name="exitMessage" value="Leaving $[methodName](): $[returnValue]"/>
        </bean>
        
        <aop:config>
          <aop:advisor advice-ref="customizableTraceInterceptor"
            pointcut="execution(public * org.springframework.data.jpa.repository.JpaRepository+.*(..))"/>
        </aop:config>
    

### [](#_infrastructure)基础设施

1.  _目前我已经实现了基于的存储库层`HibernateDaoSupport`。我`SessionFactory`使用Spring 创建了一个`AnnotationSessionFactoryBean`。我如何让Spring Data存储库在这个环境中工作？_
    
    必须更换`AnnotationSessionFactoryBean`与`HibernateJpaSessionFactoryBean`如下：
    
    例111\. `SessionFactory`从a中查找a`HibernateEntityManagerFactory`
    
        <bean id="sessionFactory" class="org.springframework.orm.jpa.vendor.HibernateJpaSessionFactoryBean">
          <property name="entityManagerFactory" ref="entityManagerFactory"/>
        </bean>
    

### [](#_auditing)审计

1.  _我想使用Spring Data JPA审计功能，但是我的数据库已经配置为在实体上设置修改和创建日期。如何防止Spring Data以编程方式设置日期。_
    
    将名称空间元素的`set-dates`属性设置`auditing`为`false`。
    

[](#glossary)附录F：术语表
--------------------

AOP

面向方面的编程

Commons DBCP

Commons DataBase连接池 - 来自Apache基础的库，提供DataSource接口的池实现。

CRUD

创建，读取，更新，删除 \- 基本的持久性操作。

DAO

数据访问对象 \- 从持久化对象中分离持久逻辑的模式

Dependency Injection

从外部将组件的依赖关系传递给组件的模式，释放组件以查找依赖关系本身。有关更多信息，请参阅[](https://en.wikipedia.org/wiki/Dependency_Injection)[http://en.wikipedia.org/wiki/Dependency_Injection](https://en.wikipedia.org/wiki/Dependency_Injection)。

EclipseLink

实现JPA的对象关系映射器 - [](http://www.eclipselink.org)[http://www.eclipselink.org](http://www.eclipselink.org)

Hibernate

实现JPA的对象关系映射器 - [](http://www.hibernate.org)[http://www.hibernate.org](http://www.hibernate.org)

JPA

Java持久性API

Spring

Java应用程序框架 - [](https://projects.spring.io/spring-framework)[http://projects.spring.io/spring-framework](https://projects.spring.io/spring-framework)

* * *

[1](#_footnoteref_1)。请参阅[XML配置](#repositories.create-instances.spring)

版本2.1.0.M3  
上次更新时间2018-05-17 09:45:35 MESZ