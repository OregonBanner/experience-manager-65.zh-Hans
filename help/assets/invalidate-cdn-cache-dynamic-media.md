---
title: 通过Dynamic Media使CDN缓存失效
description: 使CDN(内容投放网络)缓存内容失效后，您可以快速更新Dynamic Media交付的资源，而无需等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 34227ea285c48ce46488ee2256fee6c6dfeae162
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 1%

---


# 通过Dynamic Media使CDN缓存失效 {#invalidating-cdn-cache-for-dm-assets}

CDN(内容投放网络)会缓存Dynamic Media资源，以便快速投放给客户。 但是，当您更新这些资产时，您可能希望这些更改立即在您的网站上生效。 清除或取消验证CDN缓存可让您快速更新Dynamic Media交付的资产。 您无需使用TTL（生存时间）值（默认值为10小时）等待缓存过期，而是可以在Dynamic Media用户界面中发送请求，使缓存在几分钟内过期。

>[!IMPORTANT]
>
>以下步骤仅适用于AEM 6.5、Service Pack 6(AEM 6.5.6)或更高版本的Dynamic Media -Scene7模式。 此CDN失效功能还要求您使用与AEM Dynamic Media绑定的现成CDN;不支持任何其他自定义CDN。<br>如果您在AEM 6.5、Service Pack 5(AEM 6.5.5)或更早版本中使用Dynamic Media，请按照通过Dynamic Media Classic [使CDN缓存失效中的步骤操作](/help/assets/invalidate-cdn-cache-dm-classic.md)

>以下步骤仅适用于AEM 6.5、Service Pack 5(AEM 6.5.5)或更早版本中的Dynamic Media。<br>如果您在AEM 6.5、Service Pack 6(AEM 6.5.6)或更高版本中使用Dynamic Media，请按照通过Dynamic Media [使CDN缓存失效中的步骤操作](/help/assets/invalidate-cdn-cache-dynamic-media.md)

