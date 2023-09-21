---
title: MSM 转出冲突
description: 了解如何处理多站点管理器转出冲突。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 23%

---

# MSM 转出冲突{#msm-rollout-conflicts}

如果在Blueprint分支和从属Live Copy分支中都创建了具有相同页面名称的新页面，则可能会发生冲突。

转出时必须处理和解决此类冲突。

## 冲突处理 {#conflict-handling}

当Blueprint和Live Copy分支中的页面存在冲突时，MSM允许您定义应如何（甚至是否）处理冲突。

为了确保转出不被阻止，可能的定义可以包括：

* 转出期间哪个页面（Blueprint或Live Copy）优先，
* 哪些页面被重命名（以及重命名的方式），
* 这会如何影响任何已发布的内容。

  Adobe Experience Manager (AEM)（现成）的默认行为是发布的内容不受影响。 因此，如果在Live Copy分支中手动创建的页面已发布，则该内容在冲突处理和转出后仍会发布。

除了标准功能外，还可以添加自定义的冲突处理程序来实施其他规则。它们还允许将操作发布为单独的过程。

### 示例场景 {#example-scenario}

在以下部分中，您必须使用新页面的示例 `b`，在Blueprint和Live Copy分支（手动创建）中创建，用于说明解决冲突的各种方法：

* Blueprint：`/b`

  母版页；带有一个子页面bp-level-1。

* live copy： `/b`

  在Live Copy分支中手动创建的页面；具有一个子页面， `lc-level-1`.

   * 在发布为 `/b` 时与子页面一起激活.

**转出前**

<table>
 <tbody>
  <tr>
   <td><strong>转出前的Blueprint</strong></td>
   <td><strong>转出前的Live Copy</strong></td>
   <td><strong>转出前发布</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> （在Blueprint分支中创建，可供转出）<br /> </td>
   <td><code>b</code><br /> <br /> （在live copy分支中手动创建）<br /> </td>
   <td><code>b</code><br /> <br /> （包含在live copy分支中手动创建的页面b的内容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> （在live copy分支中手动创建）<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> （包含页面的内容）<br /> 在live copy分支中手动创建的子级1)</td>
  </tr>
 </tbody>
</table>

## 转出管理器和冲突处理 {#rollout-manager-and-conflict-handling}

转出管理器让您激活或停用冲突管理。

可使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 之 **Day CQ WCM转出管理器**：

* **处理与手动创建的页面的冲突**：

  ( `rolloutmgr.conflicthandling.enabled`)

  如果转出管理器应处理Live Copy中创建的页面的名称与Blueprint中已存在的名称发生的冲突，则设置为true。

AEM具有 [已停用冲突管理时的预定义行为](#behavior-when-conflict-handling-deactivated).

## 冲突处理程序 {#conflict-handlers}

AEM使用冲突处理程序来解决在将内容从Blueprint转出到Live Copy时存在的任何页面冲突。 重命名页面是解决此类冲突的一种（常用）方法。 可以运行多个冲突处理程序以允许选择不同的行为。

AEM 提供：

* [默认冲突处理程序](#default-conflict-handler)：

   * `ResourceNameRolloutConflictHandler`

* 实施[自定义处理程序](#customized-handlers)的可能性。
* 服务排名机制，可让您设置每个单独处理程序的优先级. 使用排名最高的服务。

### 默认冲突处理程序 {#default-conflict-handler}

默认冲突处理程序：

* 称为 `ResourceNameRolloutConflictHandler`

* 使用此处理程序时，Blueprint页面将获得优先权。
* 此处理程序的服务排名设置得很低(即低于 `service.ranking` 属性)，因为假设自定义处理程序需要更高的排名。 然而，排名并不是在必要时确保灵活性的绝对最低标准。

此处理程序为 Blueprint 页面提供优先权。Live Copy页面 `/b` （在live copy分支中）移至 `/b_msm_moved`.

* live copy： `/b`

  （在Live Copy中）移至 `/b_msm_moved`. 这将充当备份，并确保不丢失任何内容。

   * 不会移动 `lc-level-1`。

* Blueprint：`/b`

  转出到Live Copy页面 `/b`.

   * `bp-level-1` 转出到live copy。

**转出后**

<table>
 <tbody>
  <tr>
   <td><strong>转出后的Blueprint</strong></td>
   <td><strong>转出后的Live Copy</strong><br /> </td>
   <td></td>
   <td><strong>转出后的Live Copy</strong><br /> <br /> <br /> </td>
   <td><strong>转出后发布</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> （具有已转出的Blueprint页面b的内容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> （具有在live copy分支中手动创建的页面b的内容）</td>
   <td><code>b</code><br /> <br /> （无更改；包含在live copy分支中手动创建的原始页面b的内容，现在称为b_msm_moved）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> （无更改）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> （无更改）</td>
  </tr>
 </tbody>
</table>

### 自定义处理程序 {#customized-handlers}

自定义冲突处理程序允许您实施自己的规则。 利用服务排名机制，您还可以定义它们如何与其他处理程序交互。

自定义的冲突处理程序可以具有以下内容：

* 根据您的要求命名。
* 根据您的要求开发/配置；例如，您可以开发一个处理程序，以便为Live Copy页面提供优先权。
* 设计为使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md)；特别是：

   * **服务排名**：

     定义与其他冲突处理程序相关的顺序( `service.ranking`)。

     默认值为 0。

### 冲突处理停用时的行为 {#behavior-when-conflict-handling-deactivated}

如果您手动 [取消激活冲突处理](#rollout-manager-and-conflict-handling)，则AEM不会对任何冲突页面执行任何操作（非冲突页面按预期转出）。

>[!CAUTION]
>
>AEM不会指示将忽略冲突，因为必须显式配置此行为，因此会假定这是必需的行为。

在这种情况下，Live Copy将获得优先权。 Blueprint页面 `/b` 不会复制且live copy页面不会复制 `/b` 保持不变。

* Blueprint：`/b`

  根本不复制，而是忽略。

* live copy： `/b`

  同样的。

<table>
 <caption>
   转出后
 </caption>
 <tbody>
  <tr>
   <td><strong>转出后的Blueprint</strong></td>
   <td><strong>转出后的Live Copy</strong><br /> <br /> <br /> </td>
   <td><strong>转出后发布</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> （无更改；具有在live copy分支中手动创建的页面b的内容）</td>
   <td><code>b</code><br /> <br /> （无更改；包含在live copy分支中手动创建的页面b的内容）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> （无更改）</td>
   <td><code> /lc-level-1</code><br /> <br /> （无更改）</td>
  </tr>
 </tbody>
</table>

### 服务排名 {#service-rankings}

[OSGi](https://www.osgi.org/) 服务排名可用于定义各个冲突处理程序的优先级。
