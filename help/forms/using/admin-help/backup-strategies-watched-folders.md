---
title: 已监视文件夹的备份策略
seo-title: 已监视文件夹的备份策略
description: 本文档介绍了已监视的文件夹如何受到不同备份和恢复方案的影响，这些方案的限制和结果，以及如何最大限度地减少数据丢失。
seo-description: 本文档介绍了已监视的文件夹如何受到不同备份和恢复方案的影响，这些方案的限制和结果，以及如何最大限度地减少数据丢失。
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 2%

---

# 监视文件夹{#backup-strategies-for-watched-folders}的备份策略

本内容介绍了已监视的文件夹如何受到不同备份和恢复方案的影响，这些方案的限制和结果，以及如何最大限度地减少数据丢失。

*监视文* 件夹是基于文件系统的应用程序，它调用已配置的服务操作，这些操作将在监视文件夹层次结构中的以下文件夹之一内处理文件：

* 输入
* 暂存
* 输出
* 失败
* 保留

用户或客户端应用程序首先将文件或文件夹放在输入文件夹中。 然后，服务操作将文件移入暂存文件夹进行处理。 服务执行指定操作后，会将修改后的文件保存到输出文件夹中。 已成功处理的源文件将移到保留文件夹，失败的处理文件将移到失败文件夹。 启用监视文件夹的`Preserve On Failure`属性后，失败的处理源文件将移至保留文件夹。 （请参阅[配置监视文件夹端点](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。）

您可以通过备份文件系统来备份已监视的文件夹。

>[!NOTE]
>
>此备份与数据库或文档存储备份和恢复过程无关。

## 监视文件夹的工作方式{#how-watched-folders-work}

此内容描述已监视的文件夹文件处理过程。 在制定恢复计划之前，务必要了解此过程。 在此示例中，已启用监视文件夹的`Preserve On Failure`属性。 文件会按文件到达的顺序进行处理。

下表描述了整个过程中对五个样例文件(file1、file2、file3、file4、file5)的文件操作。 在表中，x轴表示时间（如时间1或T1），y轴表示监视文件夹层次结构（如输入）中的文件夹。

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
   <td><p>file1, file2, file3, file4</p></td>
   <td><p>file2, file3, file4</p></td>
   <td><p>文件3，文件4</p></td>
   <td><p>file4</p></td>
   <td><p>空</p></td>
   <td><p>文件5</p></td>
   <td><p>空</p></td>
  </tr>
  <tr>
   <td><p>暂存</p></td>
   <td><p>空</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>文件3</p></td>
   <td><p>file4</p></td>
   <td><p>空</p></td>
   <td><p>文件5</p></td>
  </tr>
  <tr>
   <td><p>输出</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
  </tr>
  <tr>
   <td><p>失败</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file3_fail，file3 </p></td>
   <td><p>file3_fail，file3 </p></td>
   <td><p>file3_fail，file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file1 </p></td>
   <td><p>file1,file2 </p></td>
   <td><p>file1,file2 </p></td>
   <td><p>file1, file2, file4 </p></td>
   <td><p>file1, file2, file4 </p></td>
  </tr>
 </tbody>
</table>

以下文本描述了每次的文件操作：

**T1:** 四个示例文件放置在输入文件夹中。

**T2:** 服务操作将文件1移入暂存文件夹进行操作。

**T3:** 服务操作将file2移入暂存文件夹中进行操作。它将file1的结果放在输出文件夹中，并将file1移到保留文件夹。

**T4:** 服务操作将file3放置在stage文件夹中进行操作。它将file2的结果放在输出文件夹中，并将file2放在保留文件夹中。

**T5:** 服务操作将file4放置在stage文件夹中进行操作。文件3的操作失败，服务操作将其放在失败文件夹中。

**T6:** 服务操作将文件5放置在输入文件夹中。它将file4的结果放在输出文件夹中，将file4放在保留文件夹中。

**T7:** 服务操作将文件5放置在暂存文件夹中进行操作。

## 备份监视的文件夹{#backing-up-watched-folders}

建议您将整个监视文件夹文件系统备份到另一个文件系统。

## 恢复监视的文件夹{#restoring-watched-folders}

本节介绍如何恢复已监视的文件夹。 已监视的文件夹通常会调用在一分钟内完成的短暂进程。 在这种情况下，使用每小时完成一次的备份来恢复已监视的文件夹不会阻止数据丢失。

例如，如果在T1备份时，服务器在T7出现故障，则文件1、文件2、文件3和文件4都已被处理。 使用在T1执行的备份还原已监视的文件夹，不会阻止数据丢失。

如果执行了更新的备份，则可以恢复文件。 恢复文件时，请考虑当前文件所在的监视文件夹层次结构文件夹：

**暂存：** 在还原已监视的文件夹后，将再次处理此文件夹中的文件。

**输入：** 在恢复监视的文件夹后，将再次处理此文件夹中的文件。

**结果：** 不处理此文件夹中的文件。

**输出：** 不处理此文件夹中的文件。

**保留：** 不处理此文件夹中的文件。

## 最大限度地减少数据丢失的策略{#strategies-to-minimize-data-loss}

以下策略可在还原已监视的文件夹时最大限度地减少输出和输入文件夹数据丢失：

* 经常备份输出和失败文件夹（如每小时），以避免丢失结果和失败文件。
* 将输入文件备份到监视文件夹以外的文件夹中。 这可确保在恢复后文件的可用性，以防在输出或失败文件夹中找不到文件。 确保文件命名方案一致。

   例如，如果要保存的输出具有&#x200B;`%F.`*extension*，则输出文件将与输入文件同名。 这有助于您确定要处理哪些输入文件以及必须重新提交哪些输入文件。 如果在结果文件夹中只看到file1_out文件，而没有看到file2_out、file3_out和file4_out文件，则必须重新提交file2、file3和file4。

* 如果可用的监视文件夹备份的时间早于处理作业所花费的时间，则应允许系统创建新的监视文件夹，并自动将文件放入输入文件夹中。
* 如果最新的可用备份时间不够，则备份时间少于处理文件所花费的时间，并且已恢复监视的文件夹，则文件会在以下不同阶段之一进行处理：

   * **阶段1:** 在输入文件夹中
   * **阶段2:** 已复制到阶段文件夹，但尚未调用该进程
   * **阶段3:** 复制到阶段文件夹并调用进程
   * **阶段4:** 正在进行的操作
   * **阶段5:** 返回结果

   如果文件在阶段1中，则将处理它们。 如果文件位于阶段2或3中，请将它们置于输入文件夹中以便再次进行操作。

   >[!NOTE]
   >
   >如果对文件进行多次操作，将阻止数据丢失，但结果可能会重复。

## 结论 {#conclusion}

由于监视文件夹的性质是动态的，而且不断变化，因此应使用一天内备份的文件来恢复监视文件夹。 最佳做法是备份结果、将输入文件夹存储在服务器上并跟踪输入文件，以便在失败时可以重新提交作业。
