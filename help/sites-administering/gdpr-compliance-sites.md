---
title: AEM Sites - GDPR整備
seo-title: AEM Sites - GDPR Readiness
description: 瞭解AEM Sites之GDPR整備的詳細資訊。
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 54%

---

# AEM Sites - GDPR整備{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>以下各節以GDPR為例，但說明的詳細資料適用於所有資料保護和隱私權法規，例如GDPR、CCPA等。

歐盟資料隱私權的一般資料保護規範於2018年5月起生效。

AEM Sites已準備好協助客戶履行GDPR法規遵循義務。 本頁面將引導客戶完成在AEM Sites中處理GDPR請求的程式。 它描述了私有数据的存储位置，以及如何手动或使用代码删除私有数据。

如需進一步資訊，請參閱 [Adobe隱私權中心的GDPR頁面](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>另請參閱 [AEM GDPR整備](/help/managing/data-protection-and-privacy.md) 以取得更多詳細資料。

## 作者伺服器 {#author-server}

作者伺服器上的使用者帳戶和UGC內容包含在 [平台GDPR檔案](/help/managing/data-protection-and-privacy.md).

## 發佈伺服器 {#publish-server}

用於驗證網站訪客身分的使用者帳戶以及發佈伺服器上的UGC內容都包含在 [平台GDPR檔案](/help/managing/data-protection-and-privacy.md).

默认情况下，AEM Sites 组件不会存储访客在发布服务器上输入的表单数据。建议将数据转发到第三方系统或 Adobe Campaign 以供进一步处理。

## 选择加入/选择退出 {#opt-in-opt-out}

AEM具有 [Cookie選擇退出服務](/help/sites-developing/cookie-optout.md) 可用於管理使用者的選擇加入/選擇退出。

## Analytics的增強型分析 {#enhanced-insights-by-analytics}

AEM Sites包括與Enhanced Insights by Analytics的選擇性整合，後者使用Adobe Analytics On-demand Service中的功能。

有關管理與Adobe Analytics相關的GDPR資料主體請求的進一步資訊，請參閱 [Adobe Analytics和GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html).

## Target增強的個人化 {#enhanced-personalization-by-target}

AEM Sites包括與Enhanced Personalization by Target的選擇性整合，後者使用Adobe Target On-demand Service中的功能。

有關管理與Adobe Target相關的GDPR資料主體請求的進一步資訊，請參閱 [Adobe Target — 隱私權與一般資料保護規範](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

AEM提供選購的資料層，搭配 [ContextHub](/help/sites-developing/contexthub.md). 这会将特定于访客的数据保留在浏览器中，以用于基于规则的个性化。

默认情况下，此访客数据不会存储在 AEM 中；AEM 将规则发送到数据层，以在浏览器中做出个性化决策。

>[!NOTE]
>
>在Adobe CQ 5.6之前，ClientContext（舊版ContextHub）確實將資料傳送至伺服器，但並未儲存資料。
>
>Adobe CQ 5.5及舊版現已終止服務，本檔案未涵蓋該服務。

### 实施选择加入/选择退出 {#implementing-opt-in-opt-out}

网站所有者需要根据以下指南实施选择退出组件。

这些指南将选择加入作为默认设置加以实施。因此，網站訪客必須先明確同意，才會將任何個人資料儲存在瀏覽器（使用者端）的持續性中。

* 每次包含 ContextHub 组件时都应包含选择退出组件。
* 與網站的GDPR相關的條款與條件必須顯示給網站訪客，允許他們：

   * 接受
   * 拒绝
   * 更改其上一个选择

* 如果网站访客接受网站的条款和条件，则应删除 ContextHub 选择退出 Cookie：

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果网站访客不接受网站的条款和条件，则应设置 ContextHub 选择退出 Cookie：

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要检查 ContextHub 是否正在选择退出模式下运行，应在浏览器的控制台中进行以下调用：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 预览 ContextHub 的持久存储 {#previewing-persistence-of-contexthub}

要预览使用 ContextHub 的持久存储，用户可以：

* 例如，使用浏览器的控制台：

   * Chrome：

      * 打开“开发人员工具”>“应用程序”>“存储”：

         * “本地存储”>“（网站）”>“ContextHubPersistence”
         * “会话存储”>“（网站）”>“ContextHubPersistence”
         * “Cookie”>“（网站）”>“SessionPersistence”
   * Firefox：

      * 打开“开发人员工具”>“存储”：

         * “本地存储”>“（网站）”>“ContextHubPersistence”
         * “会话存储”>“（网站）”>“ContextHubPersistence”
         * “Cookie”>“（网站）”>“SessionPersistence”
   * Safari：

      * 在菜单栏中打开“偏好设置”>“高级”>“显示开发”菜单
      * 打开“开发”>“显示 JavaScript 控制台”

         * “控制台”>“存储”>“本地存储”>“（网站）”>“ContextHubPersistence”
         * “控制台”>“存储”>“会话存储”>“（网站）”>“ContextHubPersistence”
         * “控制台”>“存储”>“Cookie”>“（网站）”>“ContextHubPersistence”
   * Internet Explorer：

      * 打开“开发人员工具”>“控制台”

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* 在浏览器的控制台中使用 ContextHub API：

   * ContextHub 提供以下数据持久层：

      * ContextHub.Utils.Persistence.Modes.LOCAL （預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub 存储定义将使用哪个持久层，因此，要查看持久存储的当前状态，应检查所有层。


例如，要查看存储在 localStorage 中的数据，请执行以下操作：

要预览使用 ContextHub 的持久存储，用户可以：

* 使用浏览器的控制台：

   * Chrome - 打开“开发人员工具”>“应用程序”>“存储”：

      * “本地存储”>“（网站）”>“ContextHubPersistence”
      * “会话存储”>“（网站）”>“ContextHubPersistence”
      * “Cookie”>“（网站）”>“SessionPersistence”
   * Firefox - 打开“开发人员工具”>“存储”：

      * “本地存储”>“（网站）”>“ContextHubPersistence”
      * “会话存储”>“（网站）”>“ContextHubPersistence”
      * “Cookie”>“（网站）”>“SessionPersistence”


* 在浏览器的控制台中使用 ContextHub API：

   * ContextHub 提供以下数据持久层：

      * ContextHub.Utils.Persistence.Modes.LOCAL （預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub 存储定义将使用哪个持久层，因此，要查看持久存储的当前状态，应检查所有层。


例如，要查看存储在 localStorage 中的数据，请执行以下操作：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除 ContextHub 的持久存储 {#clearing-persistence-of-contexthub}

要清除 ContextHub 持久存储，请执行以下操作：

* 要清除当前加载的持久存储，请执行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 要清除特定的持久层（例如 sessionStorage），请执行以下操作：

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有 ContextHub 持久层，必须为所有层调用适当的代码：

   * ContextHub.Utils.Persistence.Modes.LOCAL （預設）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
