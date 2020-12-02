---
title: 使用Adobe Campaign表单组件创建自定义AEM页面模板
seo-title: 使用Adobe Campaign表单组件创建自定义AEM页面模板
description: 构建使用Adobe Campaign表单组件的自定义页面模板
seo-description: 构建使用Adobe Campaign表单组件的自定义页面模板
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 使用Adobe Campaign表单组件创建自定义AEM页面模板{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

本页介绍如何通过检查如何实现Geometrixx-户外模板(`/apps/geometrixx-outdoors/components/page_campaign_profile`)来构建使用[Adobe Campaign表单](/help/sites-authoring/adobe-campaign-components.md)组件的自定义页面模板，并指出创建自己的自定义模板时可能需要的重要信息。

>[!NOTE]
>
>[电子邮件和表单范例仅在Geometrixx中提供](/help/sites-developing/we-retail.md)。请从包共享下载示例Geometrixx内容。

要使用Adobe Campaign表单组件创建自定义AEM页面模板，请确保您具有以下各项：

1. **更正resourceSuperType**

   确保page-component从`mcm/campaign/components/profile`继承。

   这是Servlet获取和保存信息所必需的

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext设置**

   当您查看clientcontext设置(`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)时，您会看到以下设置：

   * ClientContext指向`/etc/clientcontext/campaign`
   * 还有额外的&#x200B;*config*&#x200B;节点。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   在&#x200B;**head.jsp**&#x200B;中，您将看到以下使用&#x200B;**clientcontext-config**&#x200B;和&#x200B;**cloudservice-hook**&#x200B;的行：

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   在&#x200B;**body.jsp**&#x200B;中，云服务加载到页面底部：

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **活动页面属性**

   要能够选择Adobe Campaign模板，请使用&#x200B;**活动**&#x200B;选项卡扩展page-properties:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **模板设置**。

   在模板(`/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)中，您会看到以下默认值：

   | **acMapping** | mapRecipient(对于Adobe Campaign6.1),用户档案(对于Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | 邮件 |

   ![chlimage_1-204](assets/chlimage_1-204.png)

