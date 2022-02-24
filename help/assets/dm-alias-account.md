---
title: 配置Dynamic Media公司别名帐户
description: 了解如何在Dynamic Media中配置公司别名帐户。
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# 关于配置Dynamic Media公司别名帐户 {#about-dm-alias-acct}

Dynamic Media URL和查看器嵌入代码包含您的公司帐户名称。 此帐户名称是在配置Dynamic Media时创建的。 在某些情况下，您的企业可能已经历了收购或品牌重新命名，或者您只想使用更令人难忘的名称。 在这些情况下，很难在所有现成的URL和查看器嵌入代码中手动更新您的公司帐户名称。 此外，您还可能会影响现有Dynamic Media存储库或影响实时内容。 要解决此问题，您可以配置Dynamic Media公司别名帐户。

Dynamic Media公司别名帐户可确保用户界面中所有现成的Dynamic Media URL和查看器嵌入代码都反映对您的业务上下文所做的任何更新，如重新品牌化。 别名帐户还对SEO（搜索引擎优化）产生了积极影响，因为Dynamic Media URL和查看器嵌入代码会反映新的公司帐户名称。

配置Dynamic Media公司别名帐户时，请注意以下事项：

* 您的任何现有Dynamic Media URL或查看器嵌入代码 *live* 必须手动更新数字属性，以反映新的别名。 但是，任何具有您原始Dynamic Media公司名称的URL或查看器嵌入代码都将继续适用于现有资产或新资产。
* Dynamic Media公司别名帐户功能仅限于Experience Manager Assets创作模式和交付。 公司别名不适用于Experience Manager Sites。 WCM（Web内容管理）组件不会因此更改而更新。 这些组件将继续使用原始Dynamic Media公司名称来获取Dynamic Media资产。
* 您只能在 **[!UICONTROL 编辑Dynamic Media配置]** 页面。 但是，您可以通过支持案例创建任意数量的公司别名帐户，并在Dynamic Media URL或查看器嵌入代码中手动反映必要的别名。
* 开箱即用 [缓存失效](/help/assets/invalidate-cdn-cache-dynamic-media.md) Dynamic Media的功能使在“Dynamic Media配置”页面中配置的公司帐户和公司别名帐户在Cloud Services中都无效的URL。
* 在 **[!UICONTROL 编辑Dynamic Media配置]** 页面，要使缓存失效成功，您必须使 *both* the **[!UICONTROL 公司]** 帐户和 **[!UICONTROL 公司别名]** 帐户，同时。

另请参阅 [在Cloud Services中创建Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## 配置Dynamic Media公司别名帐户 {#configure-dm-alias-account}

首先提交支持案例，即可开始配置Dynamic Media公司别名帐户。 此步骤是必需的。

1. [使用Admin Console创建支持案例](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. 在支持案例中提供以下信息：

   * 要使用的Dynamic Media公司别名。 名称必须包含 *仅* 字母（允许混合大小写）、数字、连字符和下划线。
   * 你的地区。
   * 是否有 [规则集](/help/assets/using-rulesets-to-transform-urls.md) 以前用于通过备用Dynamic Media公司帐户名称来提供Dynamic Media内容。

1. 在支持创建Dynamic Media别名帐户后，在Experience Manageras a Cloud Service创作实例中，选择Experience Manageras a Cloud Service徽标以访问全局导航控制台。
1. 在控制台的左侧，选择工具图标，然后转到 **[!UICONTROL Cloud Services> Dynamic Media配置]**.
1. 在Dynamic Media配置浏览器页面的左窗格中，选择 **[!UICONTROL 全球]** (请勿选择 **[!UICONTROL 全球]**)。 然后选择 **[!UICONTROL 编辑]**.

   ![Dynamic Media公司别名文本字段](/help/assets/assets-dm/dm-company-alias.png)

1. 在 **[!UICONTROL 编辑Dynamic Media配置]** 页面，在 **[!UICONTROL 公司别名]** 文本字段中，键入您之前在支持案例中指定的Dynamic Media别名帐户名称。
1. 在页面的右上角，选择 **[!UICONTROL 保存]**.
现在已保存并启用Dynamic Media公司别名帐户；现在，现有资产和新资产的所有URL和查看器嵌入代码都会反映新公司别名。
