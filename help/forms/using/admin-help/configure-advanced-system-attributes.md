---
title: 配置高级系统属性
seo-title: Configure advanced system attributes
description: 使用“配置高级系统属性”页可以修改配置文件中的某些设置，而无需导出、编辑和导入文件。
seo-description: Use the Configure Advanced System Attributes page to modify certain settings in the configuration file without the need to export, edit, and import the file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# 配置高级系统属性 {#configure-advanced-system-attributes}

使用“配置高级系统属性”页可以修改配置文件中的某些设置，而无需导出、编辑和导入文件。 (请参阅 [导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>配置>配置高级系统属性]**.
1. （可选）更改以下任何会话属性：

   **会话超时限制（分钟）：** 用户自动注销系统之前经过的时间（以分钟为单位）。 默认情况下，AEM表单组件（如Workbench）会在两小时后超时，无论是否处于非活动状态，用户必须重新登录。 有效值为 `1` 到 `1440`. 默认值为 `120` （2小时）。 此设置将更新 `SAML/Producer/assertionValidityInMinutes` 输入键。

   >[!NOTE]
   >
   >不应将会话超时限制设置为低于10分钟，因为系统可能无法正常运行。 建议值为10-120（分钟）。

   **断言阈值（秒）：** 由于集群中AEM表单应用程序服务器之间的系统时间差而抵消延迟的缓冲时间。 AEM forms根据此属性中指定的时间量（以秒为单位）来回溯用户的登录时间。 有效值为 `0` 到 `3600`. 默认值为 `60`。此设置将更新 `SAML/Producer/assertionThresholdInSeconds` 输入键。

   **允许续订断言的最大值：** 无需登录即可透明续订用户会话的最大次数。 有效值为 `0` 到 `9999`. 值 `0` 意味着断言不会更新。 默认值为 10。此设置将更新 `SAML/Producer/maxAssertionRenewalCount` 输入键。

1. （可选）更改以下任何目录同步属性：

   **同步统计信息日志记录：** 指定用户管理是否在同步过程中记录详细的统计信息。 (请参阅 [在同步期间启用或禁用详细日志记录](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Synch Finisher Cron表达式：** User Management重试同步失败的间隔。 (请参阅 [配置目录同步重试选项](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **群集作业锁定超时（分钟）：** 在群集环境中使用。 如果一个节点上的同步失败且未释放群集锁定，该值指定另一个节点在强制获取锁定之前等待的分钟数。 默认值为 `15` 分钟。 有效值为 `1` 到 `1440` 分钟。

1. （可选）更改以下属性，然后单击 **[!UICONTROL 确定]**：

   **用户管理器事件审核：** 选择此选项可启用目录同步事件和身份验证事件（如成功、失败和锁定）的审核。 默认情况下，除非安装了需要审核的组件(例如Rights Management)，否则不会选择此选项。 此设置将更新 `APSAuditService` 输入键。

   **自动创建动态组：** 支持基于电子邮件域自动创建动态组。 (请参阅 [创建动态组](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

您还可以通过单击“重新加载”恢复为原始的“用户管理”设置。
