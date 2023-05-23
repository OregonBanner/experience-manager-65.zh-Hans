---
title: 瞭解資料夾結構
seo-title: Understanding the folder structure
description: 如何瞭解AEM Forms工作區原始碼的資料夾結構以自訂。
seo-description: How to understand the folder structure of AEM Forms workspace source code to customize.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 瞭解資料夾結構 {#understanding-the-folder-structure}

AEM Forms工作區元件是以MVC架構設計，使用骨幹。 每個元件都有一個檔案，用於：

* 模型，包含商業邏輯。
* 範本，即包含介面控制項的HTML檔案。
* 檢視，充當範本的Controller類別。

所有元件的資產都會放置在如下所述的資料夾結構中。 若要存取資產，請登入CRXDE Lite並瀏覽至 `/libs/ws/js/runtime/`.

**模型** 包含骨幹模型。

**檢視** 包含主幹檢視。

**範本** 僅包含元件的HTML範本。

**路由** 包含通用路由。 路由內的Templates資料夾包含HTML程式碼和元件的參照。

**服務** 包含在REST端點上呼叫Adobe Experience Manager伺服器API的服務介面。

**使用率** 包含可供多個元件使用的一般公用程式。
