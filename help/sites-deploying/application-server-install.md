---
title: 应用程序服务器安装
seo-title: 应用程序服务器安装
description: 了解如何与应用程序服务器一起安装AEM。
seo-description: 了解如何与应用程序服务器一起安装AEM。
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: 0a082d3cff66b82ef6de551a735a16a001446a1e
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# 应用程序服务器安装{#application-server-install}

>[!NOTE]
>
>`JAR` 以 `WAR` 及AEM是否在中发布文件类型。 这些格式正在进行质量保证，以满足Adobe承诺的支持级别。


本节将告诉您如何将Adobe Experience Manager(AEM)与应用程序服务器一起安装。 请查阅支 [持的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) (Supported Platforms)部分，了解为各个应用程序服务器提供的特定支持级别。

介绍了以下应用程序服务器的安装步骤：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

有关安装Web应用程序、服务器配置以及如何开始和停止服务器的详细信息，请查阅相应的应用程序服务器文档。

>[!NOTE]
>
>如果您在WAR部署中使用Dynamic Media，请参阅 [Dynamic Media文档](/help/assets/config-dynamic.md#enabling-dynamic-media)。

## 一般说明 {#general-description}

### 在应用程序服务器中安装AEM时的默认行为 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM是一个要部署的战争文件。

如果部署了以下内容，则默认情况下会发生：

* 运行模式为 `author`
* 实例(存储库、Felix OSGI环境、捆绑包等) 安装在 `${user.dir}/crx-quickstart`当前 `${user.dir}` 工作目录中，此crx-quickstart路径称为 `sling.home`

* 上下文根是war文件名，例如： `aem-6`

#### 配置 {#configuration}

可以通过以下方式更改默认行为：

* 运行模式：在部署 `sling.run.modes` 之前，在AEM `WEB-INF/web.xml` war文件的文件中配置参数

* sling.home:在部署 `sling.home` 前在AEM `WEB-INF/web.xml`war文件的文件中配置参数

* 上下文根：重命名AEM war文件

#### 发布安装 {#publish-installation}

要部署发布实例，您需要设置要发布的运行模式：

* 从AEM war文件解压缩WEB-INF/web.xml文件
* 将sling.run.modes参数更改为发布
* 将web.xml文件重新打包到AEM war文件
* 部署AEM war文件

#### 安装检查 {#installation-check}

要检查是否已安装全部：

* 跟踪文 `error.log`件，以查看是否已安装所有内容
* 查看 `/system/console` 所有捆绑包

#### 同一应用程序服务器上的两个实例 {#two-instances-on-the-same-application-server}

出于演示目的，可以在一台应用程序服务器中安装作者实例和发布实例。 为此，请执行以下操作：

1. 更改发布实例的sling.home变量和sling.run.modes变量。
1. 从AEM war文件解压缩WEB-INF/web.xml文件。
1. 将sling.home参数更改为其他路径（可以使用绝对路径和相对路径）。
1. 将sling.run.modes更改为发布实例。
1. 重新打包web.xml文件。
1. 重命名war文件，使它们具有不同的名称：例如，一个重命名为aemmauthor.war，另一个重命名为aempublish.war。
1. 使用较高的内存设置，例如，对于默认AEM实例，请使用如：-Xmx3072m
1. 部署两个Web应用程序。
1. 部署后停止两个Web应用程序。
1. 在作者实例和发布实例中，确保在sling.properties文件中，属性felix.service.urlhandlers=false设置为false（默认设置为true）。
1. 再次开始两个Web应用程序。

## 应用程序服务器安装过程 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

部署前，请阅读上 [面的常规](#general-description) 说明。

**服务器准备**

* 让基本身份验证头传递：

   * 让AEM对用户进行身份验证的一种方法是禁用WebSphere服务器的全局管理安全性，这样做：转至“安全”->“全局安全”并取消选中“启用管理安全”复选框，保存并重新启动服务器。

* 设置 `"JAVA_OPTS= -Xmx2048m"`
* 如果要使用上下文根= /安装AEM，则必须先更改现有默认Web应用程序的上下文根

**部署AEM Web应用程序**

* 下载AEM war文件
* 根据需要在web.xml中进行配置（请参阅上面的“常规”说明）

   * 解压缩WEB-INF/web.xml文件
   * 更改sling.run.modes参数以进行发布
   * 取消注释sling.home初始参数，根据需要设置此路径
   * 重复web.xml文件

* 部署AEM war文件

   * 选择上下文根目录（如果要设置部署向导的详细步骤，则需要设置sling运行模式，然后在向导的第6步中指定）

* 开始AEM web应用程序

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

部署前，请阅读上 [面的常规](#general-description) 说明。

**准备JBoss服务器**

在会议文件中设置内存参数(例如， `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果您使用deployment-scanner安装AEM web应用程序，则最好在实例的xml `deployment-timeout,` 文件中 `deployment-timeout` 增加该属性的设置(例如 `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEM Web应用程序**

* 在JBoss管理控制台中上传AEM Web应用程序。

* 启用AEM Web应用程序。

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

部署前，请阅读上 [面的常规](#general-description) 说明。

它仅对管理服务器使用简单的服务器布局。

**WebLogic服务器准备**

* 在 `${myDomain}/config/config.xml`添加到安全配置部分中：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 请参 [阅https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) ，了解正确的位置（默认情况下，将其放置在节的末尾是可以的）

* 增加虚拟机内存设置：

   * 打 `${myDomain}/bin/setDomainEnv.cmd` 开(resp .sh)搜索WLS_MEM_ARGS，设置（如集） `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新启动WebLogic服务器

* 在包文 `${myDomain}` 件夹中、cq文件夹中以及计划文件夹中创建

**部署AEM Web应用程序**

* 下载AEM war文件
* 将AEM war文件放入${myDomain}/packages/cq文件夹中
* 根据需要进 `WEB-INF/web.xml` 行配置（请参阅上面的“常规”说明）

   * 解压文 `WEB-INF/web.xml`件
   * 更改sling.run.modes参数以进行发布
   * 取消sling.home初始参数注释，并根据需要设置此路径（请参阅常规说明）
   * 重复web.xml文件

* 将AEM war文件部署为应用程序（对于其他设置，请使用默认设置）
* 安装可能需要时间……
* 检查如上“General Description（常规说明）”中所述的安装是否已完成（例如，跟踪error.log）
* 您可以在WebLogic中更改Web应用程序的“配置”选项卡中的上下文根 `/console`

#### Tomcat 8/8.5 {#tomcat}

部署前，请阅读上 [面的常规](#general-description) 说明。

* **准备Tomcat服务器**

   * 增加虚拟机内存设置：

      * 在( `bin/catalina.bat` 在unix `catalina.sh` 上响应)中，添加以下设置：
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat在安装时不允许管理员和管理者访问。 因此，您必须手动编辑才 `tomcat-users.xml` 能允许访问这些帐户：

      * 编辑 `tomcat-users.xml` 以包含管理员和管理者的访问权限。 配置应类似于以下示例：

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
      * 重命名tomcat的webapps文件夹中的ROOT.war文件夹
      * 开始Web应用程序
   * 如果使用manager-gui安装AEM Web应用程序，则需要增加已上载文件的最大大小，因为默认情况下只允许50MB的上载大小。 要打开管理器Web应用程序的web.xml,

      `webapps/manager/WEB-INF/web.xml`

      并将max-file-size和max-request-size增加到至少500MB，请参见此类 `multipart-config` 文件的以下示 `web.xml` 例。

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
   * 根据需要在web.xml中进行配置（请参阅上面的“常规”说明）

      * 解压缩WEB-INF/web.xml文件
      * 更改sling.run.modes参数以进行发布
      * 取消注释sling.home初始参数，根据需要设置此路径
      * 重复web.xml文件
   * 如果您希望将AEM war文件作为根Web应用程序部署，请将其重命名为ROOT.war，如果您希望将aemauthor作为上下文根文件，则将其重命名为eamuthor.war
   * 将其复制到tomcat的webapps文件夹中
   * 等到AEM安装完毕


## 疑难解答 {#troubleshooting}

有关处理安装过程中可能出现的问题的信息，请参阅：

* [疑难解答](/help/sites-deploying/troubleshooting.md)
