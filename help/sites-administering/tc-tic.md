---
title: 配置翻译集成框架
seo-title: Configuring the Translation Integration Framework
description: 了解如何配置翻译集成框架。
seo-description: Learn how to configure the Translation Integration Framework.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
source-git-commit: 6dea3a23c70fdb5f07bdf724547e799776002c61
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 47%

---

# 配置翻译集成框架{#configuring-the-translation-integration-framework}

翻译集成框架与第三方翻译服务集成，以编排 AEM 内容的译文。

* 连接到您的翻译服务提供商。
* 创建翻译集成框架配置。
* 将云配置与您的页面关联。

有关 AEM 中内容翻译功能的概述，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)。

## 连接到翻译服务提供商 {#connecting-to-a-translation-service-provider}

创建用于将 AEM 连接到您的翻译服务提供商的云配置。默认情况下，AEM 具有连接到 Microsoft Translator 的功能。以下翻译供应商为翻译项目提供新API的实施。 用于了解有关集成的更多信息的链接：

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)（Adobe Exchange 首选合作伙伴）
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [Smartling](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [阿尔特朗](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft (AEM中预装了Microsoft Translator)

>[!NOTE]
>
>要查找人工翻译提供商和机器翻译提供商的最新列表，请查看以下页面：
>
>
>* [AEM人工翻译](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM机器翻译](https://www.adobe.com/go/aem-machine-translation-connectors)
>


安装连接器软件包后，即可为连接器创建云配置。一般需要提供凭据，以便向翻译服务进行身份验证。有关为 Microsoft Translator 连接器添加云配置的信息，请参阅[与 Microsoft Translator 集成](/help/sites-administering/tc-msconf.md)。

如果需要，可为同一个连接器创建多个云配置。例如，为您在同一供应商的每个帐户或项目都创建一个配置。

配置连接后，即可创建使用它的翻译集成框架配置。

## 创建翻译集成配置 {#creating-a-translation-integration-configuration}

创建翻译集成框架配置以指定如何翻译您的内容。该配置包括以下信息：

* 要使用哪个翻译服务提供商。
* 要执行人工翻译还是机器翻译.
* 是否翻译与页面或资产关联的其他内容，如标记.

创建框架配置后，请将云配置与要根据该配置翻译的页面关联。开始翻译过程后，将根据关联的框架配置执行翻译工作流。

当网站的不同部分有不同的翻译要求时，请相应地创建多个框架配置。例如，多语言网站包括英语、西班牙语和日语副本。 站点所有者使用两个不同的翻译服务提供商生成西班牙语和日语译文。因此，配置了两个框架配置。每个配置使用一个不同的翻译服务提供商。

配置翻译集成框架后，可[将它与使用它的页面关联](/help/sites-administering/tc-prep.md)。

**注意：** 有关AEM中内容翻译功能的概述，请参阅 [翻译多语言站点的内容](/help/sites-administering/translation.md).

只有一个框架配置可控制如何翻译页面内容、社区内容和资产。
![chlimage_1-386](assets/translation-config-65.jpg)

### 站点配置属性 {#sites-configuration-properties}

站点属性控制如何执行页面内容的翻译。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>选择框架为网站内容执行的翻译方法：</p>
    <ul>
     <li>机器翻译：翻译提供商使用机器翻译实时执行翻译。</li>
     <li>人工翻译：将内容发送到翻译提供商，以供翻译人员翻译。 </li>
     <li>不翻译：不发送内容以供翻译。 这是为了跳过某些不翻译但可用最新内容更新的内容分支。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择要执行翻译的翻译提供商。 安装提供商的相应连接器后，列表中会显示该提供商。</td>
  </tr>
  <tr>
   <td>内容类别</td>
   <td>（仅限机器翻译）描述正在翻译的内容的类别。 在翻译内容时，类别可能会影响术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择可翻译与页面关联的标记。</td>
  </tr>
  <tr>
   <td>翻译页面资产</td>
   <td><p>选择如何翻译从文件系统添加到组件或从资源引用的资源：</p>
    <ul>
     <li>不翻译：不翻译页面资产。</li>
     <li>使用站点翻译工作流：根据站点选项卡上的配置属性处理资产。</li>
     <li>使用资产翻译工作流：根据资产选项卡上属性的配置处理资产。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择可在创建翻译项目后自动执行翻译作业。 选择此选项时，无法复查翻译作业和划定其范围。</td>
  </tr>
 </tbody>
</table>

### Communities配置属性 {#communities-configuration-properties}

社区属性控制如何执行用户生成的内容的翻译。 用户生成的内容的翻译始终使用机器翻译。 有关更多信息，请参阅 [翻译用户生成的内容](/help/communities/translate-ugc.md).

| 属性 | 描述 |
|---|---|
| 翻译提供商 | 选择要执行翻译的翻译提供商。 为其创建云配置的提供程序将显示在列表中。 |
| 内容类别 | 描述正在翻译的内容的类别。 在翻译内容时，类别可能会影响术语和措辞的选择。 |
| 选择要用作全局共享存储的区域设置 | （可选）通过选择存储UGC的区域设置，来自所有语言副本的帖子将显示在一个全局对话中。 按照惯例，选择 [基本语言](/help/communities/sites-console.md#translation) 用于网站。 选择无公用存储将禁用全局翻译。 默认情况下，全局翻译处于禁用状态。 |

### 资产配置属性 {#assets-configuration-properties}

资产属性控制如何配置资产。有关翻译资产的更多信息，请参阅[创建资产的语言副本](/help/assets/translation-projects.md)。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>选择框架为资源执行的翻译的类型：</p>
    <ul>
     <li>机器翻译：翻译提供商使用机器翻译立即执行翻译。</li>
     <li>人工翻译：自动将内容发送到翻译提供商，以供手动翻译。 </li>
     <li>不翻译：不发送资产以供翻译。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择要执行翻译的翻译提供商。 安装提供商的相应连接器后，列表中会显示该提供商。</td>
  </tr>
  <tr>
   <td>内容类别</td>
   <td>（仅限机器翻译）描述正在翻译的内容的类别。 在翻译内容时，类别可能会影响术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译资产</td>
   <td>选择以在翻译项目中包含资产。 </td>
  </tr>
  <tr>
   <td>翻译元数据</td>
   <td>选择以翻译资源元数据。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择以翻译与资源关联的标记。</td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择可在创建翻译项目后自动执行翻译作业。 选择此选项时，无法复查翻译作业或划定其范围。</td>
  </tr>
 </tbody>
</table>

1. 单击或点按侧栏中的“工具”>“操作”>“云”>“Cloud Services”。
1. 在翻译集成区域，是否已创建任何配置决定了显示的链接：

   * 如果尚未创建配置，请单击或点按立即配置。
   * 如果配置已存在，请单击或点按显示配置，然后单击或点按可用配置旁边显示的+链接。

1. 键入配置的名称，然后单击或点按创建。
1. 在站点、社区和资产选项卡上配置属性，然后单击或点按确定。

## 配置页面以供翻译 {#configuring-pages-for-translation}

要配置如何将您的源页面翻译为其他语言，请将这些页面与以下云配置关联：

* 用于将 AEM 连接到您的翻译服务提供商的云配置。
* 用于配置翻译细节的翻译集成框架。

请注意，翻译集成框架云配置标识要用于连接到服务提供商的云配置。将源页面与框架云配置关联时，该页面必须与该框架云配置使用的服务提供商云配置关联。

将页面与云配置关联时，该页面的后代页面继承这种关联。例如，如果将/content/geometrixx/en/products页面与翻译集成框架关联，则将根据该框架翻译产品页面及其下的所有页面。

必要时，可在后代页面上取代该关联。例如，网站的内容主要是关于服装。 但某个分支的页面介绍公司情况。站点的根页面与指定使用“服装”类别进行机器翻译的翻译集成框架关联。 描述公司情况的分支使用框架，该框架使用“常规”类别执行机器翻译。

此外，对于任何社区 [SCF组件](/help/communities/scf.md) 在页面上，用户生成的内容(UGC)将包括用户翻译内容的功能。 有关更多信息，请参阅 [用户生成内容的翻译](/help/communities/translate-ugc.md).

### 将页面与翻译提供商关联 {#associating-a-page-with-a-translation-provider}

将页面与您用于翻译该页面和后代页面的翻译提供商关联。

1. 在站点控制台中，选择要配置的页面，然后单击或点按查看属性。
1. 单击或点按编辑，然后单击或点按Cloud Services选项卡。
1. 单击或点按添加配置>翻译集成。
1. 选择要使用的翻译提供商，然后单击或点按完成。

### 将页面与翻译集成框架关联 {#associating-pages-with-a-translation-integration-framework}

将页面与定义您要如何为该页面和后代页面执行翻译的翻译集成框架关联。

1. 在站点控制台中，选择要配置的页面，然后单击或点按查看属性。
1. 单击或点按编辑，然后单击或点按Cloud Services选项卡。
1. 单击或点按添加配置>翻译集成。
1. 选择要使用的翻译集成框架，然后单击或点按完成。
