---
title: AEM Sites - GDPR就绪
seo-title: AEM Sites - GDPR Readiness
description: 了解在AEM Sites中处理GDPR请求的过程以及如何使用它们。
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 54%

---

# AEM Sites - GDPR就绪{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>以下部分使用GDPR作为示例，但包含的详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等。

欧盟有关数据隐私权的《通用数据保护条例》自2018年5月起生效。

AEM Sites随时准备帮助客户履行其GDPR合规义务。 本页将指导客户完成在AEM Sites中处理GDPR请求的过程。 它描述了私有数据的存储位置，以及如何手动或使用代码删除私有数据。

欲知更多信息，请参见 [Adobe隐私中心的GDPR页面](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>请参阅 [AEM GDPR就绪](/help/managing/data-protection-and-privacy.md) 以了解更多详细信息。

## 作者服务器 {#author-server}

创作服务器上的用户帐户和UGC内容包含在 [平台GDPR文档](/help/managing/data-protection-and-privacy.md).

## 发布服务器 {#publish-server}

用于对网站上的访客进行身份验证的用户帐户以及发布服务器上的UGC内容包含在 [平台GDPR文档](/help/managing/data-protection-and-privacy.md).

默认情况下，AEM Sites 组件不会存储访客在发布服务器上输入的表单数据。建议将数据转发到第三方系统或 Adobe Campaign 以供进一步处理。

## 选择加入/选择退出 {#opt-in-opt-out}

AEM具有 [Cookie选择退出服务](/help/sites-developing/cookie-optout.md) 可用于管理用户的选择启用/选择禁用。

## Analytics的增强见解 {#enhanced-insights-by-analytics}

AEM Sites包括与Analytics的增强型分析的可选集成，该集成使用Adobe Analytics按需服务中的功能。

有关管理与Adobe Analytics相关的GDPR数据主体请求的更多信息，请参阅 [Adobe Analytics和GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html).

## 按目标显示的增强型个性化 {#enhanced-personalization-by-target}

AEM Sites包括与Enhanced Personalization by Target的可选集成，该集成使用Adobe Target按需服务中的功能。

有关管理与Adobe Target相关的GDPR数据主体请求的更多信息，请参阅 [Adobe Target — 隐私和《通用数据保护条例》](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

AEM提供了一个可选的数据层，它具有 [ContextHub](/help/sites-developing/contexthub.md). 这会将特定于访客的数据保留在浏览器中，以用于基于规则的个性化。

默认情况下，此访客数据不会存储在 AEM 中；AEM 将规则发送到数据层，以在浏览器中做出个性化决策。

>[!NOTE]
>
>在Adobe CQ 5.6之前，ClientContext（ContextHub的早期版本）确实将数据发送到服务器，但未存储这些数据。
>
>Adobe CQ 5.5及更早版本现已停用，本文档未涵盖这些版本。

### 实施选择加入/选择退出 {#implementing-opt-in-opt-out}

网站所有者需要根据以下指南实施选择退出组件。

这些指南将选择加入作为默认设置加以实施。因此，必须先获得网站访客的明确同意，然后才能将任何个人数据存储在浏览器（客户端）的持久存储中。

* 每次包含 ContextHub 组件时都应包含选择退出组件。
* 必须向网站访客显示与网站GDPR相关的条款和条件，以便访客：

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

      * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
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

      * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
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

   * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