另请参 [阅Dynamic Media中的缓存概述](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**要使Dynamic Media资产的CDN缓存内容失效，请执行以下操作：**

*第1部分，共2部分：创建CDN失效模板*

1. 在AEM 6.5.6或更高版本中，点 **[!UICONTROL 按工具>资源> CDN失效。]**

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在“CDN **[!UICONTROL 失效模板]** ”页面上，根据您的方案执行下列选项之一：

   | 方案 | 选项 |
   | --- | --- |
   | 我过去已使用Dynamic Media Classic创建了CDN失效模板。 | “ **[!UICONTROL 创建模板]** ”文本字段会预填充模板数据。 在这种情况下，您可以编辑模板，也可以继续执行下一步。 |
   | 我需要创建模板。 我输入什么？ | 在创 **[!UICONTROL 建模板]** 文本字段中，输入引用的图像URL（包括图像预设或修饰符），而不是以下示例中的特定图像ID: `<ID>`如果模板仅包<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>`<ID>``https://<publishserver_name>/is/image/<company_name>/<ID>``<publishserver_name>` 含，则Dynamic Media将填充其中的Publish Server名称，该名称在Dynamic Media Classic的常规设置中定义；它是 `<company_name>` 与此AEM实例关联的公司根的名称， `<ID>` 是通过资产选取器选择的要失效的资产。<br>任何预设／修改 `<ID>` 工具帖子均按原样复制在URL定义中。<br>只有图像(即， `/is/image`可以根据模板自动形成)。<br>对 `/is/content/`于，使用资产选取器添加视频或PDF等资产不会自动生成URL。 您必须在CDN失效模板中指定此类资产，也可以在第2部分（共2部分）中手动将URL *添加到此类资产：设置CDN失效选项*。<br>**示例：**<br>&#x200B;在第一个示例中，失效模板与具 `<ID>` 有的资产URL一起包含 `/is/content`。 For example, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media会根据此信息构成URL, `<ID>` 即通过要使其失效的资产选取器选择的资产。<br>在第二个示例中，失效模板包含在Web属性中使用的资产的完整URL, `/is/content` 具体取决于资产选取器。 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 背包是资产ID。<br>Dynamic Media支持的资产格式有资格失效。 不支持CDN失效 *的资源* 文件类型包括Postscript、封装Postscript、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word和富文本格式。<br>创建模板时，请务必注意语法和错别字；Dynamic Media不执行任何模板验证。<br>请注意，必须在此CDN失效模板或第2部分的“添加URL”文 **[!UICONTROL 本字段中]** ，指定图 *像智能裁剪的URL:设置CDN失效选项。*<br>**重要：**CDN失效模板中的每个条目必须位于其自己的行中。<br>*以下模板示例仅供说明。* |

   ![CDN失效模板——创建](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 在CDN失效模板页面的 **[!UICONTROL 右上角]** ，点按 **[!UICONTROL 保存]**，然后点 **[!UICONTROL 按确定。]**<br>   *第2部分，共2部分：设置CDN失效选项*
   <br>

1. 在AEM中，点按工具>资 **[!UICONTROL 源> CDN失效Cloud Service。]**

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在“CDN **[!UICONTROL 失效]** -添 **[!UICONTROL 加详细信息]** ”页面上，选择CDN失效的资源。

   ![CDN失效——添加详细信息](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您决定不选中CDN中的“使 **[!UICONTROL 与资产关联的图像预设失]** 效 *”和* “基于模板 **** 失效”选项，则会将选定资产的基本URL设置为失效。 应仅对图像使用此选项排列。


   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中与资产关联的图像预设失效]** | （可选）选中此选项后，选定的资产及其所有关联的图像预设URL将自动生成，以便缓存失效。<br>资产及其关联的预定义预设URL会因失效而自动生成。 此选项仅适用于图像资产。 |
   | **[!UICONTROL 基于模板的失效]** | （可选）选中此选项，仅使用定义的模板来形成URL。 |
   | **[!UICONTROL 添加资产]** | 使用资产选取器选择要失效的资产。 您可以选择已发布或已取消发布的资产。<br>CDN的缓存基于URL，而非基于资产。 因此，您必须了解网站上的完整URL。 确定这些URL后，可以将其添加到模板。 然后，您可以选择并添加这些资产，并使URL失效。 <br>将此选项与CDN中与资 **[!UICONTROL 源关联的图像预设失效]**、基于 **[!UICONTROL 模板的失效或两者结合使用]**。 |
   | **[!UICONTROL 添加 URL]** | 手动添加或粘贴要使其CDN缓存失效的Dynamic Media资产的完整URL路径。 如果未在第1部分（共2部分）中创建CDN失 ***效模板，请使用此选项：创建CDN失效模板***，并且只有少数资源可以失效。<br>**重要：** 您添加的每个URL都必须位于其自己的行中。<br>在指定时间最多可使1000个URL失效。 如果“添加URL”文 **[!UICONTROL 本字段]** 中的URL数大于1000，则无法点按“下 **[!UICONTROL 一步”]**。 在这种情况下，您必须点 **[!UICONTROL 按选定]** 资产或手动添加的URL右侧的X，以将其从失效列表中删除。<br>请注意，您必须在CDN失效模板或此添加URL文本字段中为图像智 **[!UICONTROL 能裁剪指定]** URL。 |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next.]**
1. 在“CDN **[!UICONTROL 失效]** -确认 **[!UICONTROL ”页面的“URL]****** 列表”框中，您将看到一个或多个URL的列表，这些URL是从您之前创建的CDN失效模板以及您刚刚添加的资源生成的。

   例如，使用前面的步骤中显示的CDN失效模板示例，假定您添加了名为的单个资源 `spinset`。 点按“工 **[!UICONTROL 具”>“资源”>]** “CDN失效”时，会在“CDN失效——确认用 **[!UICONTROL 户界面”中生成以下五个URL]** :

   ![CDN失效——确认](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要， **点按** URL右侧的X，以将其从失效过程中删除。

1. 在页面的右上角附近，点按提 **[!UICONTROL 交]** ，开始CDN失效过程。

## 排除CDN失效错误

在所有情况下，都会处理整个批以失效，或者整个批失败。

| 错误 | 说明 |
| --- | --- |
| *无法检索选定资产的URL。* | 在满足以下任一情形时发生：<br>—— 找不到Dynamic Media配置。<br>-检索用于读取Dynamic Media配置的服务用户时出现异常。<br>- Dynamic Media配置中缺少用于构成URL的发布服务器或公司根。 |
| *某些URL定义不正确。 请更正并重新提交。* | 如果IPS CDN缓存失效API返回错误，称URL引用的是其他公司，或者URL无效（如IPS cdnCacheInvalidation API执行的验证），则发生。 |
| *无法使CDN缓存失效。* | 如果CDN缓存失效请求因任何其他原因失败发生。 |
| *未输入要失效的URL。* | 如果CDN失效——确认页面中 **[!UICONTROL 没有URL]** , **[!UICONTROL 并点按提]****[!UICONTROL 交时发生。]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
