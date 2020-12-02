---
title: 通过Dynamic Media使CDN缓存失效
description: 使CDN(内容投放网络)缓存内容失效后，您可以快速更新Dynamic Media交付的资源，而无需等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 54645149dc4968c1c4f85eedb5ce4d71f80c3b64
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 1%

---


# 通过Dynamic Media {#invalidating-cdn-cache-for-dm-assets}使CDN缓存失效

CDN(内容投放网络)会缓存Dynamic Media资源，以便快速投放给客户。 但是，当您更新这些资产时，您可能希望这些更改立即在您的网站上生效。 清除或取消验证CDN缓存可让您快速更新Dynamic Media交付的资产。 您无需使用TTL（生存时间）值（默认值为10小时）等待缓存过期，而是可以在Dynamic Media用户界面中发送请求，使缓存在几分钟内过期。

>[!IMPORTANT]
>
>以下步骤仅适用于AEM 6.5、Service Pack 6(AEM 6.5.6)或更高版本的Dynamic Media -Scene7模式。 此CDN失效功能还要求您使用与AEM Dynamic Media绑定的现成CDN;不支持任何其他自定义CDN。<br>如果您在AEM 6.5、Service Pack 5(AEM 6.5.5)或更早版本中使用Dynamic Media，请按照通过Dynamic Media  [Classic使CDN缓存失效中的步骤操作。](/help/assets/invalidate-cdn-cache-dm-classic.md)

另请参阅[Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)中的缓存概述。

**要使Dynamic Media资产的CDN缓存内容失效，请执行以下操作：**

*第1部分，共2部分：创建CDN失效模板*

