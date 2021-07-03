---
title: 通过Dynamic Media使CDN缓存失效
description: 通过使CDN（内容交付网络）缓存内容失效，您可以快速更新由Dynamic Media交付的资产，而无需等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
feature: CDN缓存
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 1%

---

# 通过Dynamic Media使CDN缓存失效 {#invalidating-cdn-cache-for-dm-assets}

Dynamic Media资产由CDN（内容交付网络）缓存，以便快速交付给客户。 但是，当您更新这些资产时，您希望这些更改在您的网站上立即生效。 通过清除或使CDN缓存失效，您可以快速更新由Dynamic Media交付的资产。 您可以在Dynamic Media中发送请求，让缓存在几分钟内过期，而不是等待缓存使用TTL（生存时间）值（默认值为10小时）过期。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。

>[!IMPORTANT]
>
>以下步骤仅适用于Adobe Experience Manager 6.5 Service Pack 6(Experience Manager6.5.6)或更高版本中的Dynamic Media - Scene7模式。 此CDN失效功能还要求您使用与Experience ManagerDynamic Media捆绑在一起的现成CDN;不支持任何其他自定义CDN。<br>如果您在Experience Manager6.5、Service Pack 5(Experience Manager6.5.5)或更早版本中使用Dynamic Media，请按照 [通过Dynamic Media Classic使CDN缓存失效](/help/assets/invalidate-cdn-cache-dm-classic.md)中的步骤操作。

另请参阅[Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)中的缓存概述。

**要使Dynamic Media资产的CDN缓存内容失效，请执行以下操作：**

*第1部分（共2部分）：创建CDN失效模板*

