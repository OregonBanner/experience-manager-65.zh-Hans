---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: fa701a480af1d1f1860586db606f83446822f718
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 2%

---

# 安装 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有 [!DNL Adobe Experience Manager] 安装增强的连接器。 安装之前，请查看平台支持和其他 [连接器先决条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!TIP]
>
>您是否在 [!DNL Workfront for Experience Manager enhanced connector] AEMas a Cloud Service文档？ 单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en).

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署和配置时没有经过认证的合作伙伴或 [!DNL Adobe Professional Services]，则Adobe不支持此功能。
>
>* Adobe可发布 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器冗余；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强的连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强的连接器版本，请导航到 `digital.hoodoo` 组在 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans).
>
>* 请参阅 [Workfront的Experience Manager Assets增强连接器合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有关考试的信息，请参阅 [考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


要安装连接器，请执行以下步骤：

1. 从下载连接器 [[!DNL Software Distribution] 链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [配置防火墙](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. 在调度程序上，允许名为 `authorization`, `username`和 `apikey`. 允许 `GET`, `POST`和 `PUT` 请求 `/bin/workfront-tools`.
1. 确保中不存在以下路径 [!DNL Experience Manager] 存储库：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 使用安装包 [!UICONTROL 包管理器]. 要了解如何安装软件包，请参阅 [包管理器文档](/help/sites-administering/package-manager.md).
1. 创建 `wf-workfront-users` in [!DNL Experience Manager] 用户组并分配权限 `jcr:all` to `/content/dam`.

系统用户 `workfront-tools` 将自动创建，并自动管理所需的权限。 所有用户 [!DNL Workfront] 使用连接器的用户将自动添加到此组中。

## 配置之间的连接 [!DNL Experience Manager] 和 [!DNL Workfront] {#configure-connection}

要创建与Workfront的连接，请执行以下步骤：

1. 在 [!DNL Experience Manager]，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**.

1. 选择 `workfront-tools` ，然后选择 **[!UICONTROL 创建]** 选项。

1. 在 **[!UICONTROL Workfront连接]** 对话框中，提供您的 [!DNL Workfront] 部署，然后选择 **[!UICONTROL 连接到Workfront]** 选项。 成功连接后， [!DNL Workfront] 文档自定义集成将在 [!DNL Workfront] 环境。

   ![连接 [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 要验证连接，请在 [!DNL Workfront] 并验证API密钥是否相同且连接是否相同 **[!UICONTROL 已启用]**. 要执行此操作，请选择 **[!UICONTROL 设置]** > **[!UICONTROL 文档]** > **[!UICONTROL 自定义集成]** in [!DNL Workfront].

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets允许您更新 [!DNL Workfront for Experience Manager enhanced connector] 从以前的版本到最新版本。

要更新 [!DNL Workfront for Experience Manager enhanced connector] 到最新版本：

1. 从下载最新版本的增强型连接器 [[!DNL Software Distribution] 链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. 使用安装包 [!UICONTROL 包管理器]. 要了解如何安装软件包，请参阅 [包管理器文档](/help/sites-administering/package-manager.md).