1. 在AEM 6.5.6或更高版本中，点按&#x200B;**[!UICONTROL 工具>资产> CDN失效。]**

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;页面上，根据您的方案执行下列选项之一：

   | 方案 | 选项 |
   | --- | --- |
   | 我过去已使用Dynamic Media Classic创建了CDN失效模板。 | **[!UICONTROL 创建模板]**&#x200B;文本字段预填充了模板数据。 在这种情况下，您可以编辑模板，也可以继续执行下一步。 |
   | 我需要创建模板。 我输入什么？ | 在&#x200B;**[!UICONTROL 创建模板]**&#x200B;文本字段中，输入引用`<ID>`的图像URL（包括图像预设或修饰符），而不是以下示例中的特定图像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果模板仅包含`<ID>`，则Dynamic Media将填充`https://<publishserver_name>/is/image/<company_name>/<ID>`，其中`<publishserver_name>`是您的发布服务器的名称在Dynamic Media Classic的“常规设置”中定义；`<company_name>`是与此AEM实例关联的公司根的名称，`<ID>`是通过要失效的资产选取器选择的资产。<br>任何预设／修改 `<ID>` 工具帖子均按原样复制在URL定义中。<br>只有图像(即， `/is/image` )才能基于模板自动形成。<br>对 `/is/content/`于，使用资产选取器添加视频或PDF等资产不会自动生成URL。您必须在CDN失效模板中指定此类资产，也可以在第2部分的&#x200B;*中手动将URL添加到此类资产：设置CDN失效选项*。<br>**示例：**<br>&#x200B;在第一个示例中，失效模板 `<ID>` 与具有的资产URL一起包含 `/is/content`。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。 Dynamic Media会根据此信息创建URL，其中`<ID>`是通过您希望使其失效的资产选取器选择的资产。<br>在第二个示例中，失效模板包含在Web属性中使用的资产的完整URL, `/is/content` 并且该URL不取决于资产选取器。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack`其中backpack是资产ID。<br>Dynamic Media支持的资产格式有资格失效。*不*&#x200B;支持CDN失效的资源文件类型包括Postscript、封装Postscript、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word和富文本格式。<br>创建模板时，请务必注意语法和错别字；Dynamic Media不执行任何模板验证。<br>请注意，您必须在此CDN失效模板或第2部分的添加URL文本字 **[!UICONTROL 段中]** 指定图像智 *能裁剪的URL:设置CDN失效选项。*<br>**重要：**CDN失效模板中的每个条目必须位于其自己的行中。<br>*以下模板示例仅供说明。* |

   ![CDN失效模板——创建](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 在&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;页面的右上角，点按&#x200B;**[!UICONTROL 保存]**，然后点按&#x200B;**[!UICONTROL 确定。]**<br>

   *第2部分，共2部分：设置CDN失效选项*
   <br>

1. 在AEM中作为Cloud Service，点按&#x200B;**[!UICONTROL 工具>资产> CDN失效。]**

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在&#x200B;**[!UICONTROL CDN失效——添加详细信息]**&#x200B;页面上，选择CDN失效的资源。

   ![CDN失效——添加详细信息](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您决定不选中“使CDN ]***和***[!UICONTROL &#x200B;基于模板&#x200B;]**失效”选项**[!UICONTROL &#x200B;使与资产相关的图像预设失效，则选定资产的基本URL会被形成为失效。 应仅对图像使用此选项排列。


   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中与资产关联的图像预设失效]** | （可选）选中此选项后，选定的资产及其所有关联的图像预设URL将自动生成，以便缓存失效。<br>资产及其关联的预定义预设URL会因失效而自动生成。此选项仅适用于图像资产。 |
   | **[!UICONTROL 基于模板的失效]** | （可选）选中此选项，仅使用定义的模板来形成URL。 |
   | **[!UICONTROL 添加资产]** | 使用资产选取器选择要失效的资产。 您可以选择已发布或已取消发布的资产。<br>CDN的缓存基于URL，而非基于资产。因此，您必须了解网站上的完整URL。 确定这些URL后，可以将其添加到模板。 然后，您可以选择并添加这些资产，并使URL失效。 <br>将此选项与CDN中与资 **[!UICONTROL 源关联的图像预设失效]**、基于 **[!UICONTROL 模板的失效或两者结合使用]**。 |
   | **[!UICONTROL 添加 URL]** | 手动添加或粘贴要使其CDN缓存失效的Dynamic Media资产的完整URL路径。 如果未在第2部分的&#x200B;***第1部分中创建CDN失效模板，请使用此选项：创建CDN失效模板***，并且只有少数资源可失效。<br>**重要：** 您添加的每个URL必须位于其自己的行中。<br>在指定时间最多可使1000个URL失效。如果&#x200B;**[!UICONTROL 添加URL]**&#x200B;文本字段中的URL数大于1000，则无法点按&#x200B;**[!UICONTROL Next]**。 在这种情况下，您必须点按选定资产右侧的&#x200B;**[!UICONTROL X]**&#x200B;或手动添加的URL，以将其从失效列表中删除。<br>请注意，您必须在CDN失效模板或此添加URL文本字段中为图像智 **[!UICONTROL 能裁]** 剪指定URL。 |

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 下一步。]**
1. 在&#x200B;**[!UICONTROL CDN失效——确认]**&#x200B;页面的&#x200B;**[!UICONTROL URL]**&#x200B;列表框中，您将看到一个列表，其中包含从您之前创建的CDN失效模板以及您刚刚添加的资源生成的一个或多个URL。

   例如，使用前面的步骤中显示的CDN失效模板示例，假定您添加了名为`spinset`的单个资源。 点按&#x200B;**[!UICONTROL 工具>资产> CDN失效]**&#x200B;时，会在&#x200B;**[!UICONTROL CDN失效——确认]**&#x200B;用户界面中生成以下五个URL:

   ![CDN失效——确认](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，点按URL右侧的&#x200B;**X**，将其从失效过程中删除。

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 提交]**&#x200B;以开始CDN失效过程。

## 排除CDN失效错误

在所有情况下，都会处理整个批以失效，或者整个批失败。

| 错误 | 说明 |
| --- | --- |
| *无法检索选定资产的URL。* | 如果满足以下任一情形，则发生：<br>-找不到Dynamic Media配置。<br>-检索用于读取Dynamic Media配置的服务用户时出现异常。<br>- Dynamic Media配置中缺少用于构成URL的发布服务器或公司根。 |
| *某些URL定义不正确。请更正并重新提交。* | 如果IPS CDN缓存失效API返回错误，称URL引用的是其他公司，或者URL无效（如IPS cdnCacheInvalidation API执行的验证），则发生。 |
| *无法使CDN缓存失效。* | 如果CDN缓存失效请求因任何其他原因失败发生。 |
| *未输入要失效的URL。* | 如果&#x200B;**[!UICONTROL CDN失效——确认]**&#x200B;页面中没有URL，则点按&#x200B;**[!UICONTROL 提交。]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
