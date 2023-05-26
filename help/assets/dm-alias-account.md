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

Dynamic Media URL和查看器嵌入代码包含您的公司帐户名称。 此帐户名是在配置Dynamic Media时创建的。 在某些情况下，您的企业可能会经历收购、品牌重塑，或者您只想使用更令人印象深刻的名称。 在这种情况下，在开箱即用的所有URL和查看器嵌入代码中手动更新公司帐户名称并不容易。 此外，还可能会影响现有Dynamic Media存储库或实时内容。 要解决此问题，您可以配置Dynamic Media公司别名帐户。

Dynamic Media公司别名帐户可确保用户界面中所有开箱即用的Dynamic Media URL和查看器嵌入代码反映对企业上下文所做的任何更新，例如品牌再造。 别名帐户也会对您的SEO（搜索引擎优化）产生积极影响，因为Dynamic Media URL和查看器嵌入代码会反映新的公司帐户名称。

配置Dynamic Media公司别名帐户时，请注意以下事项：

* 任何现有Dynamic Media URL或查看器嵌入代码 *实时* 必须手动更新数字属性以反映新的别名。 但是，任何使用您原始Dynamic Media公司名称嵌入代码的URL或查看器代码仍可用于现有资源或新资源。
* Dynamic Media公司别名帐户功能仅限于Experience Manager Assets创作模式和交付。 公司别名不适用于Experience Manager Sites。 没有为此更改更新WCM （Web内容管理）组件。 这些组件将继续使用原始Dynamic Media公司名称来获取Dynamic Media资源。
* 您只能在上设置一个公司别名帐户 **[!UICONTROL 编辑Dynamic Media配置]** 页面。 但是，您可以通过支持案例创建尽可能多的公司别名帐户，并在Dynamic Media URL或查看器嵌入代码中手动反映必要的别名。
* 开箱即用 [缓存失效](/help/assets/invalidate-cdn-cache-dynamic-media.md) Dynamic Media的功能可使在Cloud Services的“Dynamic Media配置”页面中配置的公司和公司别名帐户的URL失效。
* 在上配置公司别名帐户时 **[!UICONTROL 编辑Dynamic Media配置]** 页面，要使缓存失效成功，您必须使以下URL失效 *两者* 此 **[!UICONTROL 公司]** 帐户和 **[!UICONTROL 公司别名]** 帐户，同时。

另请参阅 [在Cloud Services中创建Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## 配置Dynamic Media公司别名帐户 {#configure-dm-alias-account}

您首先要提交支持案例，然后才能开始配置Dynamic Media公司别名帐户。 此步骤是必需的。

1. [使用Admin Console创建支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 在您的支持案例中提供以下信息：

   * 要使用的Dynamic Media公司别名。 名称必须包含 *仅限* 字母（允许混合大小写）、数字、连字符和下划线。
   * 您的地区。
   * 是否有 [规则集](/help/assets/using-rulesets-to-transform-urls.md) 以前用于通过替代Dynamic Media公司帐户名称来提供Dynamic Media内容。

1. 支持部门创建Dynamic Media别名帐户后，在Experience Manageras a Cloud Service创作实例中，选择Experience Manageras a Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，选择工具图标，然后转到 **[!UICONTROL Cloud Services> Dynamic Media配置]**.
1. 在“Dynamic Media配置浏览器”页面的左侧窗格中，选择 **[!UICONTROL 全局]** (请勿选择左侧的文件夹图标 **[!UICONTROL 全局]**)。 然后选择 **[!UICONTROL 编辑]**.

   ![Dynamic Media公司别名文本字段](/help/assets/assets-dm/dm-company-alias.png)

1. 在 **[!UICONTROL 编辑Dynamic Media配置]** 页面，在 **[!UICONTROL 公司别名]** 文本字段中，键入您之前在支持案例中指定的Dynamic Media别名帐户名称。
1. 在页面的右上角，选择 **[!UICONTROL 保存]**.
Dynamic Media公司别名帐户现已保存并启用；现有资源和新资源的所有URL和查看器嵌入代码现在都反映新的公司别名。
