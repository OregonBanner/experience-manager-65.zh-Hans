---
title: 连接到SQL数据库
seo-title: 连接到SQL数据库
description: 访问外部SQL数据库，以便您的AEM应用程序可以与数据交互
seo-description: 访问外部SQL数据库，以便您的AEM应用程序可以与数据交互
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# 连接到SQL数据库{#connecting-to-sql-databases}

访问外部SQL数据库，以便CQ应用程序可以与数据交互：

1. [创建或获取用于导出JDBC驱动程序包的OSGi包](#bundling-the-jdbc-database-driver)。
1. [配置JDBC数据源池提供程序](#configuring-the-jdbc-connection-pool-service)。
1. [获取数据源对象，并在代码中创建连接](#connecting-to-the-database)。

## 捆绑JDBC数据库驱动程序{#bundling-the-jdbc-database-driver}

某些数据库供应商在OSGi包中提供JDBC驱动程序，例如[MySQL](https://www.mysql.com/downloads/connector/j/)。 如果数据库的JDBC驱动程序不可用作OSGi包，请获取该驱动程序JAR并将其封装在OSGi包中。 包必须导出与数据库服务器交互所需的包。 包还必须导入其引用的包。

以下示例使用Maven](https://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html)的[包插件将HSQLDB驱动程序封装在OSGi包中。 POM会指示该插件嵌入标识为依赖项的hsqldb.jar文件。 所有org.hsqldb包都将导出。

该插件会自动确定要导入的包，并将其列在包的MANIFEST.MF文件中。 如果CQ服务器上没有任何包，则在安装时将不会启动包。 可能的解决方案如下：

* 在POM中指示包是可选的。 当JDBC连接实际上不需要包成员时，请使用此解决方案。 使用Import-Package元素指示可选包，如以下示例中所示：

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* 将包含包的JAR文件包装在导出包的OSGi包中，并部署包。 如果在代码执行期间需要包成员，请使用此解决方案。

了解源代码可让您确定要使用的解决方案。 您还可以尝试使用任一解决方案并执行测试以验证解决方案。

### 捆绑hsqldb.jar {#pom-that-bundles-hsqldb-jar}的POM

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>hsqldb-jdbc-driver-bundle</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>wrapper-bundle-hsqldb-driver</name>
  <url>www.adobe.com</url>
  <description>Exports the HSQL JDBC driver</description>
  <packaging>bundle</packaging>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <version>1.4.3</version>
        <extensions>true</extensions>
        <configuration>
         <instructions>
            <Embed-Dependency>*</Embed-Dependency>
            <_exportcontents>org.hsqldb.*</_exportcontents>
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>hsqldb</groupId>
      <artifactId>hsqldb</artifactId>
      <version>2.2.9</version>
    </dependency>
  </dependencies>
</project>
```

以下链接可打开一些常用数据库产品的下载页面：

* [Microsoft SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [Oracle](https://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
* [IBM DB2](https://www-01.ibm.com/support/docview.wss?uid=swg27007053)

### 配置JDBC连接池服务{#configuring-the-jdbc-connection-pool-service}

为JDBC连接池服务添加配置，该服务使用JDBC驱动程序创建数据源对象。 您的应用程序代码使用此服务获取对象并连接到数据库。

JDBC连接池(`com.day.commons.datasource.jdbcpool.JdbcPoolService`)是工厂服务。 如果您需要使用不同属性（例如只读或读/写访问）的连接，请创建多个配置。

使用CQ时，可通过多种方法来管理此类服务的配置设置；有关完整的详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

以下属性可用于配置池化连接服务。 属性名称会按在Web控制台中显示的方式列出。 `sling:OsgiConfig`节点的相应名称显示在括号中。 HSQLDB服务器和别名为`mydb`的数据库的示例值如下：

* JDBC驱动程序类(`jdbc.driver.class`):用于实现java.sql.Driver接口的Java类，例如`org.hsqldb.jdbc.JDBCDriver`。 数据类型为`String`。

* JDBC连接URI(`jdbc.connection.uri`):用于创建连接的数据库URL，例如`jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`。 URL的格式必须有效，才能与java.sql.DriverManager类的getConnection方法一起使用。 数据类型为`String`。

* 用户名(`jdbc.username`):用于通过数据库服务器进行身份验证的用户名。 数据类型为`String`。

* 密码(`jdbc.password`):用于用户身份验证的密码。 数据类型为`String`。

* 验证查询(`jdbc.validation.query`):用于验证连接是否成功的SQL语句，例如`select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`。 数据类型为`String`。

* 默认为只读(default.readonly):如果希望连接提供只读访问权限，请选择此选项。 数据类型为`Boolean`。
* 默认情况下自动提交(`default.autocommit`):选择此选项可为发送到数据库的每个SQL命令创建单独的事务，并且每个事务都会自动提交。 在代码中显式提交事务时，请勿选择此选项。 数据类型为`Boolean`。

* 池大小(`pool.size`):要向数据库提供的同时连接数。 数据类型为`Long`。

* 池等待(`pool.max.wait.msec`):连接请求超时前的时间。 数据类型为`Long`。

* 数据源名称(`datasource.name`):此数据源的名称。 数据类型为`String`。

* 其他服务属性(`datasource.svc.properties`):要附加到连接URL的一组名称/值对。 数据类型为`String[]`。

JDBC连接池服务是工厂。 因此，如果使用`sling:OsgiConfig`节点配置连接服务，则节点的名称必须包含出厂服务PID，后跟&#x200B;*`-alias`*。 对于该PID的所有配置节点，您使用的别名必须是唯一的。 示例节点名称为`com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`。

![chlimage_1-7](assets/chlimage_1-7a.png)

### 连接到数据库{#connecting-to-the-database}

在Java代码中，使用DataSourcePool服务获取您创建的配置的`javax.sql.DataSource`对象。 DataSourcePool服务提供了`getDataSource`方法，该方法为给定数据源名称返回`DataSource`对象。 作为方法参数，使用您为JDBC连接池配置指定的数据源名称（或`datasource.name`）属性的值。

以下示例JSP代码获取hsqldbds数据源的一个实例，执行简单的SQL查询，并显示返回的结果数。

#### 执行数据库查找{#jsp-that-performs-a-database-lookup}的JSP

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"%><%
%><%@ page import="com.day.commons.datasource.poolservice.DataSourcePool" %><%
%><%@ page import="javax.sql.DataSource" %><%
%><%@ page import="java.sql.Connection" %><%
%><%@ page import="java.sql.SQLException" %><%
%><%@ page import="java.sql.Statement" %><%
%><%@ page import="java.sql.ResultSet"%><%
%><html>
<cq:include script="head.jsp"/>
<body>
<%DataSourcePool dspService = sling.getService(DataSourcePool.class);
  try {
     DataSource ds = (DataSource) dspService.getDataSource("hsqldbds");
     if(ds != null) {
         %><p>Obtained the datasource!</p><%
         %><%final Connection connection = ds.getConnection();
          final Statement statement = connection.createStatement();
          final ResultSet resultSet = statement.executeQuery("SELECT * from INFORMATION_SCHEMA.SYSTEM_USERS");
          int r=0;
          while(resultSet.next()){
             r=r+1;
          }
          resultSet.close();
          %><p>Number of results: <%=r%></p><%
      }
   }catch (Exception e) {
        %><p>error! <%=e.getMessage()%></p><%
    }
%></body>
</html>
```

>[!NOTE]
>
>如果由于找不到数据源而引发getDataSource方法异常，请确保连接池服务配置正确。 验证属性名称、值和数据类型。


>[!NOTE]
>
>要了解如何将DataSourcePool注入到OSGi包中，请参阅[将DataSourcePool服务注入Adobe Experience Manager OSGi包](https://helpx.adobe.com/experience-manager/using/datasourcepool.html)。
