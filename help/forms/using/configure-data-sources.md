---
title: 配置数据源
seo-title: 配置数据源
description: 了解如何配置不同类型的数据源并利用它们创建表单数据模型。
seo-description: 了解如何配置不同类型的数据源并利用它们创建表单数据模型。
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---


# 配置数据源{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms数据集成允许您配置和连接不同的数据源。 现成支持以下类型。 但是，只需少量自定义，您也可以集成其他数据源。

* 关系数据库- MySQL、Microsoft SQL Server、IBM DB2和OracleRDBMS。
* AEM用户用户档案
* REST风格的Web服务
* 基于SOAP的Web服务
* OData服务

数据集成支持OAuth2.0、基本身份验证和API密钥现成身份验证类型，并允许为访问Web服务实现自定义身份验证。 在AEM Cloud Services中配置了RESTful、基于SOAP和OData服务时，在AEM Web控制台中配置关系用户档案库的JDBC和AEM用户的连接器。

## 配置关系数据库{#configure-relational-database}

您可以使用AEM Web Console配置配置关系数据库。 执行以下操作：

1. 转到AEM Web控制台，网址为https://server:host/system/console/configMgr。
1. 查找&#x200B;**[!UICONTROL Apache Sling Connection池化DataSource]**&#x200B;配置。 点击以在编辑模式下打开配置。
1. 在配置对话框中，指定要配置的数据库的详细信息，如：

   * 数据源的名称
   * 存储数据源名称的数据源服务属性
   * JDBC驱动程序的Java类名
   * JDBC连接URI
   * 用于与JDBC驱动程序建立连接的用户名和密码

   >[!NOTE]
   >
   >请确保在配置数据源之前加密敏感信息，如口令。 要加密：
   >
   >    
   >    
   >    1. 转到https://&#39;[server]:[port]&#39;/system/console/crypto。
   >    1. 在&#x200B;**[!UICONTROL 纯文本]**&#x200B;字段中，指定要加密的口令或任何字符串，然后点按&#x200B;**[!UICONTROL Protect]**。

   >    
   >    
   >    
   >加密的文本将显示在可在配置中指定的受保护文本字段中。

1. 启用&#x200B;**[!UICONTROL “借取时测试”]**&#x200B;或&#x200B;**[!UICONTROL “返回时测试”]**，以指定在从池借取对象或从池返回对象之前，验证对象。
1. 在&#x200B;**[!UICONTROL 验证查询]**&#x200B;字段中指定SQL SELECT查询，以验证池中的连接。 查询必须至少返回一行。 根据您的数据库，指定以下任一选项：

   * 选择1（MySQL和MS SQL）
   * 双选(Oracle)

1. 点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置。

## 配置AEM用户用户档案{#configure-aem-user-profile}

您可以使用AEM Web Console中的用户用户档案连接器配置配置AEM用户用户档案。 执行以下操作：

1. 转到AEM Web控制台，网址为https://&#39;[server]:[port]&#39;system/console/configMgr。
1. 查找&#x200B;**[!UICONTROL AEM Forms数据集成——用户用户档案连接器配置]**&#x200B;并点按以在编辑模式下打开配置。
1. 在“用户用户档案连接器配置”对话框中，可以添加、删除或更新用户用户档案属性。 指定的属性将可用于表单数据模型中。 使用以下格式指定用户用户档案属性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   示例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >上例中的&#x200B;*****&#x200B;表示CRXDE结构中AEM用户用户档案中`profile/empLocation/`节点下的所有节点。 这意味着表单数据模型可以访问`profile/empLocation/`节点下任何节点中存在的`string`类型的`city`属性。 但是，包含指定属性的节点必须采用一致的结构。

1. 点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置。

## 为云服务配置配置文件夹{#cloud-folder}

>[!NOTE]
为RESTful、SOAP和OData服务配置云服务，需要配置云服务文件夹。

