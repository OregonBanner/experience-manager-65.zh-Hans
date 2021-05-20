---
title: 同步目录
seo-title: 同步目录
description: 了解如何使用手动或计划同步将用户管理数据库与源目录服务器的更改同步。
seo-description: 了解如何使用手动或计划同步将用户管理数据库与源目录服务器的更改同步。
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---

# 正在同步目录{#synchronizing-directories}

要同步域，您可以选择手动或计划同步。 *手动同步*&#x200B;同步任何选定的域。 *计划同步*&#x200B;同步所有域。

目录同步用于将您在目录设置中指定的目录服务器的详细信息提取到用户管理数据库。 之后，如果目录服务器上发生更改或更新，您也可以进行手动同步。 例如，如果添加了用户和组或对用户帐户进行了更改，则可以执行手动同步。

您还可以设置每日同步计划，以自动将用户管理数据库与源目录服务器的更改或更新同步。 但是，请注意，此过程使用网络和服务器资源。 选择使用率较低的时间段，并避免调度与系统和网络资源绑定的不必要同步。 要最大限度地减少不必要的同步，请改用即时同步选项。

您还可以指定在同步域时是否将用户和组信息推送到AdobeLiveCycleContent Services 9（已弃用）。

>[!NOTE]
>
>在LDAP目录同步过程中，请勿创建多个本地用户和组。 尝试此进程可能会导致错误。

>[!NOTE]
>
>如果域同步过程中断（例如，在该过程中应用程序服务器被关闭），请稍候再尝试同步该域。 要评估同步状态，请查看状态。 如果用户管理在关闭前获得了锁，请等待10分钟，以便在服务器重新启动后释放锁。 如果同步状态为“正在进行”，但同步被中断或停止，则用户管理会在3分钟后重试同步。 尝试三次失败后，用户管理会将同步声明为失败并释放锁定。

>[!NOTE]
>
>Adobe®LiveCycle® Content Services ES（已弃用）是随LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 内容服务（已弃用）支持将于12/31/2014终止。 请参阅[Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 要了解有关配置Content Services的信息（已弃用），请参阅[管理Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。

## 启用增量目录同步{#enable-delta-directory-synchronization}

增量目录同步提高了目录同步的效率。 启用增量目录同步后，用户管理仅同步自上次同步以来添加或更新的用户和组。

启用增量目录同步后，用户管理会执行以下步骤：

* 从目录服务器获取所有用户，但仅使用时间戳已更改的用户更新用户管理数据库。
* 获取所有组，但仅使用时间戳已更改的组更新用户管理数据库。
* 仅为时间戳已更改的组获取组成员，并使用该信息更新用户管理数据库。

>[!NOTE]
>
>从目录中删除的用户和组在执行完整目录同步之前不会从用户管理数据库中删除。

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 在“增量同步”(Delta Synch)下，选中该复选框，然后单击“保存”(Save)。
1. 编辑将使用增量目录同步功能的每个企业域的目录设置。 在“用户设置”和“组设置”页上，找到修改时间戳设置，然后输入`modify TimeStamp`作为值。 有关编辑企业域的详细信息，请参阅[编辑和转换现有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)。

## 在同步过程中启用或禁用详细日志记录{#enable-or-disable-detailed-logging-during-synchronization}

默认情况下，用户管理会记录同步过程中的详细统计信息。

1. 在管理控制台中，单击设置>用户管理>配置>配置高级系统属性。
1. 在同步统计记录下，取消选中该复选框以禁用详细日志记录或将其选中以启用日志记录，然后单击保存。

## 配置目录同步重试选项{#configure-the-directory-synchronization-retry-option}

您可以配置“用户管理”，以定期检查是否存在任何失败的目录同步尝试。 然后，用户管理尝试完成失败的同步。

1. 在管理控制台中，单击设置>用户管理>配置>配置高级系统属性。
1. 在同步分页装订器Cron表达式下，输入一个cron表达式，该表达式表示用户管理重试失败同步的间隔。 cron表达式的使用基于Quartz开源作业调度系统1.4.0版。

   默认值为0 0/13 &amp;ast;? &amp;ast;，这意味着每13分钟进行一次检查。

## 手动同步目录{#manually-synchronize-directories}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. （可选）要将用户和组信息推送到内容服务（已弃用），请选择选择此选项以将用户和组推送到注册的外部主体存储提供程序。 通过“用户和群组”页面添加新用户和组时，此选项也适用。
1. 选中要同步的每个企业域的复选框，然后单击立即同步。

   如果选择多个域，则可以同时运行所有域的域同步。 但是，如果单独选择域，则一次只能运行一个域同步。

## 计划目录同步{#schedule-directory-synchronization}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 计划同步：

   * 要每天启用自动同步，请在调度程序下，选择发生。 从列表中选择每日，然后在相应的框中键入24小时格式的时间。 保存设置时，此值将转换为CRON表达式，该表达式显示在“CRON表达式”框中。
   * 要计划在一周或月的特定日期或特定月的同步，请选择“Cron表达式”，然后在框中键入相应的表达式。 例如，在当月最后一个星期五的凌晨1:30进行同步。

cron表达式的使用基于Quartz开源作业调度系统1.4.0版。

* 要关闭自动同步，请选择“发生”，然后从列表中选择“从不”。
* （可选）要将用户和组信息推送到内容服务（已弃用），请选择选择此选项以将用户和组推送到注册的外部主体存储提供程序。 通过“用户和群组”页面添加新用户和组时，此选项也适用。
* 单击保存。

## 停止当前正在进行的所有目录同步{#stop-all-directory-synchronizations-currently-in-progress}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击中止。 此按钮仅在目录同步进行时显示。
