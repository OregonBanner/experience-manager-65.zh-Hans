---
title: SharePoint Connector
seo-title: SharePoint Connector
description: Day JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013，版本4.0。
seo-description: 了解AEM中的Sharepoint Connector。
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 1%

---

# SharePoint Connector{#sharepoint-connector}

本文包括有关AdobeJCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013版本4.0的详细信息。

SharePoint连接器支持以下基本功能：

* 从SharePoint中读取内容和元数据。
* 通过应用本机SharePoint身份验证和授权，确认已访问内容的SharePoint安全设置
* 使用内容查找器进行内容集成
* 使用AEM组件（如外部资源）显示SharePoint图像和视频
* 将SharePoint与AEM Assets同步

所有功能都使用本机SharePoint Web服务作为SharePoint内容和服务的界面来实施。

>[!NOTE]
>
>AEM 6.1 Service Pack 2也支持SharePoint Connector。 连接器不再支持虚拟存储库装载，因此无法装载。 如果要使用Java API访问Sharepoint存储库，请在您的项目中使用Sharepoint连接器的JCR存储库实施。
>
>SharePoint服务器和相关IT基础架构的安装、配置、管理和IT操作不在本文档的范围之内。 有关这些主题的信息，请参阅[SharePoint](https://www.microsoft.com/sharepoint)上的供应商文档。 连接器要求正确安装、配置和操作基础架构的这些部分。


## 入门 {#getting-started}

要开始使用连接器，请执行以下操作：

* 确保至少安装了Java 7。
* 从Software Distribution下载连接器软件包分发文件。
* 将有效的&#x200B;*license.properties*&#x200B;文件复制到包含&#x200B;*cq-quickstart-6.4.0.jar*&#x200B;文件的目录中。

* 双击/点按.jar文件以启动AEM，或从命令行启动它。
* 从包管理器安装连接器包。
* 配置连接器选项。

## 安装SharePoint连接器{#installing-sharepoint-connector}

连接器是便于安装的内容包。 使用包管理器安装包，然后设置SharePoint服务器URL
和其他配置选项。 SharePoint内容在AEM存储库中可用。

### 安装要求{#installation-requirements}

连接器需要：

* Java运行时环境1.7或更高版本
* SharePoint Web服务可通过网络提供
* SharePoint服务器URL
* CRX和SharePoint存储库的用户凭据和权限
* [支持的平台](#supported-platforms)

可以从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673)下载SharePoint连接器。

### 支持的平台 {#supported-platforms}

该连接器支持以下功能：

* AEM版本：

   * AEM 6.4、6.3

* Microsoft SharePoint版本：

   * Microsoft Office SharePoint Server(MOSS)2010
   * Microsoft Office SharePoint Server(MOSS)2013

* 如果您需要支持连接器的自定义部署（OEM、特殊要求、自定义身份验证方法），请联系您所在地区的Adobe办公室。

>[!NOTE]
>
>连接器仅支持Microsoft官方支持的配置。 请参阅[MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx)和[MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx)系统要求。

### 标准安装{#standard-installation}

Software Distribution用于分发产品功能、示例和热修复程序。 有关详细信息，请参阅[Software Distribution文档](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution)。


#### 与AEM {#integrating-with-aem}集成

安装连接器内容包。

1. 打开Adobe支持票证以请求连接器功能。
1. 在包可用时下载该包，然后为您的AEM实例打开包管理器。
1. 点按/单击包描述页面中的&#x200B;**Install**。
1. 在&#x200B;**安装包**&#x200B;对话框中，点按/单击&#x200B;**安装**。

   **注意**:确保您以管理员身份登录。

1. 安装包后，点按/单击&#x200B;**关闭**。

## 配置SharePoint连接器{#configuring-sharepoint-connector}

安装SharePoint连接器后，请为该连接器配置应用程序和SharePoint层。

设置SharePoint服务器URL以使您的SharePoint存储库JCR兼容。 您可以设置其他参数来配置与SharePoint服务器的连接。 此外，还应使用SharePoint连接器配置身份验证。

### 配置与SharePoint服务器{#configuring-the-connection-with-the-sharepoint-server}的连接

要设置SharePoint服务器的URL和高级选项，请执行以下步骤：

1. 导航到OSGi管理控制台：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索&#x200B;**Day JCR Connector for Microsoft Sharepoint**&#x200B;包。
1. 编辑配置值。
1. 将SharePoint服务器URL设置为&#x200B;**Workspaces**&#x200B;的值。
1. 点按/单击&#x200B;**Save**。

![chlimage_1-62](assets/chlimage_1-62.png)

“工作区”和“默认工作区名称”参数：

默认情况下，连接器会公开单个JCR工作区。 此工作区公开的SharePoint服务器通过“Sharepoint Server URL”配置参数进行设置。

连接器还可以配置为多个工作区。 在这种情况下，每个工作区都与通过工作区公开的相应SharePoint服务器的URL相关联。 要添加工作区，请向Workspaces参数中添加工作区定义。 工作区定义具有以下格式：
`<name>`= `<url>`，其中
`<name>`是JCR工作区的名称，
`<url>`是该工作区的SharePoint服务器URL。

在AEM中，除上述配置步骤外，再执行一步。 允许列表“**com.day.cq.dam.cq-dam-jcr-connectors**”包。

要在AEM中允许列表包，请执行以下步骤：

1. 导航到OSGi管理控制台：http://localhost:4502/system/console/configMgr。
1. 搜索“Apache Sling登录管理员白名单”服务。
1. 选择&#x200B;**绕过白名单**。
1. 在白名单包中添加默认的`com.day.cq.dam.cq-dam-jcr-connectors`
1. 单击保存。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>如果配置多个工作区，请在默认工作区名称参数中指定默认工作区的名称。

有关与身份验证相关的参数的其他信息，请参阅[Authentication](/help/sites-administering/sharepoint-connector.md#configuring-authentication)。

### 验证Sharepoint设置{#verifying-the-sharepoint-setup}

配置连接器后，验证以下内容：

* SharePoint服务器运行，并且Web服务可供连接器实例访问
* SharePoint用户凭据有效，且用户具有必要的SharePoint权限
* 连接器已正确安装和配置

### 配置与SharePoint服务器{#configuring-dam-sync-with-the-sharepoint-server}的DAM同步

要将SharePoint Assets与AEM同步，请执行以下步骤：

1. 导航到OSGi管理控制台：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索“默认DAMAssetSynchronization”服务。
1. 编辑配置值。
1. 在SharePoint网站上设置有权访问的用户的用户名和相应的密码。
1. 单击保存。

启用DAM同步服务，默认情况下处于禁用状态：

1. 导航到OSGi Web控制台组件：[http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. 搜索“com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService”。
1. 单击启用。

（可选）您可以配置不同同步周期之间的同步延迟：

1. 导航到OSGi管理控制台：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. 搜索“DAY CQ DAM JCR连接器资产同步服务”。
1. 编辑配置值。
1. 设置同步时段的值（以秒为单位）。
1. 单击保存。

### 配置身份验证{#configuring-authentication}

Sharepoint包括经典身份验证和基于声明的身份验证方法，这两种方法都支持以下身份验证类型：

* 基本
* Forms

具体而言，可以使用以下类型的身份验证：

* 经典 — 基本
* 基于经典Forms
* 索赔 — 基本
* 基于索赔的Forms

AEM JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013版本4.0支持基于声明的身份验证（Microsoft建议使用此功能），该身份验证以下模式运行：

* **基本/NTLM身份验证**:连接器首先尝试使用基本身份验证进行连接。如果不可用，则切换到基于NTLM的身份验证。
* **基于Forms的身份验证**:Sharepoint根据用户在登录表单（通常是网页）中键入的凭据来验证用户。系统为经过身份验证的请求发出令牌，该令牌包含用于为后续请求重新建立标识的密钥。

**配置基于Forms的身份验证**

转到：[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. 单击OSGI ->配置
1. 搜索“Day JCR Connector for Microsoft Sharepoint”
1. 单击“编辑配置值”
1. 将“Sharepoint连接工厂”的值设置为“com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory”
1. 单击&#x200B;**保存**。

**配置基本身份验证(Windows)**

1. [禁用令牌身份验证](#disable-token-authentication)。
1. 转到[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)。
1. 单击OSGI >配置。
1. 搜索&#x200B;**Day JCR Connector for Microsoft Sharepoint**。
1. 单击 `Edit the configuration values`.
1. 将Sharepoint连接工厂的值设置为`com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`。
1. 单击&#x200B;**保存**。

只有在AEM和SharePoint上通过身份验证的用户才能通过连接器访问SharePoint内容。

您还可以使用连接器扩展进行身份验证来创建自定义身份验证模块，例如，将AEM用户的访问权限映射到特定SharePoint用户。 创建与SharePoint用户（用户名和密码应匹配）对应的AEM用户，以便能够查看映射到连接器实例的SharePoint内容。

要在AEM中创建用户，请执行以下操作：

1. 登录http://localhost:9502/with管理员用户。
1. 单击“工具”。
1. 单击“安全”。
1. 单击用户。
1. 单击&#x200B;**创建用户**。
1. 提供用户ID（在SharePoint上具有访问权限的用户名）。
1. 提供相应的密码。
1. 单击绿色勾号以创建用户。

要在管理员组中添加用户，请执行以下操作：

1. 转到“组管理”。
1. 单击“a”节点。
1. 单击“管理员”。
1. 在&#x200B;**Browse**&#x200B;按钮之前的文本框中键入上面创建的用户ID。
1. 单击绿色勾号将用户添加到管理员组。

### 禁用令牌身份验证{#disable-token-authentication}

1. 下载并安装包`basic auth`。 `zip` 从Software Distribution。

1. 关闭快速启动。
1. 打开文件&#x200B;*\crx-quickstart\repository\repository.xml*。
1. 查找标记`<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. 将标记`<param name="disableTokenAuth" value="true"/>`插入步骤4中所述的标记中。
1. 保存并关闭xml文件。
1. 重新启动快速入门，然后使用您的凭据登录。

#### 支持SharePoint服务器{#supporting-different-authentication-methods-of-the-sharepoint-server}的不同身份验证方法

在其标准版本中，连接器支持标准IIS **Windows**&#x200B;身份验证（基本）和基于Forms的身份验证（基于令牌）。 可通过扩展性机制支持[其他身份验证方法](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2)。

以下步骤提供了有关扩展标准身份验证以支持SharePoint服务器的各种身份验证方法的准则：

1. 实施`com.day.crx.spi.sharepoint.security.SharepointConnectionFactory`以处理特定身份验证过程的客户端。
1. 将`SharepointConnectionFactory`实施安装为具有片段主机`com.day.crx.spi.crx2sharepoint-bundle`的片段包。

   使用Maven时，请根据项目的要求调整以下`maven-bundle-plugin`配置：

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. 在连接器配置中注册`SharepointConnectionFactory`实施。 在连接器的配置窗口中，单击&#x200B;**高级选项**。 在&#x200B;**Sharepoint连接工厂**&#x200B;字段中，指定实施的名称`com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`。

1. 重新启动连接器。
