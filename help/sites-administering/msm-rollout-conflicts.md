---
title: MSM 转出冲突
seo-title: MSM Rollout Conflicts
description: 了解如何处理多站点管理器转出冲突。
seo-description: Learn how to deal with Multi Site Manager rollout conflicts.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 29%

---

# MSM 转出冲突{#msm-rollout-conflicts}

如果在Blueprint分支和从属Live Copy分支中创建具有相同页面名称的新页面，则可能会发生冲突。

转出时需要处理和解决此类冲突。

## 冲突处理 {#conflict-handling}

当存在冲突的页面（在Blueprint和Live Copy分支中）时，MSM允许您定义应如何处理（甚至是如果）这些页面。

为了确保转出不被阻止，可能的定义可以包括：

* 在转出过程中，哪个页面（blueprint或live copy）将具有优先级，
* 将重命名哪些页面（以及如何重命名）、
* 这将对任何已发布内容有何影响。

   AEM的默认行为（即装即用）是发布的内容将不会受到影响。 因此，如果在Live Copy分支中手动创建的页面已发布，则该内容在处理和转出冲突后仍会发布。

除了标准功能外，还可以添加自定义的冲突处理程序来实施其他规则。它们还允许将操作发布为单独的过程。

### 示例场景 {#example-scenario}

在以下部分中，我们使用了新页面的示例 `b`，创建于blueprint和live copy分支（手动创建）中，以说明各种冲突解决方法：

* Blueprint：`/b`

   主控页面；有1个子页，bp-level-1。

* live copy: `/b`

   在Live Copy分支中手动创建的页面；具有1个子页面， `lc-level-1`.

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
   <td><code>b</code> <br /> （在blueprint分支中创建，准备转出）<br /> </td>
   <td><code>b</code> <br /> （在live copy分支中手动创建）<br /> </td>
   <td><code>b</code> <br /> （包含在Live Copy分支中手动创建的页面b的内容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （在live copy分支中手动创建）<br /> </td>
   <td><code> /lc-level-1</code> <br /> (包含页面内容<br /> child-level-1（在live copy分支中手动创建）</td>
  </tr>
 </tbody>
</table>

## 转出管理器和冲突处理 {#rollout-manager-and-conflict-handling}

转出管理器允许您激活或停用冲突管理。

这是使用完成的 [OSGi配置](/help/sites-deploying/configuring-osgi.md) of **Day CQ WCM转出管理器**:

* **处理与手动创建的页面的冲突**:

   ( `rolloutmgr.conflicthandling.enabled`)

   如果转出管理器应处理来自在Live Copy中创建且Blueprint中存在名称的页面的冲突，则设置为true。

AEM [停用冲突管理时的预定义行为](#behavior-when-conflict-handling-deactivated).

## 冲突处理程序 {#conflict-handlers}

AEM使用冲突处理程序来解决在将内容从Blueprint转出到Live Copy时存在的任何页面冲突。 重命名页面是解决此类冲突的一种（通常）方法。 可以运行多个冲突处理程序以允许选择不同的行为。

AEM 提供：

* [默认冲突处理程序](#default-conflict-handler)：

   * `ResourceNameRolloutConflictHandler`

* 实施[自定义处理程序](#customized-handlers)的可能性。
* 服务排名机制，可让您设置每个单独处理程序的优先级. 使用排名最高的服务。

### 默认冲突处理程序 {#default-conflict-handler}

默认冲突处理程序：

* 调用 `ResourceNameRolloutConflictHandler`

* 对于此处理程序，Blueprint 页面将获得优先权。
* 此处理程序的服务排名设置得较低(“的默认值以下 `service.ranking` 属性)，因为假定自定义处理程序将需要更高的排名。 然而，排名并不是在必要时确保灵活性的绝对最低标准。

此处理程序为 Blueprint 页面提供优先权。Live Copy页面 `/b` 将（在live copy分支内）移动到 `/b_msm_moved`.

* live copy: `/b`

   将（在Live Copy中）移动到 `/b_msm_moved`. 这将充当备份，并确保不丢失任何内容。

   * 不会移动 `lc-level-1`。

* Blueprint：`/b`

   已转出到Live Copy页面 `/b`.

   * `bp-level-1` 将转出到Live Copy中。

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
   <td><code>b</code> <br /> （包含已推出的Blueprint页面b的内容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （具有在Live Copy分支中手动创建的页面b的内容）</td>
   <td><code>b</code> <br /> （无变动）包含在Live Copy分支中手动创建且现在称为b_msm_moved的原始页面b的内容<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （无更改）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> （无更改）</td>
  </tr>
 </tbody>
</table>

### 自定义处理程序 {#customized-handlers}

自定义冲突处理程序允许您实施自己的规则。利用服务排名机制，您还可以定义它们如何与其他处理程序交互。

自定义冲突处理程序可以：

* 根据您的要求进行命名。
* 根据您的要求开发/配置；例如，您可以开发一个处理程序，以便优先提供live copy页面。
* 可以设计为使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md);特别是：

   * **服务排名**:

      定义与其他冲突处理程序相关的顺序( `service.ranking`)。

      默认值为 0。

### 冲突处理停用时的行为 {#behavior-when-conflict-handling-deactivated}

如果您手动 [停用冲突处理](#rollout-manager-and-conflict-handling) 然后，AEM不对任何冲突页面执行任何操作（未冲突页面会按预期推出）。

>[!CAUTION]
>
>AEM不会指示冲突被忽略，因为必须明确配置此行为，因此假定它是必需行为。

在这种情况下，有效地优先使用Live Copy。 Blueprint页面 `/b` 将不会复制，并且Live Copy页面将不会复制 `/b` 保持不变。

* Blueprint：`/b`

   根本不复制，而是忽略。

* live copy: `/b`

   保持不变。

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
   <td><code>b</code> <br /> （无变动）具有在live copy分支中手动创建的页面b的内容)</td>
   <td><code>b</code> <br /> （无变动）包含在live copy分支中手动创建的页面b的内容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （无更改）</td>
   <td><code> /lc-level-1</code> <br /> （无更改）</td>
  </tr>
 </tbody>
</table>

### 服务排名 {#service-rankings}

[OSGi](https://www.osgi.org/) 服务排名可用于定义各个冲突处理程序的优先级。
