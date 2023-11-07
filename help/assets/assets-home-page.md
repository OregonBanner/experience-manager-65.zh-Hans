---
title: '"[!DNL Assets] 主页体验”'
description: 个性化 [!DNL Experience Manager Assets] 主页提供了丰富的欢迎屏幕体验，包括有关资产的最近活动的快照。
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] 主页体验 {#aem-assets-home-page-experience}

个性化 [!DNL Adobe Experience Manager Assets] 主页提供了丰富的欢迎屏幕体验，包括有关资产的最近活动的快照。

[!DNL Assets] 主页提供了丰富而个性化的欢迎屏幕体验，包括最近活动的快照，例如最近查看或上传的资产。

此 [!DNL Assets] 默认禁用主页。 要启用该功能，请执行以下步骤：

1. 打开 [!DNL Experience Manager] 配置管理器 `https://[aem_server]:[port]/system/console/configMgr`.
1. 打开 **[!UICONTROL Day CQ DAM事件记录器]** 服务。
1. 选择 **[!UICONTROL 启用此服务]** 以启用活动录制。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 从 **[!UICONTROL 事件类型]** 列表中，选择要记录的事件，并保存更改。

   >[!CAUTION]
   >
   >启用“已查看资产”、“已查看项目”和“已查看收藏集”选项会显着增加记录的事件数。

1. 打开 **[!UICONTROL DAM资产主页功能标记]** 配置管理器中的服务 `https://[aem_server]:[port]/system/console/configMgr`.
1. 选择 `isEnabled.name` 用于启用 [!DNL Assets] 主页功能。 保存更改。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 打开 **[!UICONTROL 用户首选项]** 对话框，然后选择 **[!UICONTROL 启用资产主页]**. 保存更改。

   ![在“用户首选项”对话框中启用资源主页](assets/Annotation-color.png)

启用 [!DNL Assets] 主页，导航到 [!DNL Assets] 用户界面的“导航”页面，或直接从URL访问它 `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![在Assets用户界面上配置Experience Link](assets/config-experience-link.png)

单击 **[!UICONTROL 单击此处配置您的体验链接]** 添加用户名、背景图像和配置文件图像。

此 [!DNL Assets] 主页包含以下部分：

* 欢迎部分
* 构件部分

**欢迎部分**

如果您的配置文件存在，“欢迎”部分将显示一则发送给您的欢迎消息。 此外，它会显示您的个人资料图片和欢迎图像（如果已配置）。

如果您的配置文件不完整，欢迎部分将显示通用欢迎消息和配置文件图片的占位符。

**构件部分**

此部分显示在欢迎部分下方，并在以下部分下显示现成的构件：

* 活动
* 最近
* 发现

**活动**：在本节下， **[!UICONTROL 我的活动]** 小组件显示登录用户最近使用资产（包括没有演绎版的资产）执行的活动，例如资产上传、下载、资产创建、编辑、注释、注释和共享。

**最近**：和 **[!UICONTROL 最近查看的项目]** 此部分下的小组件显示登录用户最近访问的实体，包括文件夹、收藏集和项目。

**发现**：和 **[!UICONTROL 新建]** 此部分下的小组件显示最近上传到的资源和演绎版 [!DNL Assets] 部署。

要启用清除用户活动数据，请启用 **[!UICONTROL DAM事件清除服务]** 从Configuration Manager。 启用此服务后，系统会删除登录用户超出指定数量的活动。

“欢迎”屏幕提供了简单的导航帮助，例如，工具栏上的图标可访问文件夹、收藏集和目录。

>[!NOTE]
>
>启用 [!UICONTROL Day CQ DAM事件记录器] 和 [!UICONTROL DAM事件清除] 服务增加了对JCR的写入操作和搜索索引，从而显着增加了 [!DNL Experience Manager] 服务器。 上的附加负荷 [!DNL Experience Manager] 服务器可能会影响其性能。

>[!CAUTION]
>
>捕获、筛选和清除所需的用户活动 [!DNL Assets] 主页会对性能造成额外开销。 因此，管理员应该为目标用户有效地配置主页。
>
>Adobe建议执行批量操作的管理员和用户避免使用资产主页功能，以防止用户活动增加。 此外，管理员可以通过配置来排除特定用户的录制活动 [!UICONTROL Day CQ DAM事件记录器] 从 [!UICONTROL 配置管理器].
>
>如果使用该功能，Adobe建议您根据服务器负载安排清除频率。
