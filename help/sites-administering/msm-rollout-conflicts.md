---
title: MSM转出冲突
seo-title: MSM转出冲突
description: 了解如何处理多站点管理器转出冲突。
seo-description: 了解如何处理多站点管理器转出冲突。
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
translation-type: tm+mt
source-git-commit: 47b69098a45f774501ebb62ee1a14a8d209ad101

---


# MSM转出冲突{#msm-rollout-conflicts}

如果在Blueprint分支和从属Live Copy分支中都创建了具有相同页面名称的新页面，则可能会发生冲突。

此类冲突需要在转出时进行处理和解决。

## 冲突处理 {#conflict-handling}

当存在冲突的页面（在Blueprint和Live Copy分支中）时，MSM允许您定义应如何（甚至是如何）处理这些页面。

要确保转出未被阻止，可能的定义可以包括：

* 在转出过程中，哪个页面（Blueprint或Live Copy）将具有优先级，
* 将重命名哪些页面（以及如何重命名）,
* 这将如何影响任何已发布内容。

   AEM（现成）的默认行为是发布的内容不会受到影响。 因此，如果在Live Copy分支中手动创建的页面已发布，则该内容在冲突处理和转出后仍将发布。

除了标准功能之外，还可以添加自定义冲突处理程序以实现不同的规则。 这些组件还可以允许将发布操作作为单个进程执行。

### 示例方案 {#example-scenario}

在以下几节中，我们使用在Blueprint和Live copy分支（手动创建）中创建的新页面示例来说明解决冲突的各种方法： `b`

* blueprint: `/b`

   主页；1个子页，bp-level-1

* live copy: `/b`

   在Live copy分支中手动创建的页面；包含1个子页面 `lc-level-1`。

   * 发布时激活 `/b`为，以及子页面。

**转出前**

<table>
 <tbody>
  <tr>
   <td><strong>Blueprint在转出前</strong></td>
   <td><strong>转出前的Live Copy</strong></td>
   <td><strong>转出前发布</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> （在blueprint分支中创建，准备转出）<br /> </td>
   <td><code>b</code> <br /> （在Live copy分支中手动创建）<br /> </td>
   <td><code>b</code> <br /> （包含在Live copy分支中手动创建的页面b的内容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （在Live copy分支中手动创建）<br /> </td>
   <td><code> /lc-level-1</code> <br /> (包含在Live copy分支中手动创建的<br /> page child-level-1的内容)</td>
  </tr>
 </tbody>
</table>

## 转出管理器和冲突处理 {#rollout-manager-and-conflict-handling}

转出管理器允许您激活或取消激活冲突管理。

这是使用 [Day CQ WCM转出管理器](/help/sites-deploying/configuring-osgi.md)**的OSGi配置完成的**:

* **处理与手动创建的页面的冲突**:

   ( `rolloutmgr.conflicthandling.enabled`)

   如果转出管理器应处理来自在Live Copy中创建的页面的冲突，并且名称在Blueprint中存在，则设置为true。

在取消激 [活冲突管理时，AEM具有预定义的行为](#behavior-when-conflict-handling-deactivated)。

## 冲突处理程序 {#conflict-handlers}

AEM使用冲突处理程序解决将内容从Blueprint转出到Live Copy时存在的任何页面冲突。 重命名页面是解决此类冲突的一种（通常）方法。 可以操作多个冲突处理程序以允许选择不同的行为。

AEM提供：

* 默认 [冲突处理程序](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* 实现自定义处理 [程序的可能性](#customized-handlers)。
* 允许您设置每个处理函数的优先级的服务排名机制。 使用排名最高的服务。

### 默认冲突处理程序 {#default-conflict-handler}

默认冲突处理函数：

* 调用 `ResourceNameRolloutConflictHandler`

* 使用此处理函数时，Blueprint页面优先。
* 此处理函数的服务等级设置为低(即属性的默认值)，因 `service.ranking` 为假定自定义处理程序需要更高的级别。 但是，在需要时，排名并非确保灵活性的绝对最小值。

此冲突处理程序优先于Blueprint。 Live Copy页面 `/b` 将移至（在Live copy分支中） `/b_msm_moved`。

* live copy: `/b`

   将（在Live Copy中）移动到 `/b_msm_moved`。 这充当备份，并确保不会丢失任何内容。

   * `lc-level-1` 不移动。

* blueprint: `/b`

   转出到Live copy页面 `/b`。

   * `bp-level-1` 转出到Live Copy。

**转出后**

<table>
 <tbody>
  <tr>
   <td><strong>转出后的蓝图</strong></td>
   <td><strong>转出后的Live Copy</strong><br /> </td>
   <td></td>
   <td><strong>转出后的Live Copy</strong><br /> <br /><br /> </td>
   <td><strong>转出后发布</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （包含已转出的Blueprint页面的内容b）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （包含在Live copy分支中手动创建的页面b的内容）</td>
   <td><code>b</code> <br /> (无变动；包含在Live copy分支中手动创建的原始页面b的内容，现在称为b_msm_moved)<br /> </td>
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

自定义的冲突处理程序允许您实施自己的规则。 使用服务排名机制，您还可以定义它们与其他处理程序的交互方式。

自定义冲突处理程序可以：

* 根据您的要求命名。
* 根据您的要求开发／配置；例如，您可以开发一个处理程序，以便Live copy页面优先。
* 可以设计为使用 [OSGi配置进行配置](/help/sites-deploying/configuring-osgi.md);特别是：

   * **服务排名**:

      定义与其他冲突处理函数( `service.ranking`)相关的顺序。

      默认值为 0。

### 冲突处理已停用时的行为 {#behavior-when-conflict-handling-deactivated}

如果您手动取 [消激活冲突处理](#rollout-manager-and-conflict-handling) ，则AEM不会对任何冲突的页面执行任何操作（未冲突的页面会按预期方式转出）。

>[!CAUTION]
>
>AEM不会给出任何被忽略冲突的指示，因为必须显式配置此行为，因此假定它是必需的行为。

在这种情况下，Live copy将有效地优先。 Blueprint页面不 `/b` 会被复制，Live copy页面也 `/b` 不会变。

* blueprint: `/b`

   根本不复制，但会被忽略。

* live copy: `/b`

   保持原样。

<table>
 <caption>
   转出后
 </caption>
 <tbody>
  <tr>
   <td><strong>转出后的蓝图</strong></td>
   <td><strong>转出后的Live Copy</strong><br /> <br /><br /> </td>
   <td><strong>转出后发布</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (无变动；包含在Live copy分支中手动创建的页面b的内容)</td>
   <td><code>b</code> <br /> (无变动；包含在Live copy分支中手动创建的页面b的内容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （无更改）</td>
   <td><code> /lc-level-1</code> <br /> （无更改）</td>
  </tr>
 </tbody>
</table>

### 服务排名 {#service-rankings}

OSGi [](https://www.osgi.org/) 服务等级可用于定义单个冲突处理程序的优先级。
