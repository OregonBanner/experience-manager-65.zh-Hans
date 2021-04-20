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
feature: Multi Site Manager
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 0%

---


# MSM转出冲突{#msm-rollout-conflicts}

如果在Blueprint分支和从属Live Copy分支中创建了具有相同页面名称的新页面，则可能会发生冲突。

此类冲突需要在转出时进行处理和解决。

## 冲突处理{#conflict-handling}

当存在冲突的页面（在Blueprint和Live Copy分支中）时，MSM允许您定义应如何（甚至是如何）处理这些页面。

要确保转出未被阻止，可能的定义可以包括：

* 在转出过程中，哪个页面（blueprint或live copy）将具有优先级，
* 将重命名哪些页面（以及如何），
* 这将如何影响任何已发布内容。

   AEM（现成）的默认行为是发布的内容不会受到影响。 因此，如果在Live Copy分支中手动创建的页面已发布，则该内容仍将在冲突处理和转出后发布。

除了标准功能，还可以添加自定义冲突处理程序以实施不同的规则。 这些组件还允许将发布操作作为单个进程执行。

### 方案{#example-scenario}示例

在以下各节中，我们将使用在Blueprint和Live Copy分支（手动创建）中创建的新页面`b`的示例来说明各种冲突解决方法：

* blueprint:`/b`

   主控页面；1页，bp-level-1

* live copy:`/b`

   在Live Copy分支中手动创建的页面；包含1个子页面，`lc-level-1`。

   * 在发布时作为`/b`以及子页面激活。

**转出前**

<table>
 <tbody>
  <tr>
   <td><strong>buelpint</strong></td>
   <td><strong>转出前</strong></td>
   <td><strong>在转出前发布</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> （在blueprint branch中创建，准备转出）<br /> </td>
   <td><code>b</code> <br /> （在Live Copy分支中手动创建）<br /> </td>
   <td><code>b</code> <br /> （包含在Live Copy分支中手动创建的页面b的内容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （在Live Copy分支中手动创建）<br /> </td>
   <td><code> /lc-level-1</code> <br /> （包含在Live Copy分支中手动创建的页面<br /> child-level-1的内容）</td>
  </tr>
 </tbody>
</table>

## 转出管理器和冲突处理{#rollout-manager-and-conflict-handling}

转出管理器允许您激活或取消激活冲突管理。

使用&#x200B;**Day CQ WCM转出管理器**&#x200B;的[OSGi configuration](/help/sites-deploying/configuring-osgi.md)完成此操作：

* **处理与手动创建的页面的冲突**:

   (`rolloutmgr.conflicthandling.enabled`)

   如果转出管理器应处理在Live Copy中创建的页面中的冲突，并且名称在Blueprint中存在，则设置为true。

当冲突管理已停用](#behavior-when-conflict-handling-deactivated)时，AEM具有[预定义行为。

## 冲突处理程序{#conflict-handlers}

AEM使用冲突处理程序解决将内容从blueprint转出到Live Copy时存在的任何页面冲突。 重命名页面是解决此类冲突的一种（通常）方法。 可以操作多个冲突处理程序以允许选择不同的行为。

AEM提供：

* [默认冲突处理函数](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* 实现[自定义处理程序](#customized-handlers)的可能性。
* 允许您设置每个处理程序的优先级的服务排名机制。 使用排名最高的服务。

### 默认冲突处理程序{#default-conflict-handler}

默认冲突处理程序：

* 名为`ResourceNameRolloutConflictHandler`

* 使用此处理程序，将优先处理Blueprint页面。
* 此处理函数的服务等级设置得较低(“低于`service.ranking`属性的默认值)，因为假定自定义处理程序需要更高的排名。 但是，排名并不是确保必要时灵活性的绝对最低值。

此冲突处理程序优先于Blueprint。 Live Copy页面`/b`将移动（在Live Copy分支中）到`/b_msm_moved`。

* live copy:`/b`

   将移动（在Live Copy中）到`/b_msm_moved`。 这用作备份，并确保不会丢失任何内容。

   * `lc-level-1` 。

* blueprint:`/b`

   转出到Live Copy页面`/b`。

   * `bp-level-1` 将转出到Live Copy中。

**转出后**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint af rollout</strong></td>
   <td><strong>转出后的Live Copy</strong><br /> </td>
   <td></td>
   <td><strong>转出后的Live Copy</strong><br /> <br /> <br /> </td>
   <td><strong>转出后发布</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （包含已转出的Blueprint页面b的内容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （包含在Live Copy分支中手动创建的页面b的内容）</td>
   <td><code>b</code> <br /> (无变动；包含在Live Copy分支中手动创建的、现在称为b_msm_moved的原始页面b的内容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （无变化）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> （无变化）</td>
  </tr>
 </tbody>
</table>

### 自定义处理程序{#customized-handlers}

自定义的冲突处理程序允许您实施您自己的规则。 使用服务排名机制，您还可以定义它们与其他处理函数的交互方式。

自定义冲突处理程序可以：

* 根据您的要求命名。
* 根据您的要求进行开发/配置；例如，您可以开发一个处理程序，以便优先处理Live Copy页面。
* 可以设计为使用[OSGi配置](/help/sites-deploying/configuring-osgi.md)进行配置；特别是：

   * **服务排名**:

      定义与其他冲突处理函数(`service.ranking`)相关的顺序。

      默认值为 0。

### 冲突处理已停用{#behavior-when-conflict-handling-deactivated}时的行为

如果您手动[取消激活冲突处理](#rollout-manager-and-conflict-handling)，则AEM不会对任何冲突页面执行任何操作（非冲突页面会按预期转出）。

>[!CAUTION]
>
>AEM不会给出任何冲突被忽略的指示，因为必须显式配置此行为，因此假定这是必需的行为。

在这种情况下，Live Copy会高效优先。 未复制Blueprint页面`/b`,Live Copy页面`/b`保持不变。

* blueprint:`/b`

   完全没有复制，但被忽略。

* live copy:`/b`

   保持不变。

<table>
 <caption>
   转出后
 </caption>
 <tbody>
  <tr>
   <td><strong>blueprint af rollout</strong></td>
   <td><strong>转出后的Live Copy</strong><br /> <br /> <br /> </td>
   <td><strong>转出后发布</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (无变动；包含在Live Copy分支中手动创建的页面b的内容)</td>
   <td><code>b</code> <br /> (无变动；包含在Live Copy分支中手动创建的页面b的内容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （无变化）</td>
   <td><code> /lc-level-1</code> <br /> （无变化）</td>
  </tr>
 </tbody>
</table>

### 服务排名{#service-rankings}

[OSGi](https://www.osgi.org/)服务等级可用于定义单个冲突处理程序的优先级。
