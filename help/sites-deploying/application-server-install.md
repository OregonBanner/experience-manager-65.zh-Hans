---
title: 应用程序服务器安装
seo-title: 应用程序服务器安装
description: 了解如何使用应用程序服务器安装AEM。
seo-description: 了解如何使用应用程序服务器安装AEM。
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---

# 应用程序服务器安装{#application-server-install}

>[!NOTE]
>
>`JAR` 和 `WAR` 中是否发布了AEM文件类型。这些格式正在进行质量保证，以满足Adobe承诺的支持级别。


本节将介绍如何使用应用程序服务器来安装Adobe Experience Manager(AEM)。 请参阅[支持的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)部分，查看为各个应用程序服务器提供的特定支持级别。

下列应用程序服务器的安装步骤如下：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [OracleWebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

有关安装Web应用程序、服务器配置以及如何启动和停止服务器的详细信息，请参阅相应的应用程序服务器文档。

>[!NOTE]
>
>如果您在WAR部署中使用Dynamic Media，请参阅[Dynamic Media文档](/help/assets/config-dynamic.md#enabling-dynamic-media)。

## 常规说明{#general-description}

### 在应用程序服务器{#default-behaviour-when-installing-aem-in-an-application-server}中安装AEM时的默认行为

AEM是一个要部署的战争文件。

如果部署了，则默认情况下会发生以下情况：

* 运行模式为`author`
* 实例（存储库、Felix OSGi环境、包等） 安装在`${user.dir}/crx-quickstart`中，其中`${user.dir}`是当前工作目录，此crx-quickstart路径称为`sling.home`

* 上下文根目录是war文件名，例如：`aem-6`

#### 配置 {#configuration}

您可以通过以下方式更改默认行为：

* 运行模式：在部署前在AEM战争文件的`WEB-INF/web.xml`文件中配置`sling.run.modes`参数

* sling.home:在部署前在AEM战争文件的`WEB-INF/web.xml`文件中配置`sling.home`参数

* 上下文根：重命名AEM战争文件

#### 发布安装{#publish-installation}

要部署发布实例，您需要设置要发布的运行模式：

* 从AEM战争文件中解包WEB-INF/web.xml文件
* 将sling.run.modes参数更改为publish
* 将web.xml文件重新编写到AEM战争文件
* 部署AEM战争文件

#### 安装检查{#installation-check}

要检查是否已安装全部：

* 跟踪`error.log`文件，以查看是否已安装所有内容
* 在`/system/console`中查看所有包都已安装

#### 同一应用程序服务器上的两个实例{#two-instances-on-the-same-application-server}

出于演示目的，可以在一个应用程序服务器中安装作者和发布实例。 为此，请执行以下操作：

1. 更改发布实例的sling.home变量和sling.run.modes变量。
1. 从AEM War文件中解压缩WEB-INF/web.xml文件。
1. 将sling.home参数更改为其他路径（可以使用绝对路径和相对路径）。
1. 将sling.run.modes更改为发布实例的。
1. 重新编写web.xml文件。
1. 重命名战争文件，以便它们具有不同的名称：例如，一个重命名为aemauthor.war，另一个重命名为aempublish.war。
1. 使用较高的内存设置，例如，对于默认的AEM实例，使用：-Xmx3072米
1. 部署两个Web应用程序。
1. 部署后，停止两个Web应用程序。
1. 在创作实例和发布实例中，确保在sling.properties文件中，属性felix.service.urlhandlers=false设置为false（默认情况下，它设置为true）。
1. 再次启动两个Web应用程序。

## 应用程序服务器安装过程{#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

在部署之前，请阅读上面的[常规说明](#general-description)。

**服务器准备**

* 让基本身份验证标头传递：

   * 让AEM验证用户的一种方法是禁用WebSphere服务器的全局管理安全性，以便执行此操作：转到“安全” — >“全局安全”，然后取消选中“启用管理安全”复选框，保存并重新启动服务器。

* set `"JAVA_OPTS= -Xmx2048m"`
* 如果要使用上下文根= /安装AEM，则必须首先更改现有默认Web应用程序的上下文根

**部署AEM Web应用程序**

* 下载AEM战争文件
* 根据需要使用web.xml进行配置（请参阅常规说明中的上文）

   * 解压缩WEB-INF/web.xml文件
   * 更改sling.run.modes参数以发布
   * 取消注释sling.home初始参数，并根据需要设置此路径
   * 修复web.xml文件

* 部署AEM战争文件

   * 选择上下文根（如果要设置Sling运行模式，则需要选择部署向导的详细步骤，然后在向导的步骤6中指定）

* 启动AEM Web应用程序

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

在部署之前，请阅读上面的[常规说明](#general-description)。

**准备JBoss服务器**

在conf文件中设置内存参数(例如，`standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果使用deployment-scanner安装AEM web应用程序，则最好在实例的xml文件中增加`deployment-timeout`属性集的`deployment-timeout,`（例如`configuration/standalone.xml)`）：

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEM Web应用程序**

* 在JBoss管理控制台中上传AEM Web应用程序。

* 启用AEM Web应用程序。

#### OracleWebLogic 12.1.3/12.2 {#oracle-weblogic}

在部署之前，请阅读上面的[常规说明](#general-description)。

它仅使用管理服务器来使用简单的服务器布局。

**WebLogic服务器准备**

* 在`${myDomain}/config/config.xml`中，将添加到安全配置部分：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 请参 [阅https://xmlns.oracle.com/weblogic/domain/1.0/domain.](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsd中的正确位置（默认情况下，将其放置在部分末尾是正常的）

* 增加虚拟机内存设置：

   * 打开`${myDomain}/bin/setDomainEnv.cmd`(resp .sh)搜索WLS_MEM_ARGS，例如设置`WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新启动WebLogic服务器

* 在`${myDomain}`中创建包文件夹，在cq文件夹中创建Plan文件夹

**部署AEM Web应用程序**

* 下载AEM战争文件
* 将AEM战争文件放入${myDomain}/packages/cq文件夹中
* 根据需要在`WEB-INF/web.xml`中进行配置（请参阅常规说明中的上文）

   * 解压缩`WEB-INF/web.xml`文件
   * 更改sling.run.modes参数以发布
   * 取消注释sling.home初始参数，并根据需要设置此路径（请参阅常规描述）
   * 修复web.xml文件

* 将AEM战争文件部署为应用程序（对于其他设置，使用默认设置）
* 安装可能需要时间……
* 检查安装是否已按常规说明中所述完成（例如跟踪error.log）
* 您可以在WebLogic `/console`中更改Web应用程序的“配置”选项卡中的上下文根

#### Tomcat 8/8.5 {#tomcat}

在部署之前，请阅读上面的[常规说明](#general-description)。

* **准备Tomcat服务器**

   * 增加虚拟机内存设置：

      * 在`bin/catalina.bat`（对于unix，响应`catalina.sh`）中，添加以下设置：
      * `set "JAVA_OPTS= -Xmx2048m`
   * 安装时，Tomcat不允许管理员或管理员访问。 因此，您必须手动编辑`tomcat-users.xml`才能允许访问这些帐户：

      * 编辑`tomcat-users.xml`以包含对管理员和管理器的访问权限。 配置应类似于以下示例：

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

      * 停止和取消部署根Web应用程序
      * 在tomcat的Webapps文件夹中重命名ROOT.war文件夹
      * 再次启动Web应用程序
   * 如果使用管理器 — gui安装AEM Web应用程序，则需要增加上载文件的最大大小，因为默认情况下仅允许50MB的上载大小。 要打开管理器Web应用程序的web.xml，

      `webapps/manager/WEB-INF/web.xml`

      并将max-file-size和max-request-size增加到至少500MB，请参阅以下`multipart-config`此类`web.xml`文件的示例。

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **部署AEM Web应用程序**

   * 下载AEM战争文件
   * 根据需要使用web.xml进行配置（请参阅常规说明中的上文）

      * 解压缩WEB-INF/web.xml文件
      * 更改sling.run.modes参数以发布
      * 取消注释sling.home初始参数，并根据需要设置此路径
      * 修复web.xml文件
   * 如果要将AEM war文件作为根Web应用程序部署，请将其重命名为ROOT.war，如果希望将aemothor作为上下文根，则将其重命名为aemauthor.war
   * 将其复制到tomcat的webapps文件夹中
   * 等待安装AEM


## 疑难解答 {#troubleshooting}

有关处理安装过程中可能出现的问题的信息，请参阅：

* [疑难解答](/help/sites-deploying/troubleshooting.md)