1. 在Experience Manager6.5.6或更高版本中，点按&#x200B;**[!UICONTROL 工具>资产> CDN失效]**。

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;页面上，根据您的方案执行以下任一选项：

   | 方案 | 选项 |
   | --- | --- |
   | 我以前已使用Dynamic Media Classic创建了CDN失效模板。 | **[!UICONTROL 创建模板]**&#x200B;文本字段已预填充模板数据。 在这种情况下，您可以编辑模板，也可以继续下一步。 |
   | 我必须创建一个模板。 我要输入什么？ | 在&#x200B;**[!UICONTROL 创建模板]**&#x200B;文本字段中，输入引用`<ID>`的图像URL（包括图像预设或修饰符），而不是像以下示例中所示的特定图像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果模板仅包含`<ID>`，则Dynamic Media会填入`https://<publishserver_name>/is/image/<company_name>/<ID>`中，其中`<publishserver_name>`是在Dynamic Media Classic的“常规设置”中定义的发布服务器名称。 `<company_name>`是与此Experience Manager实例关联的公司根目录的名称，`<ID>`是通过要失效的资产选取器选择的资产。<br>在URL定义中，所 `<ID>` 有预设/修饰符帖子都会按原样复制。<br>只能根据模板 `/is/image` 自动形成图像。<br>对 `/is/content/`于，使用资产选取器添加资产（如视频或PDF）时，不会自动生成URL。您而是必须在CDN失效模板中指定此类资产，或者可以在&#x200B;*第2部分（共2部分）中手动将URL添加到此类资产：设置CDN失效选项*。<br>**示例：**<br>&#x200B;在第一个示例中，失效模板包 `<ID>` 含的资产URL具有 `/is/content`。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。 Dynamic Media会根据此路径形成URL，其中`<ID>`是通过要失效的资产选取器选择的资产。<br>在第二个示例中，失效模板包含Web属性中所用资产的完整URL，其具 `/is/content` 体取决于资产选取器。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack`，其中，背包是资产ID。<br>Dynamic Media中支持的资产格式有资格失效。*不*&#x200B;支持CDN失效的资产文件类型包括PostScript®、封装的PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word和富文本格式。<br>创建模板时，请务必注意语法和拼写错误；Dynamic Media不执行任何模板验证。<br>在此CDN失效模板或第2部分的添加URL文本字 **[!UICONTROL 段中]** 指定图像智 *能裁剪的URL:设置CDN失效选项。*<br>**重要信息：**CDN失效模板中的每个条目必须位于其自身的行上。<br>*以下模板示例仅供说明之用。* |

   ![CDN失效模板 — 创建](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 在&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;页面的右上角，点按&#x200B;**[!UICONTROL Save]**，然后点按&#x200B;**[!UICONTROL OK]**。<br>

   *第2部分：设置CDN失效选项*
   <br>

1. 在作为Experience Manager的Cloud Service中，点按&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL CDN失效]**。

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在&#x200B;**[!UICONTROL CDN失效 — 添加详细信息]**&#x200B;页面上，选择要使CDN失效的资产。

   ![CDN失效 — 添加详细信息](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您决定取消选中&#x200B;**[!UICONTROL 使CDN中与资产关联的图像预设失效]** *和* **[!UICONTROL 基于模板无效]**&#x200B;选项，则会为失效形成选定资产的基本URL。 仅对图像使用此选项排列。


   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中与资产关联的图像预设失效]** | （可选）选中此选项后，为使缓存失效，会自动形成选定资产及其所有关联的图像预设URL。<br>资产及其关联的预定义预设URL将自动形成为失效。此选项仅适用于图像资产。 |
   | **[!UICONTROL 基于模板的失效]** | （可选）选中此选项可仅使用定义的模板进行URL形成。 |
   | **[!UICONTROL 添加资产]** | 使用资产选取器选择要失效的资产。 您可以选择已发布或未发布的资产。<br>CDN上的缓存基于URL，而不是基于资产。因此，您必须了解您网站上的完整URL。 确定这些URL后，可以将其添加到模板中。 然后，您可以选择并添加这些资产，并在一个步骤中使URL失效。 <br>将此选项与CDN中 **[!UICONTROL 与资产关联的图像预设]**&#x200B;结合使用，或与 **[!UICONTROL 基于模板失效]**&#x200B;结合使用，或与这两者结合使用。 |
   | **[!UICONTROL 添加 URL]** | 手动向要使其CDN缓存失效的Dynamic Media资产添加或粘贴完整URL路径。 如果未在2的&#x200B;***第1部分中创建CDN失效模板，请使用此选项：创建CDN失效模板***，并且只有少数资产要失效。<br>**重要信息：** 您添加的每个URL都必须位于其自身的行中。<br>您一次最多可以使1000个URL失效。如果&#x200B;**[!UICONTROL Add URL]**&#x200B;文本字段中的URL数大于1000，则无法点按&#x200B;**[!UICONTROL Next]**。 在这种情况下，您必须点按选定资产右侧的&#x200B;**[!UICONTROL X]**&#x200B;或手动添加的URL，以将其从失效列表中删除。<br>在CDN失效模板或此添加URL文本字段中，指定图像智能裁剪 **[!UICONTROL 的]** URL。 |

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL CDN失效 — Confirm]**&#x200B;页面的&#x200B;**[!UICONTROL URL]**&#x200B;列表框中，您可以看到从之前创建的CDN失效模板生成的一个或多个URL以及您刚才添加的资产列表。

   例如，使用前面步骤中显示的CDN失效模板示例，假设您添加了一个名为`spinset`的资产。 点按&#x200B;**[!UICONTROL 工具>资产> CDN失效]**&#x200B;时，它会在&#x200B;**[!UICONTROL CDN失效 — Confirm]**&#x200B;用户界面中生成以下五个生成的URL:

   ![CDN失效 — 确认](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，请点按URL右侧的&#x200B;**X** ，以将其从失效过程中删除。

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL Submit]**&#x200B;以开始CDN失效过程。

## 对CDN失效错误进行故障诊断

在所有情况下，都会处理整个批次以使其失效，或者整个批次失败。

| 错误 | 说明 |
| --- | --- |
| *无法检索选定资产的URL。* | 如果满足以下任何情况，则发生：<br> — 未找到Dynamic Media配置。<br> — 检索用于读取Dynamic Media配置的服务用户时出现异常。<br>- Dynamic Media配置中缺少用于构成URL的发布服务器或公司根目录。 |
| *某些URL定义不正确。更正并重新提交。* | 如果IPS CDN缓存失效API返回错误，导致URL引荐到其他公司，则发生。 或者，如果URL无效，与IPS `cdnCacheInvalidation` API完成的验证相同。 |
| *无法使CDN缓存失效。* | 在CDN缓存失效请求因任何其他原因失败时发生。 |
| *输入的URL无效。* | 如果&#x200B;**[!UICONTROL CDN失效 — 确认]**&#x200B;页面中不存在URL，然后点按&#x200B;**[!UICONTROL 提交]**，则会发生。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
