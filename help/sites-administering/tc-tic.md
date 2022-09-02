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
source-wordcount: '0'
ht-degree: 0%

---

# 配置翻译集成框架{#configuring-the-translation-integration-framework}

翻译集成框架与第三方翻译服务集成，以编排 AEM 内容的译文。

* 连接到您的翻译服务提供商。
* 创建翻译集成框架配置。
* 将云配置与您的页面关联。

有关 AEM 中内容翻译功能的概述，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)。

## 连接到翻译服务提供商 {#connecting-to-a-translation-service-provider}

创建用于将 AEM 连接到您的翻译服务提供商的云配置。默认情况下，AEM 具有连接到 Microsoft Translator 的功能。以下翻译供应商为翻译项目提供了新API的实施。 链接可了解有关集成的更多信息：

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
* Microsoft(AEM中预安装了Microsoft Translator)

>[!NOTE]
>
>要查找人文和机器翻译提供商的最新列表，请查看以下页面：
>
>
>* [AEM人文翻译](https://www.adobe.com/go/aem-human-translation-connectors)
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

当网站的不同部分有不同的翻译要求时，请相应地创建多个框架配置。例如，多语言网站包含英语、西班牙语和日语副本。 站点所有者使用两个不同的翻译服务提供商生成西班牙语和日语译文。因此，配置了两个框架配置。每个配置使用一个不同的翻译服务提供商。

配置翻译集成框架后，可[将它与使用它的页面关联](/help/sites-administering/tc-prep.md)。

**注意：** 有关AEM中的内容翻译功能的概述，请参阅 [翻译多语言站点的内容](/help/sites-administering/translation.md).

框架的单个配置可控制如何翻译页面内容、社区内容和资产。
![chlimage_1-386](assets/translation-config-65.jpg)

### 站点配置属性 {#sites-configuration-properties}

“站点”属性可控制页面内容翻译的执行方式。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>选择框架对网站内容执行的翻译方法：</p>
    <ul>
     <li>机器翻译：翻译提供者使用机器翻译实时执行翻译。</li>
     <li>人文翻译：内容将发送给翻译提供商，由翻译人员翻译。 </li>
     <li>请勿翻译：内容不会发送以进行翻译。 这是为了跳过某些不翻译但可用最新内容更新的内容分支。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择翻译提供程序以执行翻译。 安装相应的连接器后，提供程序即会显示在列表中。</td>
  </tr>
  <tr>
   <td>内容类别</td>
   <td>（仅限机器翻译）描述正在翻译的内容的类别。 在翻译内容时，类别可能会影响术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择以翻译与页面关联的标记。</td>
  </tr>
  <tr>
   <td>翻译页面资产</td>
   <td><p>选择如何转换从文件系统添加到组件或从资产中引用的资产：</p>
    <ul>
     <li>请勿翻译：页面资产未进行折算。</li>
     <li>使用站点翻译工作流：资产将根据站点选项卡上的配置属性进行处理。</li>
     <li>使用资产翻译工作流：资产根据资产选项卡上属性的配置进行处理。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择此选项可在创建翻译项目后自动执行翻译作业。 选择此选项时，无法复查翻译作业和划定其范围。</td>
  </tr>
 </tbody>
</table>

### 社区配置属性 {#communities-configuration-properties}

社区属性控制如何执行用户生成内容的翻译。 用户生成内容的翻译始终使用机器翻译。 有关更多信息，请参阅 [翻译用户生成的内容](/help/communities/translate-ugc.md).

| 属性 | 描述 |
|---|---|
| 翻译提供商 | 选择翻译提供程序以执行翻译。 为其创建云配置的提供程序将显示在列表中。 |
| 内容类别 | 描述要翻译的内容的类别。 在翻译内容时，类别可能会影响术语和措辞的选择。 |
| 选择要用作全局共享存储的区域设置 | （可选）通过选择存储UGC的区域设置，所有语言副本中的帖子将显示在一个全局对话中。 根据惯例，选择 [基本语言](/help/communities/sites-console.md#translation) 中。 选择“无公用商店”将禁用全局翻译。 默认情况下，全局翻译处于禁用状态。 |

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
   <td><p>选择框架为资产执行的翻译类型：</p>
    <ul>
     <li>机器翻译：翻译提供程序使用机器翻译立即执行翻译。</li>
     <li>人文翻译：内容会自动发送到翻译提供商以进行手动翻译。 </li>
     <li>请勿翻译：不会发送资产进行翻译。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择翻译提供程序以执行翻译。 安装相应的连接器后，提供程序即会显示在列表中。</td>
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
   <td>选择以转换资产元数据。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择以翻译与资产关联的标记。</td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择此选项可在创建翻译项目后自动执行翻译作业。 选择此选项时，无法复查翻译作业或划定其范围。</td>
  </tr>
 </tbody>
</table>

1. 在侧栏中，单击或点按工具>操作>云>Cloud Services。
1. 在“翻译集成”区域中，是否已创建任何配置决定了将显示哪个链接：

   * 如果尚未创建配置，请单击或点按立即配置。
   * 如果配置已存在，请单击或点按显示配置，然后单击或点按可用配置旁边显示的+链接。

1. 键入配置的名称，然后单击或点按创建。
1. 在站点、社区和资产选项卡中配置属性，然后单击或点按确定。

## 配置页面以供翻译 {#configuring-pages-for-translation}

要配置如何将您的源页面翻译为其他语言，请将这些页面与以下云配置关联：

* 用于将 AEM 连接到您的翻译服务提供商的云配置。
* 用于配置翻译细节的翻译集成框架。

请注意，翻译集成框架云配置标识要用于连接到服务提供商的云配置。将源页面与框架云配置关联时，该页面必须与该框架云配置使用的服务提供商云配置关联。

将页面与云配置关联时，该页面的后代页面继承这种关联。例如，如果将/content/geometrixx/en/products页面与翻译集成框架相关联，则“产品”页面及其下的所有页面都将根据框架进行翻译。

必要时，可在后代页面上取代该关联。例如，网站的内容大多与服装有关。 但某个分支的页面介绍公司情况。站点的根页面与翻译集成框架相关联，该框架使用Clothing类别指定机器翻译。 描述公司的分支使用使用使用常规类别执行机器翻译的框架。

此外，对于任何社区 [SCF组件](/help/communities/scf.md) 在页面上，用户生成的内容(UGC)将包括用户翻译内容的功能。 有关更多信息，请参阅 [用户生成内容的翻译](/help/communities/translate-ugc.md).

### 将页面与翻译提供商关联 {#associating-a-page-with-a-translation-provider}

将页面与您用于翻译该页面和后代页面的翻译提供商关联。

1. 在站点控制台中，选择要配置的页面，然后单击或点按查看属性。
1. 单击或点按编辑，然后单击或点按Cloud Services选项卡。
1. 单击或点按添加配置>翻译集成。
1. 选择要使用的翻译提供程序，然后单击或点按完成。

### 将页面与翻译集成框架关联 {#associating-pages-with-a-translation-integration-framework}

将页面与定义您要如何为该页面和后代页面执行翻译的翻译集成框架关联。

1. 在站点控制台中，选择要配置的页面，然后单击或点按查看属性。
1. 单击或点按编辑，然后单击或点按Cloud Services选项卡。
1. 单击或点按添加配置>翻译集成。
1. 选择要使用的翻译集成框架，然后单击或点按完成。
