---
title: 配置高级系统属性
seo-title: 配置高级系统属性
description: 使用“配置高级系统属性”页可以修改配置文件中的某些设置，而无需导出、编辑和导入文件。
seo-description: 使用“配置高级系统属性”页可以修改配置文件中的某些设置，而无需导出、编辑和导入文件。
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置高级系统属性 {#configure-advanced-system-attributes}

使用“配置高级系统属性”页可以修改配置文件中的某些设置，而无需导出、编辑和导入文件。 (请参阅 [导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。)

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>配置>配置高级系统属性]**。
1. （可选）更改以下任意会话属性：

   **** 会话超时限制（分钟）:用户自动从系统中注销之前的时间（以分钟为单位）。 默认情况下，无论活动或不活动，Workbench等AEM表单组件在两小时后都会超时，并且用户必须重新登录。 有效值 `1` 为 `1440`。 默认值是( `120` 2小时)。 此设置会更新 `SAML/Producer/assertionValidityInMinutes` 配置文件中的条目键。

   >[!NOTE]
   >
   >您不应将会话超时限制设置在10分钟以下，因为系统可能无法正常运行。 建议的值为10-120（分钟）。

   **** 断言阈值（秒）:用于抵消由群集中AEM表单应用程序服务器之间的系统时间差异导致的延迟的缓冲时间。 AEM表单按此属性中指定的时间（以秒为单位）来回溯用户的登录时间。 有效值 `0` 为 `3600`。 默认值为 `60`. 此设置会更新 `SAML/Producer/assertionThresholdInSeconds` 配置文件中的条目键。

   **** 断言的最大允许续订数：无需登录即可透明地续订用户会话的最大次数。 有效值 `0` 为 `9999`。 值表示 `0` 不续订断言。 默认值为 10。此设置会更新 `SAML/Producer/maxAssertionRenewalCount` 配置文件中的条目键。

1. （可选）更改以下任意目录同步属性：

   **** 同步统计记录：指定用户管理是否在同步过程中记录详细统计信息。 (请参阅 [在同步过程中启用或禁用详细记录](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)。)

   **** 同步Finisher Cron表达式：用户管理重试失败同步的间隔。 (请参 [阅配置目录同步重试选项](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)。)

   **** 群集作业锁定超时（以分钟为单位）:用于群集环境。 如果一个节点上的同步失败且群集锁定未释放，则此值指定另一个节点在强制获取锁定之前等待的分钟数。 The default value is `15` minutes. 有效值为 `1` 分钟 `1440` 数。

1. （可选）更改以下属性，然后单击“确 **[!UICONTROL 定”]**:

   **** 用户管理者事件审核：选择此选项可启用对目录同步事件和身份验证事件（如成功、失败和锁定）的审核。 默认情况下，除非您安装了需要审核的组件（如Rights Management），否则不会选择此选项。 此设置会更新 `APSAuditService` 配置文件中的条目键。

   **** 动态组的自动创建：支持基于电子邮件域自动创建动态组。 (请参 [阅创建动态组](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)。)

您还可以通过单击重新加载，还原到原始的用户管理设置。
