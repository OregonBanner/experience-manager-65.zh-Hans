---
title: 应用程序服务器安装
seo-title: Application Server Install
description: 了解如何在应用程序服务器中安装AEM。
seo-description: Learn how to install AEM with an application server.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# 应用程序服务器安装{#application-server-install}

>[!NOTE]
>
>`JAR` 和 `WAR` 是AEM发布时所用的文件类型。 这些格式正在进行质量保证，以满足Adobe承诺的支持级别。

本节将介绍如何通过应用程序服务器安装Adobe Experience Manager (AEM)。 请参阅 [支持的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 部分，以了解为各个应用程序服务器提供的特定支持级别。

以下应用程序服务器的安装步骤已说明：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [oracleWebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

有关安装Web应用程序、服务器配置以及如何启动和停止服务器的详细信息，请参阅相应的应用程序服务器文档。

>[!NOTE]
>
>如果您在WAR部署中使用Dynamic Media，请参阅 [Dynamic Media文档](/help/assets/config-dynamic.md#enabling-dynamic-media).

## 常规描述 {#general-description}

### 在应用程序服务器中安装AEM时的默认行为 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM只提供一个war文件来进行部署。

如果部署，则默认情况下会发生以下情况：

* 运行模式为 `author`
* 实例（存储库、Felix OSGI环境、捆绑包等） 安装在 `${user.dir}/crx-quickstart`位置 `${user.dir}` 是当前工作目录，将调用crx-quickstart的此路径 `sling.home`

* 上下文根目录是war文件名，例如： `aem-6`

#### 配置 {#configuration}

您可以通过以下方式更改默认行为：

* 运行模式：配置 `sling.run.modes` 中的参数 `WEB-INF/web.xml` 部署前的AEM war文件

* sling.home：配置 `sling.home` 中的参数 `WEB-INF/web.xml`部署前的AEM war文件

* 上下文根：重命名AEM war文件

#### 发布安装 {#publish-installation}

要部署发布实例，您需要将运行模式设置为发布：

* 从AEM war文件中解压缩WEB-INF/web.xml
* 将sling.run.modes参数更改为发布
* 将web.xml文件重新打包到AEM war文件中
* 部署AEM war文件

#### 安装检查 {#installation-check}

要检查是否已安装所有组件，您可以：

* 跟踪 `error.log`文件，以查看是否已安装所有内容
* 查看 `/system/console` 已安装所有包

#### 同一应用程序服务器上的两个实例 {#two-instances-on-the-same-application-server}

出于演示目的，可以将创作实例和发布实例安装在一个应用程序服务器中。 为此，请执行以下操作：

1. 更改发布实例的sling.home变量和sling.run.modes变量。
1. 从AEM war文件中解压缩WEB-INF/web.xml文件。
1. 将sling.home参数更改为其他路径（可以使用绝对路径和相对路径）。
1. 将sling.run.modes更改为发布实例的发布。
1. 重新打包web.xml文件。
1. 重命名war文件，使其具有不同的名称：例如，一个重命名为aemauthor.war，另一个重命名为aempublish.war。
1. 使用更高的内存设置，例如，默认AEM实例使用 — Xmx3072m
1. 部署两个Web应用程序。
1. 部署后，停止两个Web应用程序。
1. 在创作实例和发布实例中，均确保在sling.properties文件中，属性felix.service.urlhandlers=false设置为false（默认设置为true）。
1. 再次启动两个Web应用程序。

## 应用程序服务器安装过程 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

在部署之前，请阅读 [常规描述](#general-description) 上面。

**服务器准备**

* 让基本身份验证标头通过：

   * 允许AEM对用户进行身份验证的一种方法是禁用WebSphere服务器的全局管理安全性，方法是转到“安全性” — >“全局安全性”，然后取消选中“启用管理安全性”复选框，保存并重新启动服务器。

* set `"JAVA_OPTS= -Xmx2048m"`
* 如果要使用上下文根= /安装AEM，则必须首先更改现有默认Web应用程序的上下文根

**部署AEM Web应用程序**

* 下载AEM war文件
* 如果需要，在web.xml中进行配置（请参阅上面的“一般说明”）

   * 解包WEB-INF/web.xml文件
   * 将sling.run.modes参数更改为发布
   * 取消对sling.home初始参数的注释，并根据需要设置此路径
   * 重新打包web.xml文件

* 部署AEM war文件

   * 选择上下文根目录（如果要设置sling运行模式，则需要选择部署向导的详细步骤，然后在向导的步骤6中指定它）

* 启动AEM Web应用程序

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

在部署之前，请阅读 [常规描述](#general-description) 上面。

**准备JBoss服务器**

在conf文件中设置内存参数(例如 `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果您使用的部署扫描程序来安装AEM Web应用程序，则增加 `deployment-timeout,` 对于该集 `deployment-timeout` 实例的xml文件中的属性(例如 `configuration/standalone.xml)`：

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEM Web应用程序**

* 在JBoss管理控制台中上传AEM Web应用程序。

* 启用AEM Web应用程序。

#### oracleWebLogic 12.1.3/12.2 {#oracle-weblogic}

在部署之前，请阅读 [常规描述](#general-description) 上面。

该配置使用仅具有管理服务器的简单服务器布局。

**WebLogic服务器准备**

* In `${myDomain}/config/config.xml`添加到security-configuration部分：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 查看日期 [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) 正确的位置（默认情况下，将其定位在部分的末尾即可）

* 增加VM内存设置：

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp .sh)搜索WLS_MEM_ARGS，设置例如 `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新启动WebLogic Server

* 在中创建 `${myDomain}` 包文件夹，cq文件夹内和计划文件夹内

**部署AEM Web应用程序**

* 下载AEM war文件
* 将AEM war文件放入${myDomain}/packages/cq文件夹中
* 在中进行配置 `WEB-INF/web.xml` 如果需要（请参阅上文“一般说明”中的）

   * 解包 `WEB-INF/web.xml`文件
   * 将sling.run.modes参数更改为发布
   * 取消对sling.home初始参数的注释，并根据需要设置此路径（请参阅常规描述）
   * 重新打包web.xml文件

* 将AEM war文件部署为应用程序（对于其他设置，使用默认设置）
* 安装可能需要一些时间……
* 检查安装是否已完成，如一般说明中所述（例如，跟踪error.log）
* 可以在WebLogic的Web应用程序的“配置”选项卡中更改上下文根目录 `/console`

#### Tomcat 8/8.5 {#tomcat}

在部署之前，请阅读 [常规描述](#general-description) 上面。

* **准备Tomcat服务器**

   * 增加VM内存设置：

      * In `bin/catalina.bat` (响应 `catalina.sh` 在unix上)添加以下设置：
      * `set "JAVA_OPTS= -Xmx2048m`
   * 在安装时，Tomcat不启用管理员或管理员访问权限。 因此，您必须手动编辑 `tomcat-users.xml` 要允许这些帐户访问，请执行以下操作：

      * 编辑 `tomcat-users.xml` 以包括管理员和经理的访问权限。 该配置应类似于以下示例：

         ```xml
         <?xml version='1.0' encoding='utf-8'?>
         <tomcat-users>
         role rolename="manager"/>
         role rolename="tomcat"/>
         <role rolename="admin"/>
         <role rolename="role1"/>
         <role rolename="manager-gui"/>
         <user username="both" password="tomcat" roles="tomcat,role1"/>
         <user username="tomcat" password="tomcat" roles="tomcat"/>
         <user username="admin" password="admin" roles="admin,manager-gui"/>
         <user username="role1" password="tomcat" roles="role1"/>
         </tomcat-users>
         ```
   * 如果要使用上下文根“/”部署AEM，则必须更改现有ROOT Web应用程序的上下文根：

      * 停止和取消部署ROOT Web应用程序
      * 重命名tomcat webapps文件夹中的ROOT.war文件夹
      * 再次启动Web应用程序
   * 如果使用管理器gui安装AEM Web应用程序，则需要增加已上传文件的最大大小，因为默认仅允许50MB上传大小。 对于打开管理器Web应用程序的web.xml，

      `webapps/manager/WEB-INF/web.xml`

      并将max-file-size和max-request-size增加到至少500MB，请参见以下内容 `multipart-config` 此类的示例 `web.xml` 文件。

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **部署AEM Web应用程序**

   * 下载AEM war文件
   * 如果需要，在web.xml中进行配置（请参阅上面的“一般说明”）

      * 解包WEB-INF/web.xml文件
      * 将sling.run.modes参数更改为发布
      * 取消对sling.home初始参数的注释，并根据需要设置此路径
      * 重新打包web.xml文件
   * 将AEM war文件重命名为ROOT.war如果要将其部署为根Web应用程序，请将其重命名为aemauthor.war例如，如果要将aemauthor作为上下文根
   * 将其复制到tomcat的webapps文件夹中
   * 等待安装AEM


## 疑难解答 {#troubleshooting}

有关处理安装过程中可能出现的问题的信息，请参阅：

* [疑难解答](/help/sites-deploying/troubleshooting.md)
