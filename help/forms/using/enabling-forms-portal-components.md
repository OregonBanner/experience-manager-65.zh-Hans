---
title: 启用表单门户组件
seo-title: 启用表单门户组件
description: 开箱即用地禁用Forms Portal组件。 启用“文档服务”和“文档服务”谓词组以启用Forms Portal组件。
seo-description: 开箱即用地禁用Forms Portal组件。 启用“文档服务”和“文档服务”谓词组以启用Forms Portal组件。
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# 启用Forms Portal组件{#enabling-forms-portal-components}

开箱即用的表单门户组件不可用。 要使组件显示在AEM Sidekick的可用组件列表中，请执行以下步骤：

1. 登录到网站的创作实例，然后打开AEM Sites页面。

1. 对于使用静态模板的页面，请执行以下步骤：

   1. 在页面标题中，点按![Canvas-drop-down](assets/canvas-drop-down.png) > **Design** ，以在设计模式下打开页面。
   1. 点按任意组件（带蓝色边框），然后点按![字段级别](assets/field-level.png)以选择包含当前组件的段落系统。
   1. 在段落系统中，点按![settings_icon](assets/settings_icon.png) ，打开段落系统的编辑对话框。
   1. 在&#x200B;**[!UICONTROL 允许的组件]**&#x200B;列表中，启用&#x200B;**[!UICONTROL Document Services]**&#x200B;和&#x200B;**[!UICONTROL Document Services谓词]**&#x200B;组件的复选框。 点按&#x200B;**[!UICONTROL 确定]**。

1. 对于使用动态模板的页面，请执行以下步骤：

   1. 在页面标题中，点按![属性](assets/properties.png) > **编辑模板**&#x200B;以打开页面的模板。
   1. 点按&#x200B;**布局容器** ，然后点按![FeedManagement](/help/forms/using/assets/feedmanagement.png)。 在&#x200B;**允许的组件**&#x200B;选项卡中，启用&#x200B;**文档服务和文档服务谓词**&#x200B;选项，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

>[!NOTE]
>
>您还可以通过选择这些类别中的组件来启用特定组件。 有关组件及其用法的更多信息，请参阅[创建表单门户页面](/help/forms/using/creating-form-portal-page.md)和[在页面](/help/forms/using/embedding-link-component-page.md)中嵌入链接组件。

现在，组件浏览器中提供了“文档服务”和“文档服务”谓词组件类别。 对于使用相同模板的所有页面，都会启用这些组件。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列出表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单简介](/help/forms/using/introduction-publishing-forms.md)
