---
title: 启用表单门户组件
seo-title: 启用表单门户组件
description: 开箱即用时，将禁用Forms Portal组件。 启用“文档服务”和“文档服务”谓词组以启用Forms Portal组件。
seo-description: 开箱即用时，将禁用Forms Portal组件。 启用“文档服务”和“文档服务”谓词组以启用Forms Portal组件。
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
translation-type: tm+mt
source-git-commit: a209b2dda04985a3f2d7c6838f11f0b5dc62d520

---


# 启用表单门户组件 {#enabling-forms-portal-components}

开箱即用的表单门户组件不可用。 要使组件显示在AEM Sidekick中的可用组件列表中，请执行以下步骤：

1. 登录到网站的作者实例，然后打开AEM站点页面。

1. 对于使用静态模板的页面，请执行以下步骤：

   1. 在页面标题中，点 ![按画布下拉框](assets/canvas-drop-down.png) > **设计** ，以在设计模式下打开页面。
   1. 点按任何组件（带蓝色边框），然后点 ![按字段级别](assets/field-level.png) ，以选择包含当前组件的段落系统。
   1. 在段落系统中，点按 ![settings_icon](assets/settings_icon.png) ，打开段落系统的编辑对话框。
   1. 从“允许的组 **[!UICONTROL 件”列表]**，启用“文档服务”和“文档服务”谓词组件的复选框 ******** 。 点按 **[!UICONTROL 确定]**。

1. 对于使用动态模板的页面，请执行以下步骤：

   1. 在页面标题中，点按 ![属性](assets/properties.png) > **编辑模板** ，以打开页面模板。
   1. 点按 **布局容器** ，然后点 ![按FeedManagement](/help/forms/using/assets/feedmanagement.png)。 在“允 **许的组件** ”选项卡中，启用“文档 **服务”和“文档服务谓词** ”选项，然后点 ![按aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

>[!NOTE]
>
>您还可以通过选择组件从这些类别中启用特定组件。 有关组件及其用法的详细信息，请参 [阅创建表单门户页面](/help/forms/using/creating-form-portal-page.md) , [以及在页面中嵌入链接组件](/help/forms/using/embedding-link-component-page.md)。

现在，“文档服务”和“文档服务谓词”组件类别在组件浏览器中可用。 对于使用相同模板的所有页面，都会启用这些组件。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列出表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)
