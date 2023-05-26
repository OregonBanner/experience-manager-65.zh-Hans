---
title: 通过Dynamic Media使内容分发网络缓存失效
description: 使CDN（内容分发网络）缓存的内容失效可让您快速更新Dynamic Media交付的资产，而不是等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---


# 通过 Dynamic Media 使 CDN 缓存失效 {#invalidating-cdn-cache-for-dm-assets}

Dynamic Media资产通过CDN（内容分发网络）缓存，以便快速交付给客户。 但是，当您更新这些资产时，希望这些更改立即在您的网站上生效。 通过清除或使CDN缓存失效，可快速更新Dynamic Media交付的资源。 您可以在Dynamic Media中发送请求，让缓存在几分钟内过期，而不是使用TTL（生存时间）值（默认为10小时）等待缓存过期。



>[!IMPORTANT]
>
>以下步骤仅适用于Adobe Experience Manager 6.5、Service Pack 6(Experience Manager6.5.6)或更高版本中的Dynamic Media - Scene7模式。 此CDN失效功能还要求您使用与Adobe Experience Manager - Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。<br>如果您在Experience Manager6.5、Service Pack 5(Experience Manager6.5.5)或更早版本中使用Dynamic Media，请按照以下步骤操作： [通过Dynamic Media Classic使CDN缓存失效](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**要使Dynamic Media资源的CDN缓存内容失效，请执行以下操作：**

*第1部分（共2部分）：创建CDN失效模板*

1. 在Experience Manager6.5.6或更高版本中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL CDN失效]**.

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在 **[!UICONTROL CDN失效模板]** 页面，根据您的方案执行以下选项之一：

   | 方案 | 选项 |
   | --- | --- |
   | 我以前使用Dynamic Media Classic创建过CDN失效模板。 | 此 **[!UICONTROL 创建模板]** 文本字段已预填充了您的模板数据。 在这种情况下，您可以编辑模板或继续下一步骤。 |
   | 我必须创建一个模板。 我该输入什么？ | 在 **[!UICONTROL 创建模板]** 文本字段，输入引用图像URL（包括图像预设或修饰符） `<ID>`，而不是下面的示例中所述的特定图像ID：<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果模板仅包含 `<ID>`，然后Dynamic Media填充 `https://<publishserver_name>/is/image/<company_name>/<ID>` 位置 `<publishserver_name>` 是在Dynamic Media Classic的“常规设置”中定义的发布服务器的名称。 此 `<company_name>` 是与此Experience Manager实例关联的公司根的名称，并且 `<ID>` 是通过要失效的资产选取器选定的资产。<br>任何预设/修饰符发布 `<ID>` 在URL定义中按原样复制。<br>仅图像 — 即， `/is/image`  — 可以基于模板自动形成。<br>对象 `/is/content/`，使用资源选取器添加视频或PDF等资源不会自动生成URL。 相反，您必须在CDN失效模板中指定此类资源，或者可以手动将URL添加到中的此类资源 *第2部分（共2部分）：设置CDN失效选项*.<br>**示例：**<br>&#x200B;在第一个示例中，失效模板包含 `<ID>` 以及资源URL `/is/content`. 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media基于此路径通过 `<ID>` 是要使其失效的通过资产选取器选定的资产。<br>在第二个示例中，失效模板包含Web属性中使用的资产的完整URL，其中 `/is/content` （不依赖于资产选取器）。 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 其中，backpack是资产ID。<br>Dynamic Media中支持的资源格式符合失效条件。 资源文件类型 *非* 支持CDN失效的功能包括PostScript®、封装PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft®Powerpoint、Microsoft®Excel、Microsoft®Word和富文本格式。<br><br>·创建模板时，请务必注意语法和拼写错误；Dynamic Media不执行任何模板验证。<br>· CDN失效模板最多可保存2500个字符的文本。<br>·在此CDN失效模板中或在 **[!UICONTROL 添加URL]** 中的文本字段 *第2部分：设置CDN失效选项。*<br>· CDN失效模板中的每个条目必须位于其自己的行上。<br>·以下CDN失效模板示例仅用于演示目的。 |

   ![CDN失效模板 — 创建](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN失效模板最多可保存2500个字符的文本。

1. 在 **[!UICONTROL CDN失效模板]** 页面，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 确定]**.<br>

   *第2部分（共2部分）：设置CDN失效选项*
   <br>

