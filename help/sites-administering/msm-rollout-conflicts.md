---
title: MSM 转出冲突
seo-title: MSM Rollout Conflicts
description: 瞭解如何處理「多網站管理員」轉出衝突。
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

如果在Blueprint分支和相依的即時副本分支中同時建立具有相同頁面名稱的新頁面，則可能會發生衝突。

转出时需要处理和解决此类冲突。

## 冲突处理 {#conflict-handling}

當Blueprint和即時副本分支中確實存在衝突頁面時，MSM可讓您定義應如何（甚至是否）處理這些頁面。

为了确保转出不被阻止，可能的定义可以包括：

* 轉出期間哪個頁面（Blueprint或即時副本）優先，
* 將重新命名哪些頁面（以及重新命名方式），
* 這會如何影響任何已發佈的內容。

   AEM的預設行為（現成可用）是發佈的內容將不會受到影響。 因此，如果在即時副本分支中手動建立的頁面已發佈，在衝突處理和轉出後，該內容仍會發佈。

除了标准功能外，还可以添加自定义的冲突处理程序来实施其他规则。它们还允许将操作发布为单独的过程。

### 示例场景 {#example-scenario}

在以下各節中，我們使用新頁面的範例 `b`，建立於Blueprint和即時副本分支（手動建立）中，以說明解決衝突的各種方法：

* Blueprint：`/b`

   主版頁面；具有1個子頁面，bp-level-1。

* 即時副本： `/b`

   在即時副本分支中手動建立的頁面；具有1個子頁面、 `lc-level-1`.

   * 在发布为 `/b` 时与子页面一起激活.

**转出前**

<table>
 <tbody>
  <tr>
   <td><strong>轉出前的Blueprint</strong></td>
   <td><strong>轉出前的即時副本</strong></td>
   <td><strong>轉出前發佈</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> （在Blueprint分支中建立，可準備轉出）<br /> </td>
   <td><code>b</code> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code>b</code> <br /> （包含在即時副本分支中手動建立的頁面b內容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code> /lc-level-1</code> <br /> （包含頁面內容）<br /> child-level-1 （已在即時副本分支中手動建立）</td>
  </tr>
 </tbody>
</table>

## 转出管理器和冲突处理 {#rollout-manager-and-conflict-handling}

转出管理器允许您激活或停用冲突管理。

這是使用來完成的 [OSGi設定](/help/sites-deploying/configuring-osgi.md) 之 **Day CQ WCM轉出管理員**：

* **處理與手動建立的頁面衝突**：

   ( `rolloutmgr.conflicthandling.enabled`)

   如果轉出管理員應處理在即時副本中建立的頁面與Blueprint中存在的名稱之間的衝突，則設為true。

AEM具有 [停用衝突管理時的預先定義行為](#behavior-when-conflict-handling-deactivated).

## 冲突处理程序 {#conflict-handlers}

AEM使用衝突處理常式，來解決將內容從Blueprint轉出至即時副本時存在的任何頁面衝突。 重新命名頁面是解決這類衝突的一種（一般）方法。 可以运行多个冲突处理程序以允许选择不同的行为。

AEM 提供：

* [默认冲突处理程序](#default-conflict-handler)：

   * `ResourceNameRolloutConflictHandler`

* 实施[自定义处理程序](#customized-handlers)的可能性。
* 服务排名机制，可让您设置每个单独处理程序的优先级. 使用排名最高的服务。

### 默认冲突处理程序 {#default-conflict-handler}

默认冲突处理程序：

* 已呼叫 `ResourceNameRolloutConflictHandler`

* 对于此处理程序，Blueprint 页面将获得优先权。
* 此處理常式的服務排名設定為低(「即低於 `service.ranking` 屬性)，因為假設自訂處理常式需要較高的排名。 然而，排名并不是在必要时确保灵活性的绝对最低标准。

此处理程序为 Blueprint 页面提供优先权。即時副本頁面 `/b` （在即時副本分支中）移至 `/b_msm_moved`.

* 即時副本： `/b`

   移動（在即時副本中）至 `/b_msm_moved`. 这将充当备份，并确保不丢失任何内容。

   * 不会移动 `lc-level-1`。

* Blueprint：`/b`

   轉出至即時副本頁面 `/b`.

   * `bp-level-1` 轉出到livecopy。

**转出后**

<table>
 <tbody>
  <tr>
   <td><strong>轉出後的Blueprint</strong></td>
   <td><strong>轉出後的即時副本</strong><br /> </td>
   <td></td>
   <td><strong>轉出後的即時副本</strong><br /> <br /> <br /> </td>
   <td><strong>轉出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （具有已轉出的blueprint頁面b的內容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （具有在即時副本分支中手動建立的頁面b的內容）</td>
   <td><code>b</code> <br /> （無變更；包含在即時副本分支中手動建立的原始頁面b的內容，現在稱為b_msm_moved）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
  </tr>
 </tbody>
</table>

### 自定义处理程序 {#customized-handlers}

自定义冲突处理程序允许您实施自己的规则。利用服务排名机制，您还可以定义它们如何与其他处理程序交互。

自定义冲突处理程序可以：

* 根据您的要求进行命名。
* 根據您的需求開發/設定；例如，您可以開發處理常式，好讓即時副本頁面獲得優先權。
* 可設計為透過以下方式設定： [OSGi設定](/help/sites-deploying/configuring-osgi.md)；尤其是：

   * **服務排名**：

      定義與其他衝突處理常式相關的順序( `service.ranking`)。

      默认值为 0。

### 衝突處理停用時的行為 {#behavior-when-conflict-handling-deactivated}

如果您手動 [停用衝突處理](#rollout-manager-and-conflict-handling) AEM就不會對任何衝突頁面採取任何動作（非衝突頁面會如預期般轉出）。

>[!CAUTION]
>
>AEM不會指出系統忽略衝突，因為此行為必須明確設定，因此我們假設這是必要的行為。

在這種情況下，即時副本會有效取得優先權。 Blueprint頁面 `/b` 不會複製且即時副本頁面 `/b` 保持不變。

* Blueprint：`/b`

   根本不复制，而是忽略。

* 即時副本： `/b`

   保持不变。

<table>
 <caption>
   转出后
 </caption>
 <tbody>
  <tr>
   <td><strong>轉出後的Blueprint</strong></td>
   <td><strong>轉出後的即時副本</strong><br /> <br /> <br /> </td>
   <td><strong>轉出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （無變更；具有在即時副本分支中手動建立的頁面b內容）</td>
   <td><code>b</code> <br /> （無變更；包含在live copy分支中手動建立的頁面b內容）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
  </tr>
 </tbody>
</table>

### 服务排名 {#service-rankings}

[OSGi](https://www.osgi.org/) 服务排名可用于定义各个冲突处理程序的优先级。
