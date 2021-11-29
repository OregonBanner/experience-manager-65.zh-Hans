---
title: 创建Assets文件夹无标题快速入门指南
description: 使用AEM内容片段模型来定义内容片段的结构，这是您无头内容的基础。
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
source-git-commit: a5cb385aa369a5e59889e77597119358b77b55be
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 1%

---

# 创建Assets文件夹无标题快速入门指南 {#creating-an-assets-folder}

使用AEM内容片段模型来定义内容片段的结构，这是您无头内容的基础。 然后，内容片段将存储在资产文件夹中。

##  什么是资产文件夹？ {#what-is-an-assets-folder}

[现在，您已创建内容片段模型](create-content-model.md) 定义了希望用于将来内容片段的结构，您可能很兴奋地创建一些片段。

但是，您首先需要创建一个资产文件夹，以便将其存储在该文件夹中。

资产文件夹用于 [组织传统内容资产](/help/assets/manage-assets.md) ，例如图像和视频以及内容片段。

## 如何创建资产文件夹 {#how-to-create-an-assets-folder}

管理员在创建内容时，只需偶尔创建文件夹即可组织内容。 出于本快速入门指南的目的，我们只需创建一个文件夹。

1. 登录AEM，然后从主菜单中选择 **导航 — >资产 — >文件**.
1. 点按或单击 **创建 — >文件夹**.
1. 提供 **标题** 和 **名称** 文件夹的URL。
   * 的 **标题** 应具有描述性。
   * 的 **名称** 将成为存储库中的节点名称。
      * 将根据标题自动生成并根据 [AEM命名约定。](/help/sites-developing/naming-conventions.md)
      * 如有必要，可进行调整。

   ![创建文件夹](../assets/assets-folder-create.png)
1. 选择之前创建的文件夹，然后选择 **属性** (或使用 `p` [键盘快捷键。](/help/sites-authoring/keyboard-shortcuts.md))
1. 在 **属性** 窗口，选择 **Cloud Services** 选项卡。
1. 对于 **云配置** 选择 [配置。](create-configuration.md)

   ![配置资产文件夹](../assets/assets-folder-configure.png)
1. 点按或单击 **保存并关闭**.
1. 点按或单击 **确定** 在确认窗口中。

   ![确认窗口](../assets/assets-folder-confirmation.png)

您可以在刚刚创建的文件夹中创建其他子文件夹。 子文件夹将继承 **云配置** 的子目录访问Advertising Cloud帮助。 但是，如果您希望使用其他配置中的模型，则可以覆盖此值。

如果您使用的是本地化的站点结构，则可以 [创建语言根](/help/assets/multilingual-assets.md) 下。

## 后续步骤 {#next-steps}

现在，您已为内容片段创建文件夹，接下来可以转到入门指南的第四部分和 [创建内容片段。](create-content-fragment.md)

>[!TIP]
>
>有关管理内容片段的完整详细信息，请参阅 [内容片段文档](/help/assets/content-fragments/content-fragments.md)