AEM中的所有云服务配置都整合在AEM存储库的`/conf`文件夹中。 默认情况下，`conf`文件夹包含`global`文件夹，您可以在其中创建云服务配置。 但是，您需要手动为云配置启用它。 您还可以在`conf`中创建其他文件夹，以创建和组织云服务配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转至&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
1. 执行以下操作以启用云配置的全局文件夹，或跳过此步骤，为云服务配置创建和配置其他文件夹。

   1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，选择`global`文件夹，然后点按&#x200B;**[!UICONTROL 属性]**。

   1. 在&#x200B;**[!UICONTROL 配置属性]**&#x200B;对话框中，启用&#x200B;**[!UICONTROL 云配置]**。

   1. 点按&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，点按&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，指定文件夹的标题并启用&#x200B;**[!UICONTROL 云配置]**。
1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以创建为云服务配置启用的文件夹。

## 配置RESTful Web服务{#configure-restful-web-services}

REST风格的Web服务可在Swagger定义文件中使用JSON格式的[Swagger规范](https://swagger.io/specification/)或YAML格式进行描述。 要在AEM云服务中配置RESTful Web服务，请确保在文件系统上有Swagger文件或文件托管的URL。

执行以下操作以配置RESTful服务：

1. 转至&#x200B;**[!UICONTROL 工具>Cloud Services>数据源]**。 点按以选择要在其中创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置配置配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据源配置向导]**。 指定配置的名称和标题（可选），从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL RESTful服务]**，选择浏览并选择配置的缩略图，然后点按&#x200B;**[!UICONTROL 下一页]**。
1. 为RESTful服务指定以下详细信息：

   * 从“Swagger源”下拉菜单中选择“URL”或“文件”，然后相应地指定Swagger URL到Swagger定义文件或从本地文件系统上传Swagger文件。
   * 根据Swagger源输入，以下字段预填充了值：

      * 方案：REST API使用的传输协议。 在下拉列表中显示的方案类型数取决于在Swagger源中定义的方案。
      * 主机：提供REST API的主机的域名或IP地址。 这是必填字段。
      * 基本路径：所有API路径的URL前缀。 它是可选字段。\
         如有必要，请编辑这些字段的预填充值。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证、API密钥、自定义身份验证或相互身份验证）以访问RESTful服务，并相应地提供身份验证详细信息。

   如果选择&#x200B;**[!UICONTROL API密钥]**&#x200B;作为身份验证类型，请指定API密钥的值。 API密钥可以作为请求头或查询参数发送。 从&#x200B;**[!UICONTROL 位置]**&#x200B;下拉列表中选择这些选项之一，并相应地在&#x200B;**[!UICONTROL 参数名称]**&#x200B;字段中指定标头或查询参数的名称。

   如果选择&#x200B;**[!UICONTROL 相互身份验证]**&#x200B;作为身份验证类型，请参阅[针对RESTful和SOAP Web服务的基于证书的相互身份验证](#mutual-authentication)。

1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以创建RESTful服务的云配置。

## 配置SOAP Web服务{#configure-soap-web-services}

使用[Web服务描述语言(WSDL)规范](https://www.w3.org/TR/wsdl)描述基于SOAP的Web服务。 要在AEM云服务中配置基于SOAP的Web服务，请确保您具有Web服务的WSDL URL，并执行以下操作：

1. 转至&#x200B;**[!UICONTROL 工具>Cloud Services>数据源]**。 点按以选择要在其中创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置配置配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据源配置向导]**。 指定配置的名称和标题（可选），从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL SOAP Web服务]**，选择浏览并选择配置的缩略图，然后点按&#x200B;**[!UICONTROL 下一页]**。
1. 为SOAP Web服务指定以下内容：

   * Web服务的WSDL URL。
   * 服务端点. 在此字段中指定一个值以覆盖WSDL中提及的服务端点。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证、自定义身份验证、X509令牌或相互身份验证）以访问SOAP服务，并相应地提供身份验证的详细信息。

      如果选择&#x200B;**[!UICONTROL X509令牌]**&#x200B;作为身份验证类型，请配置X509证书。 有关详细信息，请参阅[设置证书](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)。
在**[!UICONTROL 密钥别名]**&#x200B;字段中指定X509证书的KeyStore别名。 在&#x200B;**[!UICONTROL Time To Live]**&#x200B;字段中指定验证请求保持有效的时间（以秒为单位）。 （可选）选择对邮件正文或时间戳标题进行签名，或者同时对两者进行签名。

      如果选择&#x200B;**[!UICONTROL 相互身份验证]**&#x200B;作为身份验证类型，请参阅[针对RESTful和SOAP Web服务的基于证书的相互身份验证](#mutual-authentication)。

1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以创建SOAP Web服务的云配置。

## 配置OData服务{#config-odata}

OData服务由其服务根URL标识。 要在AEM云服务中配置OData服务，请确保您具有该服务的服务根URL，并执行以下操作：

>[!NOTE]
有关配置Microsoft Dynamics 365的分步指南（联机或本地），请参阅[Microsoft Dynamics OData配置](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 转至&#x200B;**[!UICONTROL 工具>Cloud Services>数据源]**。 点按以选择要在其中创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置配置配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据源配置向导]**。 指定配置的名称和标题（可选），从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL OData服务]**，选择浏览并选择配置的缩略图，然后点按&#x200B;**[!UICONTROL 下一页]**。
1. 为OData服务指定以下详细信息：

   * 要配置的OData服务的服务根URL。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证或自定义身份验证）以访问OData服务，并相应地提供身份验证的详细信息。

   >[!NOTE]
   必须选择OAuth 2.0身份验证类型，以使用OData端点作为服务根连接Microsoft Dynamics服务。

1. 点按&#x200B;**创建**&#x200B;以创建OData服务的云配置。

## 针对RESTful和SOAP Web服务{#mutual-authentication}的基于证书的相互身份验证

为表单数据模型启用相互身份验证后，数据源和运行表单数据模型的AEM服务器在共享任何数据之前都会相互验证其身份。 可以对基于REST和SOAP的连接（数据源）使用相互身份验证。 要在您的AEM Forms环境上为表单数据模型配置相互身份验证，请执行以下操作：

1. 将私钥（证书）上传到[!DNL AEM Forms]服务器。 要上传私钥，请执行以下操作：
   1. 以管理员身份登录到您的[!DNL AEM Forms]服务器。
   1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。 选择`fd-cloudservice`用户并点按&#x200B;**[!UICONTROL 属性]**。
   1. 打开&#x200B;**[!UICONTROL Keystore]**&#x200B;选项卡，展开&#x200B;**[!UICONTROL 从KeyStore文件]**&#x200B;添加私钥选项，上传KeyStore文件，指定别名、密码，然后点按&#x200B;**[!UICONTROL 提交]**。 证书已上载。  私钥别名在证书中提及，并在创建证书时进行设置。
1. 将信任证书上传到全局信任存储。 要上传证书，请执行以下操作：
   1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 信任存储]**。
   1. 展开&#x200B;**[!UICONTROL 从CER文件]**&#x200B;添加证书选项，点按&#x200B;**[!UICONTROL 选择证书文件]**，上传证书，然后点按&#x200B;**[!UICONTROL 提交]**。
1. 将[SOAP](#configure-soap-web-services)或[RESTful](#configure-restful-web-services) Web服务配置为数据源，并选择&#x200B;**[!UICONTROL Mutual authentication]**&#x200B;作为身份验证类型。 如果为`fd-cloudservice`用户配置多个自签名证书，请指定证书的密钥别名。

## 后续步骤{#next-steps}

您已配置数据源。 接下来，您可以创建表单数据模型；如果已经创建了没有数据源的表单数据模型，则可以将其与刚刚配置的数据源关联。 有关详细信息，请参阅[创建表单数据模型](/help/forms/using/create-form-data-models.md)。
