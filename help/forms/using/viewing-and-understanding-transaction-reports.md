---
title: 檢視與瞭解交易報表
seo-title: Viewing and Understanding Transaction Reports
description: 使用交易報告，針對產品使用情況以及重新平衡軟硬體投資做出明智的決策。
seo-description: Use transaction reports to make an informed decision about the product usage and rebalancing investments in hardware and software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 75e1697c301dca3a649833a45caa1753fdc81514
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---

# 檢視與瞭解交易報表{#viewing-and-understanding-transaction-reports}

交易報表可讓您擷取及追蹤已提交的表單、已處理檔案及已轉譯檔案數目。 追蹤這些交易的目的在於，針對產品使用狀況做出明智的決策，並重新平衡軟硬體投資。 如需詳細資訊，請參閱 [AEM Forms交易報表概觀](../../forms/using/transaction-reports-overview.md).

## 設定交易報告  {#setting-up-transaction-reports}

交易報告功能屬於AEM Forms附加元件套件的一部分。 如需有關在所有作者和發佈執行個體上安裝附加元件套件的資訊，請參閱 [安裝和設定AEM表單](/help/forms/using/installing-configuring-aem-forms-osgi.md). 安裝AEM Forms附加元件套件後，請執行下列動作：

* 在所有發佈執行個體上啟用反向復寫
* 啟用交易報告
* 提供檢視交易報告的許可權
* （選擇性）設定異動排清期間與寄件匣 [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms交易報表不支援僅包含發佈例項的拓撲。
>* 在使用交易報告之前，請確定已針對所有發佈執行個體啟用反向復寫。
>* 交易資料會從發佈執行個體反向復寫至僅對應的製作或處理執行個體。 作者或處理執行個體無法進一步將資料復寫至其他執行個體。
>


### 在所有發佈執行個體上啟用反向復寫 {#enable-reverse-replication-on-all-the-publish-instances}

交易報表會使用反向復寫來合併從發佈執行個體到編寫執行個體的交易計數。 在所有發佈執行個體上設定反向復寫。 如需設定反向復寫的詳細指示，請參閱 [復寫](/help/sites-deploying/replication.md).

### 啟用交易報告 {#enable-transaction-reports}

交易報告預設為停用。 您可以從AEM Web主控台啟用報表。 若要在AEM Forms環境中啟用交易報表，請在所有製作和發佈執行個體上執行下列步驟：

1. 以管理員身分登入AEM執行個體。 前往 **工具** > **作業** > **網頁主控台**.
1. 找到並開啟 **Forms交易報告** 服務。
1. 選取「記錄異動」核取方塊。 单击“**保存**”。

   在所有製作和發佈執行個體上重複步驟1至3。

### 提供檢視交易報告的許可權 {#provide-rights-to-view-a-transaction-report}

只有fd-administrator群組的成員可以檢視交易報告。 若要允許使用者檢視交易報告，請讓使用者成為fd-administrator群組的成員。 如需讓使用者成為AEM群組成員的指示，請參閱 [使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md).

### （選擇性）設定異動排清期間與寄件匣 {#optional-configure-transaction-flush-period-and-outboxes}

交易會先在記憶體中快取，再儲存在存放庫中。 會遵循此程式，以確保不會頻繁寫入存放庫。 根據預設，快取期間（「交易排清期間」）設為60秒。 您可以變更預設期間以符合您的環境。 執行以下步驟來變更預設快取期間：

1. 以管理員身分登入作者執行個體。 前往 **工具** > **作業** > **網頁主控台**.
1. 找到並開啟 **Forms交易存放庫儲存提供者** 服務。
1. 指定中的秒數 **異動排清期間** 欄位。 单击“**保存**”。

反向復寫會將交易資料複製到製作執行個體的預設寄件匣。 您可以將交易資料放入自訂寄件匣。 執行以下步驟來指定自訂寄件匣：

1. 以管理員身分登入作者執行個體。 前往 **工具** > **作業** > **網頁主控台**.
1. 找到並開啟 **Forms交易存放庫儲存提供者** 服務。
1. 指定自訂寄件匣的名稱 **寄件匣** 欄位。 单击“**保存**”。會在所有編寫執行個體上建立具有指定名稱的寄件匣。

## 檢視交易報告 {#viewing-the-transaction-report}

您可以檢視有關作者或發佈執行個體的交易報告。 製作執行個體上的交易報告提供在設定的製作和發佈執行個體上發生的所有交易的彙總總和。 發佈執行個體上的交易報告會提供只發生在基礎發佈執行個體上的交易計數。 執行以下步驟來檢視報表：

1. 登入AEM Forms伺服器，網址為 `https://[hostname]:'port'`.
1. 導覽至 **工具** > **Forms**>**檢視交易報告**.

## 瞭解報告 {#understanding-the-report}

AEM Forms會顯示自設定日期以來的交易報表，如下列摘要報表所示：

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 使用 **將日期重設為今天** 重設交易記錄的選項。 當您將日期重設為今天時，所有先前的交易記錄都會遺失。 當您在作者執行個體上重設日期時，此變更不會影響「發佈」執行個體上的交易報告，反之亦然。
* 使用 **僅顯示發佈執行個體的交易** 以檢視只在已設定的發佈執行個體或發佈伺服器陣列上發生的所有交易。
* 使用類別： **已處理的檔案**， **已呈現的檔案**、和 **Forms已提交** 以檢視對應的交易。 如需這些分類中入帳的交易型態，請參閱 [可記帳交易報表API](../../forms/using/transaction-reports-billable-apis.md).

## 檢視交易報告記錄 {#view-transaction-reporting-logs}

交易報告會將所有顯示在報告中的資訊和一些其他資訊放入日誌中。 記錄檔中提供的資訊對進階使用者很有幫助。 例如，記錄會將交易分割成多個精細類別，而報告中會顯示三個整合的類別。 記錄檔位於 `error.log` 檔案位於 `/crx-repository/logs/` 目錄。 即使您未從AEM Web主控台啟用交易報告，仍可使用記錄檔。

## 相关文章 {#related-articles}

* [交易報表概觀](../../forms/using/transaction-reports-overview.md)
* [交易報表可記帳API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自訂實作的交易](/help/forms/using/record-transaction-custom-implementation.md)
