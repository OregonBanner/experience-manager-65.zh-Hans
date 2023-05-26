---
title: 根据使用的模板显示组件
seo-title: Displaying components based on the template used
description: 创建表单时，了解如何根据所选模板在侧栏中启用组件。
seo-description: When you create a form, learn how you can enable components in the sidebar based on the template selected.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# 根据使用的模板显示组件{#displaying-components-based-on-the-template-used}

当表单作者使用创建自适应表单时 [模板](../../forms/using/template-editor.md)，表单作者可以查看和使用基于模板策略的特定组件。 您可以指定一个模板内容策略，以便选择表单作者在表单创作时看到的一组组件。

## 更改模板的内容策略 {#changing-the-content-policy-of-a-template}

创建模板时，模板创建于 `/conf` 在内容存储库中。 基于您在中创建的文件夹 `/conf` 目录，模板的路径为： `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

执行以下步骤，根据模板的内容策略在侧栏中显示组件：

1. 打开CRXDE lite。\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. 在CRXDE中，导航到在其中创建模板的文件夹。

   例如：`/conf/<your-folder>/`

1. 在CRXDE中，导航到： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   要选择一组组件，需要新的内容策略。 要创建新策略，请复制并粘贴默认策略，然后对其进行重命名。

   默认内容策略的路径为： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   在 `gridFluidLayout` 文件夹，复制粘贴默认策略并对其进行重命名。 例如：`myPolicy`。

   ![复制默认策略](assets/crx-default1.png)

1. 选择您创建的新策略，然后选择 **组件** 右侧面板中具有类型的属性 `string[]`.

   选择并打开components属性时，您会看到“编辑组件”对话框。 通过“编辑组件”对话框，您可以使用组件组 **+** 和 **-** 按钮。 您可以添加包含您希望作者使用的表单的组件的组件组。

   ![在策略中添加或删除组件](assets/add-components-list1.png)

   添加组件组后，单击 **确定** 以更新列表，然后单击 **全部保存** 在CRXDE地址栏上方进行刷新。

1. 在模板中，将内容策略从默认策略更改为您创建的新策略。 ( `myPolicy` 在此示例中。)

   要更改策略，请在CRXDE中导航到 `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   在 `cq:policy` 属性，更改 `default` 到新策略名称( `myPolicy`)。

   ![已更新模板内容策略](assets/updated-policy.png)

   在创作使用该模板创建的表单时，您可以在侧栏中看到添加的组件。
