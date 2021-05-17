---
title: 配置翻译集成框架
seo-title: 配置翻译集成框架
description: 了解如何配置翻译集成框架。
seo-description: 了解如何配置翻译集成框架。
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: 语言复制
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
source-git-commit: bed7ffd413c7826cf0e419fa1c31e3d3c325d4b1
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 2%

---

# 配置翻译集成框架{#configuring-the-translation-integration-framework}

翻译集成框架与第三方翻译服务集成以协调AEM内容的翻译。

* 连接到您的翻译服务提供商。
* 创建翻译集成框架配置。
* 将云配置与您的页面关联。

有关AEM中内容翻译功能的概述，请参阅[多语言站点内容翻译](/help/sites-administering/translation.md)。

## 连接到翻译服务提供商{#connecting-to-a-translation-service-provider}

创建将AEM连接到翻译服务提供商的云配置。 AEM默认包含连接到Microsoft Translator的功能。
以下翻译供应商为翻译项目提供了新API的实施。 链接可了解有关集成的更多信息：

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (Adobe Exchange Premier合作伙伴)
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [云字](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [CrossLang NV](https://exchange.adobe.com/experiencecloud.details.90049.crosslang-xtm-for-adobe-experience-manager.html)
* [XTM云](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [林戈特克](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [智能](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [阿尔特朗](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft(AEM中预装了Microsoft Translator)

>[!NOTE]
>
>要查找人文和机器翻译提供商的最新列表，请查看以下页面：
>
>
>* [AEM人文翻译](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM Machine Translation](https://www.adobe.com/go/aem-machine-translation-connectors)

>



安装连接器包后，可以为连接器创建云配置。 通常，您需要提供凭据以便向翻译服务进行身份验证。 有关为Microsoft Translator连接器添加云配置的信息，请参阅[与Microsoft Translator](/help/sites-administering/tc-msconf.md)集成。

如果需要，可以为同一连接器创建多个云配置。 例如，为您与同一供应商拥有的每个帐户或项目创建一个配置。

配置连接后，您可以创建使用该连接的翻译集成框架配置。

## 创建翻译集成配置{#creating-a-translation-integration-configuration}

创建翻译集成框架配置以指定如何翻译您的内容。 配置包括以下信息：

* 要使用的翻译服务提供商。
* 是否要执行人或机器翻译。
* 是否翻译与页面或资产关联的其他内容，如标记。

在创建框架配置后，您可以根据配置将云配置与要翻译的页面相关联。 当翻译过程启动时，翻译工作流会根据关联的框架配置进行。

当网站的不同部分具有不同的翻译要求时，请相应地创建多个框架配置。 例如，多语言网站包含英语、西班牙语和日语副本。 站点所有者对西班牙语和日语翻译使用两种不同的翻译服务提供商。 因此，配置了框架的两种配置。 每个配置都使用不同的翻译服务提供商。

配置翻译集成框架后，可以[将其与使用该框架的页面](/help/sites-administering/tc-prep.md)关联。

**注意：** 有关AEM中内容翻译功能的概述，请参阅 [多语言站点翻译内容](/help/sites-administering/translation.md)。

框架的单个配置控制如何翻译页面内容、社区内容和资产。
![chlimage_1-386](assets/translation-config-65.jpg)

### 站点配置属性{#sites-configuration-properties}

“站点”属性控制页面内容翻译的执行方式。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>选择框架对站点内容执行的翻译方法：</p>
    <ul>
     <li>机器翻译：翻译提供商使用机器翻译实时执行翻译。</li>
     <li>人文翻译：内容将发送给翻译提供商，由翻译人员进行翻译。 </li>
     <li>不翻译：内容不会发送以供翻译。 这样可跳过某些内容分支，这些分支不会翻译，但可以使用最新内容进行更新。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择要执行翻译的翻译提供者。 安装相应连接器后，列表中将显示提供程序。</td>
  </tr>
  <tr>
   <td>内容目录</td>
   <td>（仅限机器翻译）描述要翻译的内容的类别。 类别会影响翻译内容时术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择以翻译与页面关联的标记。</td>
  </tr>
  <tr>
   <td>翻译页面资产</td>
   <td><p>选择如何转换从文件系统添加到组件或从资产引用的资产：</p>
    <ul>
     <li>不翻译：页面资产不会进行翻译。</li>
     <li>使用站点翻译工作流：资产会根据“站点”选项卡上的配置属性进行处理。</li>
     <li>使用资产翻译工作流：资产会根据“资产”选项卡上属性的配置进行处理。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择此项可在创建翻译项目后自动执行翻译作业。 当您选择此选项时，您没有机会复查和范围翻译作业。</td>
  </tr>
 </tbody>
</table>

### 社区配置属性{#communities-configuration-properties}

“社区”属性控制用户生成内容的翻译执行方式。 用户生成内容的翻译始终使用机器翻译。 有关详细信息，请参阅[翻译用户生成的内容](/help/communities/translate-ugc.md)。

| 属性 | 描述 |
|---|---|
| 翻译提供商 | 选择要执行翻译的翻译提供者。 创建云配置的提供程序将显示在列表中。 |
| 内容目录 | 描述要翻译的内容的类别。 类别会影响翻译内容时术语和措辞的选择。 |
| 选择要用作全局共享存储的区域设置 | （可选）通过选择存储UGC的区域设置，来自所有语言副本的帖子将显示在一个全局对话中。 根据惯例，为网站的[基本语言](/help/communities/sites-console.md#translation)选择区域设置。 选择“无公用商店”将禁用全局翻译。 默认情况下，全局翻译处于禁用状态。 |

### 资产配置属性{#assets-configuration-properties}

资产属性控制如何配置资产。 有关翻译资产的详细信息，请参阅[为资产创建语言副本](/help/assets/translation-projects.md)。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>选择框架为资产执行的转换类型：</p>
    <ul>
     <li>机器翻译：翻译提供者使用机器翻译立即执行翻译。</li>
     <li>人文翻译：内容会自动发送到翻译提供者以进行手动翻译。 </li>
     <li>不翻译：资产不会发送以进行翻译。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>选择要执行翻译的翻译提供者。 安装相应连接器后，列表中将显示提供程序。</td>
  </tr>
  <tr>
   <td>内容目录</td>
   <td>（仅限机器翻译）描述要翻译的内容的类别。 类别会影响翻译内容时术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译资产</td>
   <td>选择此项可在翻译项目中包含资产。 </td>
  </tr>
  <tr>
   <td>翻译元数据</td>
   <td>选择以转换资产元数据。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>选择此项可翻译与资产关联的标记。</td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>选择此项可在创建翻译项目后自动执行翻译作业。 当您选择此选项时，您没有机会复查或调整翻译作业的范围。</td>
  </tr>
 </tbody>
</table>

1. 在侧栏中，单击或点按工具>操作>云>Cloud Services。
1. 在“翻译集成”区域中，是否已创建任何配置决定显示哪个链接：

   * 如果未创建任何配置，请单击或点按立即配置。
   * 如果配置已存在，请单击或点按显示配置，然后单击或点按可用配置旁边显示的+链接。

1. 键入配置的名称，然后单击或点按创建。
1. 在站点、社区和资产选项卡上配置属性，然后单击或点按确定。

## 配置翻译{#configuring-pages-for-translation}的页面

要将源页面翻译为其他语言，请将这些页面与以下云配置关联：

* 将AEM连接到翻译提供商的云配置。
* 配置翻译详细信息的翻译集成框架。

请注意，翻译集成框架云配置标识要用于连接到服务提供商的云配置。 将源页面与框架云配置关联时，该页面必须与框架云配置使用的服务提供商云配置关联。

将页面与云配置关联时，页面的后代将继承关联。 例如，如果将/content/geometrixx/cn/products页面与翻译集成框架关联，则“产品”页面及其下面的所有页面将根据框架进行翻译。

如果需要，您可以在后代页面上覆盖关联。 例如，网站的内容主要是服装。 但是，页面的一个分支描述了该公司。 站点的根页面与一个Translation Integration Framework关联，该Translation Integration Framework指定使用Clothing类别进行机器翻译。 描述公司的分支使用使用常规类别执行机器翻译的框架。

此外，对于页面上的任何社区[SCF组件](/help/communities/scf.md)，用户生成的内容(UGC)将包括用户翻译内容的功能。 有关详细信息，请参阅[用户生成内容的翻译](/help/communities/translate-ugc.md)。

### 将页面与翻译提供程序{#associating-a-page-with-a-translation-provider}关联

将页面与用于翻译页面和后代页面的翻译提供程序关联。

1. 在站点控制台中，选择要配置的页面，然后单击或点按视图属性。
1. 单击或点按编辑，然后单击或点按Cloud Services选项卡。
1. 单击或点按添加配置>翻译集成。
1. 选择要使用的翻译提供程序，然后单击或点按完成。

### 将页面与翻译集成框架{#associating-pages-with-a-translation-integration-framework}关联

将页面与翻译集成框架关联，该框架定义了您要如何执行页面和后代页面的翻译。

1. 在站点控制台中，选择要配置的页面，然后单击或点按视图属性。
1. 单击或点按编辑，然后单击或点按Cloud Services选项卡。
1. 单击或点按添加配置>翻译集成。
1. 选择要使用的翻译集成框架，然后单击或点按完成。
