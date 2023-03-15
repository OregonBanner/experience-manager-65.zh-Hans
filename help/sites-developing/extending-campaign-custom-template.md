---
title: 使用Adobe Campaign表单组件创建自定义AEM页面模板
seo-title: Creating Custom AEM Page Template with Adobe Campaign Form Components
description: 构建使用Adobe Campaign表单组件的自定义页面模板
seo-description: Build a custom page template that uses Adobe Campaign Form components
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 3%

---

# 使用Adobe Campaign表单组件创建自定义AEM页面模板{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

本页介绍如何构建使用的自定义页面模板 [Adobe Campaign表单](/help/sites-authoring/adobe-campaign-components.md) 通过检查Geometrixx室外模板( `/apps/geometrixx-outdoors/components/page_campaign_profile`)，并指出了创建自己的自定义模板时可能需要的重要信息。

>[!NOTE]
>
>[电子邮件和表单示例仅在Geometrixx中可用](/help/sites-developing/we-retail.md). 请从“包共享”中下载 Geometrixx 示例内容。

要使用Adobe Campaign表单组件创建自定义AEM页面模板，请确保您满足以下条件：

1. **正确的resourceSuperType**

   确保页面组件继承自 `mcm/campaign/components/profile`.

   这是servlet获取和保存信息所必需的

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext设置**

   查看clientcontext设置时( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)，您将看到以下设置：

   * ClientContext指向 `/etc/clientcontext/campaign`
   * 此外，酒店还额外提供 *config* 节点。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   In **head.jsp**，您会看到以下使用 **clientcontext-config** 和 **cloudservice-hook**：

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   In **body.jsp**，则云服务将加载到页面底部：

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **营销活动页面属性**

   为了能够选择Adobe Campaign模板，使用扩展了页面属性 **Campaign** 选项卡：

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **模板设置**.

   在模板中( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)您将看到以下默认值：

   | **acMapping** | mapRecipient(适用于Adobe Campaign 6.1)，profile(适用于Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | 邮件 |

   ![chlimage_1-204](assets/chlimage_1-204.png)
