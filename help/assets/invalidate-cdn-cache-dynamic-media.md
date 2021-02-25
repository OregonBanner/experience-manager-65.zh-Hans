---
title: 通过Dynamic Media使CDN缓存失效
description: 使您的CDN(内容投放网络)缓存内容失效后，您可以快速更新由Dynamic Media交付的资源，而不是等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 729fbf3a97d3ae3bc91204f8831fd115d9d77f20
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 1%

---


# 通过Dynamic Media {#invalidating-cdn-cache-for-dm-assets}使CDN缓存失效

Dynamic Media资源由CDN(内容投放网络)缓存，以便快速投放给您的客户。 但是，当您更新这些资产时，您希望这些更改立即在您的网站上生效。 清除或取消验证CDN缓存可让您快速更新由Dynamic Media交付的资源。 您可以在Dynamic Media内发送请求，使缓存在几分钟内过期，而不用使用TTL（生存时间）值（默认为十小时）等待缓存过期。

>[!NOTE]
>
>客户必须使用与Adobe Experience Manager Dynamic Media捆绑的CDN，以从CDN缓存失效中受益。

>[!IMPORTANT]
>
>以下步骤仅适用于Dynamic Media - Scene7模式(在Adobe Experience Manager 6.5、Service Pack 6(Experience Manager 6.5.6)或更高版本中)。 此CDN失效功能还要求您使用与Experience Manager Dynamic Media捆绑的现成CDN;不支持任何其他自定义CDN。<br>如果您在Experience Manager 6.5、Service Pack 5(Experience Manager 6.5.5)或更早版本中使用Dynamic Media，请按照通过Dynamic Media Classic使CDN缓 [存失效中的步骤操作。](/help/assets/invalidate-cdn-cache-dm-classic.md)

