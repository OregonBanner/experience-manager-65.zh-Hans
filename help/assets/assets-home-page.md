---
title: '[!DNL Assets] 主页体验'
description: 个性化 [!DNL Experience Manager Assets] 主页，获得丰富的欢迎屏幕体验，包括资产最近活动的快照。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] 主页体验  {#aem-assets-home-page-experience}

个性化[!DNL Adobe Experience Manager Assets]主页，获得丰富的欢迎屏幕体验，包括资产最近活动的快照。

[!DNL Assets] 主页提供丰富且个性化的欢迎屏幕体验，其中包括最近活动的快照，如最近查看或上传的资产。

默认情况下，[!DNL Assets]主页处于禁用状态。 要启用它，请执行以下步骤：

1. 打开[!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`。
1. 打开&#x200B;**[!UICONTROL Day CQ DAM事件记录器]**&#x200B;服务。
1. 选择&#x200B;**[!UICONTROL 启用此服务]**&#x200B;以启用活动录制。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 从&#x200B;**[!UICONTROL 事件类型]**&#x200B;列表中，选择要记录的事件并保存更改。

   >[!CAUTION]
   >
   >启用“已查看资产”、“已查看项目”和“已查看集合”选项，可显着增加已记录事件的数量。

1. 从Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`打开&#x200B;**[!UICONTROL DAM资产主页功能标志]**&#x200B;服务。
1. 选择`isEnabled.name`选项以启用[!DNL Assets]主页功能。 保存更改。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 打开&#x200B;**[!UICONTROL 用户首选项]**&#x200B;对话框，然后选择&#x200B;**[!UICONTROL 启用资产主页]**。 保存更改。

   ![在“用户首选项”对话框上启用资产主页](assets/Annotation-color.png)

启用[!DNL Assets]主页后，从“导航”页面导航到[!DNL Assets]用户界面，或直接从URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`访问它。

![在资产用户界面上配置体验链接](assets/config-experience-link.png)

单击&#x200B;**[!UICONTROL 单击此处配置您的体验链接]**&#x200B;以添加您的用户名、背景图像和用户档案图像。

[!DNL Assets]主页包含以下部分：

* 欢迎部分
* 构件部分

**欢迎部分**

如果您的用户档案存在，欢迎部分将显示一封发送给您的欢迎邮件。 此外，它还显示您的用户档案图片和欢迎图像（如果已配置）。

如果您的用户档案不完整，“欢迎”部分将显示一条通用的欢迎消息和用户档案图片的占位符。

**构件部分**

此部分显示在欢迎部分的下方，并在以下部分下显示现成构件：

* 活动
* 最近
* 发现

**活动**:在此部分中，“我 **[!UICONTROL 的]** 活动”构件显示登录用户使用资产（包括无演绎版的资产）执行的最近活动，例如资产上传、下载、资产创建、编辑、注释、批注和共享。

**最近**:此部 **[!UICONTROL 分]** 下的“最近查看的”构件显示登录用户最近访问的实体，包括文件夹、集合和项目。

**发现**:此部 **** 分下的新构件显示最近上传到部署的资产和演 [!DNL Assets] 绎版。

要启用清除用户活动数据，请从Configuration Manager中启用&#x200B;**[!UICONTROL DAM事件清除服务]**。 启用此服务后，系统将删除超过指定数量的登录用户活动。

欢迎屏幕提供简单的导航帮助，例如，工具栏上的图标可访问文件夹、集合和目录。

>[!NOTE]
>
>启用[!UICONTROL Day CQ DAM事件记录器]和[!UICONTROL DAM事件清除]服务会增加对JCR的写入操作和搜索索引，这会显着增加[!DNL Experience Manager]服务器上的负载。 [!DNL Experience Manager]服务器上的额外负载会影响其性能。

>[!CAUTION]
>
>捕获、过滤和清除[!DNL Assets]活动所需的用户主页会对性能造成开销。 因此，管理员应该为主页用户有效配置目标。
>
>Adobe建议执行批量操作的管理员和用户避免使用资产主页功能来防止用户活动增加。 此外，管理员可以从[!UICONTROL Configuration Manager]中配置[!UICONTROL Day CQ DAM事件记录器]，从而排除特定用户的录制活动。
>
>如果您使用该功能，Adobe建议您根据服务器负载计划清除频率。
