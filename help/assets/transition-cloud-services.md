---
title: 将翻译云服务应用到文件夹
description: 将翻译云服务应用到文件夹
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 将翻译云服务应用到文件夹 {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager(AEM)允许您从您选择的翻译提供商那里获得基于云的翻译服务，以确保您的资产已根据您的要求进行翻译。

您可以将翻译云服务直接应用到您的资产文件夹，以便在翻译工作流程中使用这些服务。

## 应用翻译服务 {#applying-the-translation-services}

将翻译云服务直接应用到您的资产文件夹，无需在创建或更新翻译工作流程时配置翻译服务。

1. 从“资产”用户界面中，选择要将翻译服务应用到的文件夹。
1. 在工具栏中，单击／点按属 **[!UICONTROL 性图标]** ，以显示“文件 **[!UICONTROL 夹属性]** ”页面。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 导航到云服 **[!UICONTROL 务选项卡]** 。
1. 从云服务配置列表中，选择所需的翻译提供商。 例如，如果要使用Microsoft的翻译服务，请选择“ **[!UICONTROL Microsoft Translator”]**。

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 为翻译提供者选择连接器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 在工具栏中，单击／点 **[!UICONTROL 按保存]**，然后单击确定以关 **** 闭对话框。翻译服务将应用于文件夹。

## 应用自定义翻译连接器 {#applying-custom-translation-connector}

如果要为要在翻译工作流程中使用的翻译服务应用自定义连接器。 要应用自定义连接器，请首先从“包管理器”安装连接器。 然后，从云服务控制台配置连接器。 配置连接器后，该连接器会显示在应用转换服务中所述云服务选项卡的 [连接器列表中](transition-cloud-services.md#applying-the-translation-services)。 应用自定义连接器并运行翻译工作流后，翻译项目的“ **[!UICONTROL Translation]** Summary”（翻译摘要）拼贴会在heads **[!UICONTROL Provider]** and **[!UICONTROL Method（提供者和方法）下显示连接器详细信息]**。

1. 从包管理器安装连接器。
1. 单击／点按AEM徽标，然后导航到工 **[!UICONTROL 具>部署>云服务]**。
1. 在“云服务”页面的“ **[!UICONTROL 第三方服务]** ”下找 **[!UICONTROL 到您安装的连接器]** 。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 单击／点按 **[!UICONTROL 立即配置]** ，打开创建配 **[!UICONTROL 置对话框]** 。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 指定连接器的标题和名称，然后单击／点按创 **[!UICONTROL 建]**。 自定义连接器位于应用翻译服务步骤5中所述的 **[!UICONTROL 云服务]** ，该连接器列 [表中](#applying-the-translation-services)。
1. 在应用自定义连接器后，运 [行创建翻译项目中描述的任何翻译](translation-projects.md) 工作流程。 在“项目”控制台中验证翻译项 **[!UICONTROL 目的“翻译摘要]** ”拼贴中连接器的 **[!UICONTROL 详细信息]** 。

   ![chlimage_1-220](assets/chlimage_1-220.png)
