---
title: 單一登入和逾時處理常式
seo-title: Single Sign On and timeout handlers
description: 如何設定AEM Forms工作區的工作階段逾時值。
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 單一登入和逾時處理常式 {#single-sign-on-and-timeout-handlers}

AEM Forms工作區已啟用SSO。 如果使用者已登入AEM Forms應用程式(如Forms管理員或PDF產生器使用者介面)並在相同的瀏覽器工作階段中存取AEM Forms工作區，則使用者會登入AEM Forms工作區，反之亦然。

## 在AEM Forms工作區中處理伺服器逾時 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

您可以在管理控制檯中設定使用者的工作階段逾時。

若要設定逾時，請登入 `https://'[server]:[port]'/adminui`，導覽至 **設定>使用者管理>設定>設定進階系統屬性**，並進行所需的設定。

在AEM Forms中，工作區逾時的處理方式為：

* 使用者的工作階段期間可用於回應 `initialize` 會初始化使用者工作階段的呼叫。
* 快顯對話方塊會通知使用者工作階段即將到期，在工作階段到期前15秒。

在此快顯對話方塊上：

* 按一下「確定」結束使用者作業階段。
* 按一下[取消]重新初始化使用者工作階段。

>[!NOTE]
>
>如果未採取任何動作，系統會在工作階段到期前三秒自動將使用者登出AEM Forms工作區。