1. 在Experience Manageras a Cloud Service中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL CDN失效]**.

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在 **[!UICONTROL CDN失效 — 添加详细信息]** 页面中，选择要使CDN失效的资产。

   ![CDN失效 — 添加详细信息](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您决定保留选项 **[!UICONTROL 使CDN中与资产关联的图像预设失效]** *和* **[!UICONTROL 基于模板失效]** 如果未选中，则会形成选定资产的基本URL以进行失效。 仅对图像使用此选项排列。


   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中与资产关联的图像预设失效]** | （可选）选中此选项后，会自动形成所选资源及其所有相关图像预设URL，以便使缓存失效。<br>资产及其关联的预定义预设URL会自动形成以便失效。 此选项仅适用于图像资产。 |
   | **[!UICONTROL 基于模板失效]** | （可选）选中此选项可仅使用定义的模板来构建URL。 |
   | **[!UICONTROL 添加资产]** | 使用资产选取器选择要使其失效的资产。 您可以选择已发布或已取消发布的资源。<br>CDN上的缓存基于URL，而不是基于资产。 因此，您必须了解您网站上的完整URL。 确定这些URL后，可以将其添加到模板中。 然后，您可以选择并添加这些资源，并在一个步骤中使URL失效。 <br>将此选项与 **[!UICONTROL 使CDN中与资产关联的图像预设失效]**，或 **[!UICONTROL 基于模板失效]**，或同时使用两者。 |
   | **[!UICONTROL 添加 URL]** | 手动将完整URL路径添加或粘贴到要使CDN缓存失效的Dynamic Media资源。 如果您没有在中创建CDN失效模板，请使用此选项 ***第1部分（共2部分）：创建CDN失效模板***，并且只有少数资产可失效。<br>**重要提示：** 您添加的每个URL都必须位于其自身的行中。<br>在给定时间内，最多可以使1000个URL失效。 如果 **[!UICONTROL 添加URL]** 文本字段大于1000，您无法选择 **[!UICONTROL 下一个]**. 在这种情况下，您必须选择 **[!UICONTROL X]** 右侧的选定资源或手动添加的URL以将其从失效列表中删除。<br>在CDN失效模板中或在此模板中指定图像智能裁剪的URL **[!UICONTROL 添加URL]** 文本字段。 |

1. 在页面的右上角附近，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL CDN失效 — 确认]** 页面，在 **[!UICONTROL URL]** 列表框中，您可以看到根据您之前创建的CDN失效模板以及您刚刚添加的资产生成的一个或多个URL的列表。

   例如，使用前面步骤中显示的CDN失效模板示例，假设您添加了一个名为的资产 `spinset`. 当您导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL CDN失效]**，它会在中生成以下五个URL **[!UICONTROL CDN失效 — 确认]** 用户界面：

   ![CDN失效 — 确认](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，请选择 **X** URL的右侧，以将其从失效进程中删除。

1. 在页面的右上角附近，选择 **[!UICONTROL 提交]** 以开始CDN失效过程。

## CDN失效错误疑难解答

在所有情况下，要么处理整个批次以使其失效，要么整个批次失败。

| 错误 | 解释 |
| --- | --- |
| *无法检索选定资产的URL。* | 如果满足以下任一方案，则发生：<br> — 未找到Dynamic Media配置。<br> — 检索用于读取Dynamic Media配置的服务用户时出现异常。<br>- Dynamic Media配置中缺少用于形成URL的发布服务器或公司根目录。 |
| *未正确定义某些URL。 更正并重新提交。* | 如果IPS CDN缓存失效API返回错误URL引用了其他公司，则会发生。 或者，如果URL根据IPS完成的验证无效 `cdnCacheInvalidation` API。 |
| *无法使CDN缓存失效。* | 在CDN缓存失效请求由于任何其他原因失败时发生。 |
| *没有输入要失效的URL。* | 如果中不存在URL，则会发生 **[!UICONTROL CDN失效 — 确认]** 页面，然后选择 **[!UICONTROL 提交]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
