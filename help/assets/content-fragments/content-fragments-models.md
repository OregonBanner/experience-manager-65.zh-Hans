---
title: 内容片段模型
seo-title: 内容片段模型
description: 内容片段模型用于创建具有结构化内容的内容片段。
seo-description: 内容片段模型用于创建具有结构化内容的内容片段。
uuid: 73e38629-37c6-4f68-97a9-62f9783cc3d4
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 9da10294-2dc8-4e82-8d32-f034e6a5aeeb
docset: aem65
feature: 内容片段
role: User, Admin
exl-id: 76f3a684-027d-4822-9eb4-220fc96956e3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 21%

---

# 内容片段模型{#content-fragment-models}

内容片段模型定义[内容片段](/help/assets/content-fragments/content-fragments.md)的内容结构。

## 启用内容片段模型 {#enable-content-fragment-models}

>[!CAUTION]
>
>如果未启用&#x200B;**内容片段模型**，则&#x200B;**创建**&#x200B;选项将不可用于创建新模型。

要启用内容片段模型，您需要：

* 在[配置浏览器](/help/sites-administering/configurations.md)中启用内容片段模型的使用
* 将配置应用到Assets文件夹

### 在配置管理器中启用内容片段模型 {#enable-content-fragment-models-in-configuration-manager}

要[创建新的内容片段模型](#creating-a-content-fragment-model)，您&#x200B;**必须**&#x200B;首先使用配置管理器启用它们：

>[!CAUTION]
>
>不支持将子配置（嵌套在配置中的配置）与内容片段一起使用。

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用&#x200B;**Create**&#x200B;打开对话框，其中：

   1. 指定&#x200B;**标题**。
   1. 选择&#x200B;**内容片段模型**&#x200B;以启用其使用。

   ![cfm-6420-09](assets/cfm-6420-09.png)

1. 选择&#x200B;**创建**&#x200B;以保存定义。

<!-- 1. Select the location appropriate to your website. -->

### 将配置应用到您的Assets文件夹 {#apply-the-configuration-to-your-assets-folder}

为内容片段模型启用配置&#x200B;**全局**&#x200B;后，用户创建的任何模型都可以在任何Assets文件夹中使用。

要将其他配置（即不包括全局配置）与类似的 Assets 文件夹一起使用，您必须定义连接。可使用&#x200B;**云服务**&#x200B;选项卡（位于相应文件夹的&#x200B;**文件夹属性**&#x200B;中）中的&#x200B;**配置**&#x200B;完成来此操作。

## 创建内容片段模型 {#creating-a-content-fragment-model}

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。
1. 导航到适合您的[配置](#enable-content-fragment-models)的文件夹。
1. 使用&#x200B;**Create**&#x200B;打开向导。

   >[!CAUTION]
   >
   >如果[对内容片段模型的使用尚未启用](#enable-content-fragment-models)，则&#x200B;**创建**&#x200B;选项将不可用。

1. 指定&#x200B;**模型标题**。您还可以根据需要添加&#x200B;**描述**。

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. 使用&#x200B;**Create**&#x200B;保存空模型。 将显示一条消息，指示操作成功，您可以选择&#x200B;**打开**&#x200B;以立即编辑模型，或选择&#x200B;**完成**&#x200B;以返回到控制台。

## 定义内容片段模型 {#defining-your-content-fragment-model}

内容片段模型有效地定义了生成的内容片段的结构。 使用模型编辑器，您可以添加和配置必填字段：

>[!CAUTION]
>
>编辑现有内容片段模型可能会影响依赖的片段。

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 打开&#x200B;**Edit**&#x200B;所需的模型；使用快速操作，或选择模型，然后从工具栏中选择操作。

   打开模型编辑器后，会显示：

   * 左：字段已定义
   * 右侧：可用于创建字段的&#x200B;**数据类型**（可在创建字段后使用的&#x200B;**属性**）

   >[!NOTE]
   >
   >当字段为&#x200B;**必填字段**&#x200B;时，左窗格中显示的&#x200B;**标签**&#x200B;将标有一个星号标记 (*****)。

   ![cfm-6420-12](assets/cfm-6420-12.png)

1. **添加字段**

   * 将字段的必需数据类型拖到所需位置：

   ![cfm-6420-11](assets/cfm-6420-11.png)

   * 将字段添加到模型后，右侧面板将显示可为该特定数据类型定义的&#x200B;**属性**。 您可以在此定义该字段的必需内容。 例如：

   ![cfm-6420-13](assets/cfm-6420-13.png)

   >[!NOTE]
   对于数据类型&#x200B;**多行文本**，可将&#x200B;**默认类型**&#x200B;定义为以下任一类型：
   * **富文本**

   * **Markdown**

   * **纯文本**

   如果未指定，则此字段将使用默认值&#x200B;**富文本**。
   更改内容片段模型中的&#x200B;**默认类型**&#x200B;仅会对在编辑器中打开并保存的现有相关内容片段生效。

1. **删除字段**

   选择必填字段，然后单击/点按垃圾桶图标。 系统将要求您确认该操作。

   ![cf-32](assets/cf-32.png)

1. 添加所有必填字段并定义属性后，使用&#x200B;**Save**&#x200B;保留定义。 例如：

   ![cfm-6420-14](assets/cfm-6420-14.png)

## 删除内容片段模型 {#deleting-a-content-fragment-model}

>[!CAUTION]
删除内容片段模型可能会影响相关片段。

要删除内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 选择模型，然后从工具栏中选择&#x200B;**Delete**。

   >[!NOTE]
   如果引用了模型，则会发出警告。 采取适当措施。

## 发布内容片段模型 {#publishing-a-content-fragment-model}

在发布任何相关内容片段时/之前，需要发布内容片段模型。

要发布内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 选择您的模型，然后从工具栏中选择&#x200B;**Publish** 。

   >[!NOTE]
   如果发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。