另请参阅Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)中的[缓存概述。

**要使Dynamic Media资源的CDN缓存内容失效，请执行以下操作：**

*第1部分，共2部分：创建CDN失效模板*

1. 在Experience Manager 6.5.6或更高版本中，点按&#x200B;**[!UICONTROL 工具>资源> CDN失效。]**

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;页面上，根据您的方案执行下列选项之一：

   | 方案 | 选项 |
   | --- | --- |
   | 我过去曾使用Dynamic Media Classic创建过CDN失效模板。 | **[!UICONTROL 创建模板]**&#x200B;文本字段会预填充模板数据。 在这种情况下，您可以编辑模板，也可以继续执行下一步。 |
   | 我必须创建一个模板。 我要输入什么？ | 在&#x200B;**[!UICONTROL 创建模板]**&#x200B;文本字段中，输入引用`<ID>`的图像URL（包括图像预设或修饰符），而不是如下例所示的特定图像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果模板仅包含`<ID>`，则Dynamic Media将填充`https://<publishserver_name>/is/image/<company_name>/<ID>`，其中`<publishserver_name>`是Publish Server中定义的名称Dynamic Media Classic中的常规设置。 `<company_name>`是与此公司实例关联的Experience Manager根名称，`<ID>`是通过资产选取器选择的要失效的资产。<br>在URL定义中，将 `<ID>` 按原样复制任何预设/修饰符帖子。<br>只有图像(即， `/is/image` )才能基于模板自动形成。<br>对 `/is/content/`于，使用资产选取器添加视频或PDF等资产不会自动生成URL。您必须在CDN失效模板中指定此类资源，或者可以在&#x200B;*第2部分（共2部分）中手动将URL添加到此类资源：设置CDN失效选项*。<br>**示例：**<br>&#x200B;在第一个示例中，失效模板 `<ID>` 与具有的资产URL一起包含 `/is/content`。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。 Dynamic Media会根据此路径构建URL，其中`<ID>`是通过您希望失效的资产选取器选择的资产。<br>在第二个示例中，失效模板包含您的Web属性中使用的资产的完整URL( `/is/content` 不取决于资产选取器)。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack`其中，backpack是资产ID。<br>Dynamic Media中支持的资产格式有权失效。*不*&#x200B;支持CDN失效的资源文件类型包括PostScript®、封装PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word和富文本格式。<br>创建模板时，请务必注意语法和错别字；Dynamic Media不执行任何模板验证。<br>在此CDN失效模板或第2部分的“添加URL”文本字段中 **[!UICONTROL 指]** 定图像智 *能裁剪的URL:设置CDN失效选项。*<br>**重要：**CDN失效模板中的每个条目必须位于其自己的行中。<br>*以下模板示例仅供说明之用。* |

   ![CDN失效模板 — 创建](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 在&#x200B;**[!UICONTROL CDN Invalidation模板]**&#x200B;页面的右上角，点按&#x200B;**[!UICONTROL 保存]**，然后点按&#x200B;**[!UICONTROL 确定。]**<br>

   *第2部分，共2部分：设置CDN失效选项*
   <br>

1. 在Experience Manager作为Cloud Service时，点按&#x200B;**[!UICONTROL 工具>资源> CDN失效。]**

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在&#x200B;**[!UICONTROL CDN失效 — 添加详细信息]**&#x200B;页面上，选择用于CDN失效的资源。

   ![CDN失效 — 添加详细信息](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您决定不选中选项&#x200B;**[!UICONTROL 使CDN]** *和* **[!UICONTROL 中与资源关联的图像预设失效，则选定资源的基本URL会被设置为失效。]**&#x200B;仅对图像使用此选项排列。


   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中与资产关联的图像预设失效]** | （可选）选中此选项后，选定的资产及其所有关联的图像预设URL都会因缓存失效而自动生成。<br>资产及其关联的预定义URL会因失效而自动形成。此选项仅适用于图像资源。 |
   | **[!UICONTROL 基于模板的失效]** | （可选）选中此选项可仅对URL形成使用定义的模板。 |
   | **[!UICONTROL 添加资产]** | 使用资产选取器选择要失效的资产。 您可以选择已发布或未发布的资产。<br>CDN上的缓存基于URL，而非基于资源。因此，您必须了解您网站上的完整URL。 确定这些URL后，可以将其添加到模板。 然后，您可以选择并添加这些资产，并使URL在一步中失效。 <br>在CDN中与资源关 **[!UICONTROL 联的图像预设或基于模板的无]**&#x200B;效(或同时使用两者 ****)中使用此选项。 |
   | **[!UICONTROL 添加 URL]** | 手动添加或粘贴要使其CDN缓存失效的Dynamic Media资源的完整URL路径。 如果未在&#x200B;***第1部分（共2部分）中创建CDN失效模板，请使用此选项：创建CDN失效模板***，并且只有少量资源可以失效。<br>**重要信** 息：您添加的每个URL必须位于其自己的行中。<br>一次最多可使1000个URL失效。如果&#x200B;**[!UICONTROL 添加URL]**&#x200B;文本字段中的URL数大于1000，则无法点按&#x200B;**[!UICONTROL 下一个]**。 在这种情况下，您必须点按选定资产右侧的&#x200B;**[!UICONTROL X]**，或手动添加的URL，以将其从失效列表中删除。<br>在CDN失效模板或此添加URL文本字段中指定图像智能裁剪 **[!UICONTROL 的]** URL。 |

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 下一步。]**
1. 在&#x200B;**[!UICONTROL CDN失效 — 确认]**&#x200B;页面的&#x200B;**[!UICONTROL URL]**&#x200B;列表框中，可以看到从您之前创建的CDN失效模板以及刚刚添加的资源生成的一个或多个URL的列表。

   例如，使用前面步骤中显示的CDN失效模板示例，假定您添加了名为`spinset`的单个资源。 点按&#x200B;**[!UICONTROL 工具>资源> CDN失效]**&#x200B;时，会在&#x200B;**[!UICONTROL CDN失效 — 确认]**&#x200B;用户界面中生成以下五个生成的URL:

   ![CDN失效 — 确认](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，请点按URL右侧的&#x200B;**X**，将其从失效过程中删除。

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 提交]**&#x200B;以开始CDN失效过程。

## 对CDN失效错误进行疑难解答

在所有情况下，要么处理整个批以失效，要么处理整个批失败。

| 错误 | 解释 |
| --- | --- |
| *无法检索选定资产的URL。* | 如果满足以下任一情况，则发生：<br> — 找不到Dynamic Media配置。<br> — 检索读取Dynamic Media配置的服务用户时出现异常。<br> — 在Dynamic Media配置中缺少用于构成URL的发布服务器或公司根。 |
| *某些URL定义不正确。更正并重新提交。* | 当IPS CDN缓存失效API返回URL引用其他公司的错误时发生。 或者，如果URL无效，与IPS `cdnCacheInvalidation` API完成的验证相同。 |
| *无法使CDN缓存失效。* | 在CDN缓存失效请求因任何其他原因失败时发生。 |
| *未输入URL作为无效URL。* | 如果&#x200B;**[!UICONTROL CDN失效 — 确认]**&#x200B;页面中没有URL，则点按&#x200B;**[!UICONTROL 提交。]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
