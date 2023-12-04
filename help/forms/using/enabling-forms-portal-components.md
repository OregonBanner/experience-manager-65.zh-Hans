---
title: 启用Forms Portal组件
seo-title: Enabling forms portal components
description: 现成Forms Portal组件已禁用。 启用Document Services和Document Services谓词组以启用Forms Portal组件。
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 5%

---

# 启用Forms Portal组件 {#enabling-forms-portal-components}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | 本文 |

表单门户组件现成不可用。 要使组件显示在AEM sidekick的可用组件列表中，请执行以下步骤：

1. 登录到网站的创作实例并打开AEM Sites页面。

1. 对于使用静态模板的页面，请执行以下步骤：

   1. 在页眉中，选择 ![画布下拉列表](assets/canvas-drop-down.png) > **设计** 以在设计模式下打开页面。
   1. 选择任意组件（使用蓝色边框），然后选择 ![字段级](assets/field-level.png) 以选择包含当前组件的段落系统。
   1. 在段落系统中，选择 ![settings_icon](assets/settings_icon.png) 打开段落系统的“编辑”对话框。
   1. 从列表 **[!UICONTROL 允许的组件]**，启用复选框 **[!UICONTROL 文档服务]** 和 **[!UICONTROL 文档服务谓词]** 组件。 选择 **[!UICONTROL 确定]**.

1. 对于使用动态模板的页面，请执行以下步骤：

   1. 在页眉中，选择 ![属性](assets/properties.png) > **编辑模板** 以打开页面的模板。
   1. 选择 **布局容器** 并选择 ![信息源管理](/help/forms/using/assets/feedmanagement.png). 在 **允许的组件** 选项卡，启用 **文档服务和文档服务谓词** 选项，然后选择 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>您还可以通过选择组件来启用这些类别中的特定组件。 有关组件及其用法的更多信息，请参阅 [创建表单门户页面](/help/forms/using/creating-form-portal-page.md) 和 [在页面中嵌入链接组件](/help/forms/using/embedding-link-component-page.md).

现在，在组件浏览器中提供了Document Services和Document Services谓词组件类别。 对于使用同一模板的所有页面，都会启用这些组件。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出网页上的表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)
