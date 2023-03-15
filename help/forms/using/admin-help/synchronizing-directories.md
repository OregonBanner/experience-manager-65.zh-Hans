---
title: 同步目录
seo-title: Synchronizing directories
description: 了解如何使用手动或计划同步将用户管理数据库与对源目录服务器的更改同步。
seo-description: Learn how to synchronize the User Management database with changes to the source directory servers using manual or scheduled synchronization.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: 2a2f8538b6554540b546f4d345c0b3c0d3e706f3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# 同步目录 {#synchronizing-directories}

要同步域，您可以选择执行手动同步或计划同步。 A *手动同步* 同步任何选定的域。 A *计划同步* 同步所有域。

目录同步用于将您在目录设置中指定的目录服务器的详细信息提取到用户管理数据库中。 之后，如果目录服务器上发生更改或更新，您也可以执行手动同步。 例如，如果添加用户和组或者对用户帐户进行更改，则可以执行手动同步。

您还可以设置每日同步计划，以自动将User Management数据库与对源目录服务器的更改或更新同步。 但是，请注意，此过程使用网络和服务器资源。 选择低使用时间段，并避免安排不必要的同步，以免占用系统和网络资源。 要最大限度地减少不必要的同步，请改用立即同步选项。

您还可以指定在同步域时是否将用户和组信息推送到AdobeLiveCycleContent Services 9（已弃用）。

>[!NOTE]
>
>请勿在LDAP目录同步过程中创建多个本地用户和组。 尝试此进程可能会导致错误。

>[!NOTE]
>
>如果域同步过程中断（例如，应用程序服务器在该过程中关闭），请稍等片刻，然后再尝试同步该域。 要评估同步状态，请查看状态。 如果User Management在关闭前获得锁定，请等待10分钟，以便在服务器重新启动后释放锁定。 如果同步状态为“进行中”，但同步被中断或停止，则用户管理将在3分钟后重试同步。 3次尝试失败后， User Management将同步声明为失败并释放锁定。

>[!NOTE]
>
>Adobe®LiveCycle®内容服务ES（已弃用）是随LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 内容服务（已弃用）支持于2014年12月31日终止。 参见 [Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## 启用增量目录同步 {#enable-delta-directory-synchronization}

增量目录同步提高了目录同步的效率。 启用增量目录同步后，用户管理仅同步自上次同步以来添加或更新过的用户和组。

启用增量目录同步时，用户管理会执行以下步骤：

* 从目录服务器获取所有用户，但只使用时间戳已更改的用户更新用户管理数据库。
* 获取所有组，但只使用时间戳已更改的组更新用户管理数据库。
* 仅获取时间戳已更改的组的组成员，并使用该信息更新用户管理数据库。

>[!NOTE]
>
>在执行完整的目录同步之前，不会从用户管理数据库中删除从目录中删除的用户和组。

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 在“增量同步”下，选中该复选框并单击“保存”。
1. 编辑将使用增量目录同步功能的每个企业域的目录设置。 在“用户设置”和“组设置”页面上，找到修改时间戳设置并输入 `modify TimeStamp` 作为值。 有关编辑企业域的详细信息，请参阅 [编辑和转换现有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## 在同步期间启用或禁用详细日志记录 {#enable-or-disable-detailed-logging-during-synchronization}

默认情况下，“用户管理”会在同步过程中记录详细的统计信息。

1. 在管理控制台中，单击设置>用户管理>配置>配置高级系统属性。
1. 在同步统计信息日志记录下，取消选中该复选框以禁用详细日志记录，或选中该复选框以启用日志记录，然后单击保存。

## 配置目录同步重试选项 {#configure-the-directory-synchronization-retry-option}

您可以配置用户管理定期检查任何失败的目录同步尝试。 然后，用户管理会尝试完成失败的同步。

1. 在管理控制台中，单击设置>用户管理>配置>配置高级系统属性。
1. 在同步完成器Cron表达式下，输入一个cron表达式，该表达式表示用户管理重试同步失败的时间间隔。 cron表达式的使用基于Quartz开源作业调度系统1.4.0版。

   缺省值为0 0/13 &amp;ast； ？ &amp;ast； ，这意味着每13分钟进行一次检查。

## 手动同步目录 {#manually-synchronize-directories}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. （可选）要将用户和组信息推送到Content Services（已弃用），请选择选择此选项以将用户和组推送到“已注册的外部主体存储提供程序”选项。 通过“用户和组”页面添加新用户和组时，此选项也适用。
1. 选中要同步的每个企业域的复选框，然后单击立即同步。

   如果选择多个域，则可以同时运行所有域的域同步。 但是，如果单独选择域，则一次只能运行一个域同步。

## 计划目录同步 {#schedule-directory-synchronization}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 计划同步：

   * 要每天启用自动同步，请在Scheduler下，选择Occurs。 从列表中选择“每日”，并在相应的框中以24小时制键入时间。 保存设置时，此值将转换为cron表达式，该表达式显示在Cron表达式框中。
   * 要安排在一周或一个月中的某一天或某一特定月份进行同步，请选择Cron表达式，然后在框中键入相应的表达式。 例如，在每月最后一个星期五凌晨1:30进行同步。

cron表达式的使用基于Quartz开源作业调度系统1.4.0版。

* 要关闭自动同步，请选择Occurs并从列表中选择Never。
* （可选）要将用户和组信息推送到Content Services（已弃用），请选择选择此选项以将用户和组推送到“已注册的外部主体存储提供程序”选项。 通过“用户和组”页面添加新用户和组时，此选项也适用。
* 单击“保存”。

## 停止当前正在进行的所有目录同步 {#stop-all-directory-synchronizations-currently-in-progress}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击“中止”。 此按钮仅在进行目录同步时显示。
