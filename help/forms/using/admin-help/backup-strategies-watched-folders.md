---
title: 监视文件夹的备份策略
seo-title: 监视文件夹的备份策略
description: 本文档描述了受监视的文件夹如何受到不同备份和恢复方案的影响，这些方案的局限性和结果，以及如何最大限度地减少数据丢失。
seo-description: 本文档描述了受监视的文件夹如何受到不同备份和恢复方案的影响，这些方案的局限性和结果，以及如何最大限度地减少数据丢失。
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 2%

---


# 监视文件夹{#backup-strategies-for-watched-folders}的备份策略

本内容描述了监视的文件夹如何受到不同备份和恢复方案的影响，这些方案的局限性和结果，以及如何最大限度地减少数据丢失。

*监视* 文件夹是基于文件系统的应用程序，它调用已配置的服务操作，操作在监视的文件夹层次结构中的以下文件夹之一内操作文件：

* 输入
* 暂存
* 输出
* 失败
* 保留

用户或客户端应用程序首先将文件或文件夹放到输入文件夹中。 然后，服务操作将文件移入舞台文件夹进行处理。 服务执行指定操作后，会将修改后的文件保存到输出文件夹中。 已成功处理的源文件将移至保留文件夹，失败的处理文件将移至失败文件夹。 启用监视文件夹的`Preserve On Failure`属性后，已处理失败的源文件将移至保留文件夹。 （请参阅[配置监视的文件夹端点](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。）

可通过备份文件系统来备份监视的文件夹。

>[!NOTE]
>
>此备份独立于数据库或文档存储备份和恢复过程。

## 监视文件夹的工作方式{#how-watched-folders-work}

此内容描述了监视的文件夹文件处理过程。 在制定恢复计划之前，必须了解此过程。 在此示例中，已启用监视文件夹的`Preserve On Failure`属性。 文件将按文件到达的顺序进行处理。

下表描述了整个过程中五个示例文件(file1、file2、file3、file4、file5)的文件操作。 在表中，x轴表示时间（如时间1或T1）,y轴表示监视的文件夹层次结构（如输入）中的文件夹。

<table>
 <thead>
  <tr>
   <th><p>文件夹</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>输入</p></td>
   <td><p>file1、file2、file3、file4</p></td>
   <td><p>file2, file3, file4</p></td>
   <td><p>file3, file4</p></td>
   <td><p>file4</p></td>
   <td><p>空</p></td>
   <td><p>file5</p></td>
   <td><p>空</p></td>
  </tr>
  <tr>
   <td><p>暂存</p></td>
   <td><p>空</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>空</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>输出</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>失败</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file1 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2, file4 </p></td>
   <td><p>file1, file2, file4 </p></td>
  </tr>
 </tbody>
</table>

以下文本描述了每次的文件操作：

**T1：四** 个范例文件放在输入文件夹中。

**T2：服** 务操作将file1移入舞台文件夹进行操作。

**T3：服** 务操作将file2移入舞台文件夹进行操作。它将file1的结果放在output文件夹中，并将file1移到preserve文件夹。

**T4：服** 务操作将file3放在舞台文件夹中进行操作。它将file2的结果放在output文件夹中，并将file2放在preserve文件夹中。

**T5：服** 务操作将file4放在舞台文件夹中进行处理。文件3的操作失败，服务操作将它放在失败文件夹中。

**T6：服** 务操作将文件5放置在输入文件夹中。它将file4的结果放在output文件夹中，将file4放在preserve文件夹中。

**T7：服** 务操作将文件5放在舞台文件夹中进行处理。

## 备份监视文件夹{#backing-up-watched-folders}

建议您将整个监视文件夹文件系统备份到另一个文件系统。

## 恢复监视的文件夹{#restoring-watched-folders}

本节介绍如何恢复监视的文件夹。 监视的文件夹通常调用在一分钟内完成的短时进程。 在这种情况下，使用每小时完成的备份恢复监视的文件夹不会防止数据丢失。

例如，如果在T1时进行备份，而服务器在T7时失败，则file1、file2、file3和file4已经受到处理。 使用在T1执行的备份恢复监视的文件夹不会防止数据丢失。

如果执行了更新的备份，则可以恢复文件。 恢复文件时，请考虑当前文件所在的监视文件夹层次结构文件夹：

**阶段：** 恢复监视的文件夹后，将再次处理此文件夹中的文件。

**输入：** 恢复监视的文件夹后，将再次处理此文件夹中的文件。

**结果：** 不处理此文件夹中的文件。

**输出：** 不处理此文件夹中的文件。

**保留：** 不处理此文件夹中的文件。

## 最小化数据丢失的策略{#strategies-to-minimize-data-loss}

以下策略可以在恢复监视的文件夹时最大程度地减少输出和输入文件夹数据丢失：

* 频繁备份输出和失败文件夹（如每小时），以避免丢失结果和失败文件。
* 备份监视文件夹以外的文件夹中的输入文件。 这可确保在恢复后文件可用，以防您在输出或失败文件夹中找不到文件。 确保文件命名方案一致。

   例如，如果用&#x200B;`%F.`*extension*&#x200B;保存输出，则输出文件将与输入文件同名。 这有助于您确定要处理哪些输入文件以及必须重新提交哪些输入文件。 如果结果文件夹中只显示file1_out文件，而不显示file2_out、file3_out和file4_out，则必须重新提交file2、file3和file4。

* 如果可用的监视文件夹备份比处理作业所用的时间早，则应允许系统创建新的监视文件夹，并自动将文件放置在输入文件夹中。
* 如果最新可用备份时间不够，则备份时间小于处理文件所用的时间，并且已恢复监视的文件夹，则文件会在以下不同阶段之一进行处理：

   * **阶段1:** 在输入文件夹中
   * **阶段2:** 复制到阶段文件夹，但尚未调用该进程
   * **阶段3：复** 制到阶段文件夹并调用该进程
   * **阶段4:** 操作正在进行
   * **阶段5:** 返回结果

   如果文件在阶段1中，则将对它们进行操作。 如果文件在Stage 2或3中，请将它们放在输入文件夹中，以便再次进行处理。

   >[!NOTE]
   >
   >如果对文件进行多次操作，将防止数据丢失，但结果可能会重复。

## 结论{#conclusion}

由于监视文件夹的性质动态且不断更改，因此应使用一天内备份的文件恢复监视文件夹。 最佳做法是备份结果、将输入文件夹存储在服务器上并跟踪输入文件，以便在出现故障时重新提交作业。
