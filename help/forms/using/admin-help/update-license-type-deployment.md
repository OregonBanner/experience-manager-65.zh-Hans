---
title: 更新部署的授權型別
seo-title: Update the license type for the deployment
description: 使用管理主控台中的「變更授權」頁面，更新部署的授權型別。
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 更新部署的授權型別 {#update-the-license-type-for-the-deployment}

在AEM表單安裝程式中，您使用Configuration Manager來設定和部署所需的AEM表單模組。 依預設，這些模組會設定60天的評估授權。 使用Administration Console中的「變更授權」頁面來變更部署的授權型別。 目前部署的模組會顯示在「變更授權」頁面上。

「變更許可證」頁面會顯示有關您的許可證的資訊：

* 目前的授權型別
* 上次更新授權的日期和時間
* 上次執行更新的人員
* 授權的目前狀態
* 安裝AEM表單的日期
* 目前授權到期的日期

>[!NOTE]
>
>授權變更適用於所有已部署的模組。 在變更授權型別之前，請取消部署任何未授權的模組。 如果部署的模組清單包含的模組不是您從Adobe購買的模組，請勿選擇生產授權型別。

## 更新授權型別 {#update-the-license-type}

1. 在管理控制檯中，按一下「授權」。
1. 閱讀AEM Forms一般使用者授權合約，如果您同意合約條款，請選取「我接受」，然後按一下「下一步」。
1. 在「變更授權」頁面上，選取授權型別：

   * **估計：** 60天評估授權
   * **開發：** 永久開發授權
   * **NFR：** 2年評估授權
   * **影片：** 訂閱Adobe Developer計畫1年
   * **生產：** 永久授權

1. 選取「是，授權變更對所有已部署的模組有效」。
1. 按一下「確認授權變更」。 系統會顯示訊息，指出授權已成功更新。
