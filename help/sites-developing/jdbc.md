---
title: 连接到SQL数据库
seo-title: Connecting to SQL Databases
description: 访问外部SQL数据库，以便AEM应用程序可以与数据交互
seo-description: Access an external SQL database to so that your AEM applications can interact with the data
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
source-git-commit: e147605ff4d5c3d2403632285956559db235c084
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# 连接到SQL数据库{#connecting-to-sql-databases}

访问外部SQL数据库，以便CQ应用程序可以与数据交互：

1. [创建或获取用于导出JDBC驱动程序包的OSGi包](#bundling-the-jdbc-database-driver).
1. [配置JDBC数据源池提供程序](#configuring-the-jdbc-connection-pool-service).
1. [获取数据源对象并在代码中创建连接](#connecting-to-the-database).

## 捆绑JDBC数据库驱动程序 {#bundling-the-jdbc-database-driver}

例如，一些数据库供应商在OSGi捆绑包中提供JDBC驱动程序 [MySQL](https://dev.mysql.com/downloads/connector/j/). 如果数据库的JDBC驱动程序不能作为OSGi捆绑包使用，请获取驱动程序JAR并将其包装在OSGi捆绑包中。 捆绑包必须导出与数据库服务器交互所需的包。 捆绑包还必须导入它引用的包。

以下示例使用 [适用于Maven的捆绑包插件](https://felix.apache.org/documentation/subprojects/apache-felix-maven-bundle-plugin-bnd.html) 将HSQLDB驱动程序封装在OSGi包中。 POM指示插件嵌入标识为依赖项的hsqldb.jar文件。 所有org.hsqldb包均已导出。

该插件会自动确定要导入的包，并在包的MANIFEST.MF文件中列出这些包。 如果CQ服务器上没有任何软件包，则安装时不会启动捆绑包。 两种可能的解决方案如下：

* 在POM中指明包是可选的。 当JDBC连接实际上不需要软件包成员时，可使用此解决方案。 使用Import-Package元素来指示可选软件包，如下例所示：

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* 将包含包的JAR文件包装在用于导出包的OSGi捆绑包中，并部署该捆绑包。 当代码执行期间需要包成员时，请使用此解决方案。

了解源代码后，您可以决定使用哪个解决方案。 您还可以尝试任一解决方案并执行测试以验证解决方案。

### 捆绑了hsqldb.jar的POM {#pom-that-bundles-hsqldb-jar}

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

以下链接可打开某些常用数据库产品的下载页：

* [Microsoft® SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)
* [IBM® DB2®](https://www.ibm.com/support/pages/download-db2-fix-packs-version-db2-linux-unix-and-windows)

### 配置JDBC连接池服务 {#configuring-the-jdbc-connection-pool-service}

为使用JDBC驱动程序创建数据源对象的JDBC连接池服务添加配置。 您的应用程序代码使用此服务来获取对象并连接到数据库。

JDBC连接池( `com.day.commons.datasource.jdbcpool.JdbcPoolService`)是工厂服务。 如果需要使用不同属性（例如只读或读/写访问）的连接，请创建多个配置。

使用CQ时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整的详细信息。

以下属性可用于配置池连接服务。 资产名称在Web控制台中按其显示方式列出。 对应的名称 `sling:OsgiConfig` 节点显示在括号中。 对于HSQLDB服务器和别名为 `mydb`：

* JDBC驱动程序类( `jdbc.driver.class`)：要使用的实现java.sql.Driver接口的Java™类，例如 `org.hsqldb.jdbc.JDBCDriver`. 数据类型是 `String`.

* JDBC连接URI ( `jdbc.connection.uri`)：用于创建连接的URL，例如 `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. URL的格式必须对java.sql.DriverManager类的getConnection方法有效。 数据类型是 `String`.

* 用户名( `jdbc.username`)：用于向数据库服务器进行身份验证的用户名。 数据类型是 `String`.

* 密码( `jdbc.password`)：用于用户身份验证的密码。 数据类型是 `String`.

* 验证查询( `jdbc.validation.query`)：用于验证连接是否成功的SQL语句，例如 `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. 数据类型是 `String`.

* 默认只读(default.readonly)：如果希望连接提供只读访问，请选择此选项。 数据类型是 `Boolean`.
* 默认自动提交( `default.autocommit`)：选择此选项可以为发送到数据库的每个SQL命令创建单独的事务，并且每个事务都会自动提交。 在代码中明确提交事务时，请勿选择此选项。 数据类型是 `Boolean`.

* 池大小( `pool.size`)：可供数据库使用的同时连接数。 数据类型是 `Long`.

* 池等待( `pool.max.wait.msec`)：连接请求超时之前经过的时间。 数据类型是 `Long`.

* 数据源名称( `datasource.name`)：此数据源的名称。 数据类型是 `String`.

* 其他服务属性( `datasource.svc.properties`)：要附加到连接URL的一组名称/值对。 数据类型是 `String[]`.

JDBC连接池服务是一个工厂。 因此，如果您使用 `sling:OsgiConfig` 节点要配置连接服务，节点的名称必须包含工厂服务PID，后跟一个 *`-alias`*. 您使用的别名对于该PID的所有配置节点必须是唯一的。 示例节点名称为 `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### 连接到数据库 {#connecting-to-the-database}

在Java™代码中，使用DataSourcePool服务获取 `javax.sql.DataSource` 您创建的配置的对象。 DataSourcePool服务提供 `getDataSource` 返回值的方法 `DataSource` 指定数据源名称的对象。 作为方法参数，使用数据源名称的值(或 `datasource.name`)属性，该属性为JDBC连接池配置指定。

以下示例JSP代码获取hsqldbds数据源的实例，执行简单的SQL查询，并显示返回的结果数。

#### 执行数据库查找的JSP {#jsp-that-performs-a-database-lookup}

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
>如果getDataSource方法由于未找到数据源而引发异常，请确保连接池服务配置正确。 验证属性名称、值和数据类型。

<!-- Link below redirects to the "Get started with AEM Sites - WKND tutorial"
>[!NOTE]
>
>To learn how to inject a DataSourcePool into an OSGi bundle, see [Injecting a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html). -->
