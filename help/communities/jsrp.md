---
title: JSRP - JCR儲存資源提供者
seo-title: JSRP - JCR Storage Resource Provider
description: JSRP通常最適合用於一個發佈執行個體和一個作者執行個體的示範或開發環境
seo-description: JSRP is generally best suited for demonstration or development environments of one publish instance and one author instance
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# JSRP - JCR儲存資源提供者 {#jsrp-jcr-storage-resource-provider}

## 關於JSRP {#about-jsrp}

當AEM Communities使用JSRP作為其儲存選項（預設）時，社群內容儲存在JCR中，使用者產生的內容(UGC)只能從發佈它的作者或發佈執行個體存取。

由於部署簡單，JSRP通常最適合用於一個發佈執行個體和一個作者執行個體的示範或開發環境。

另請參閱 [SRP選項的特性](working-with-srp.md#characteristics-of-srp-options) 和 [建議的拓撲](topologies.md).

## 配置 {#configuration}

### 選取JSRP {#select-jsrp}

依預設，JSRP是UGC的儲存選項。

此 [儲存設定主控台](srp-config.md) 允許選取預設儲存設定，以識別要使用的SRP實作。

在製作環境中，若要存取儲存設定主控台

* 從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 儲存設定]**

* 選取 **[!UICONTROL JCR儲存資源提供者(JSRP)]**

* 選取 **[!UICONTROL 提交]**

![jsrp-configuration](assets/jsrp-configuration.png)

### 發佈設定 {#publishing-the-configuration}

雖然JSRP是預設設定，但要確保在發佈環境中設定了相同的設定：

* 從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**
* 選取 **[!UICONTROL 啟動樹狀結構]** > **[!UICONTROL 開始路徑]**：

   * 瀏覽至 `/conf/global/settings/community/srpc/`

* 選取 **[!UICONTROL 啟動]**

## 管理使用者資料 {#managing-user-data}

有關以下專案的資訊： *使用者*， *使用者設定檔* 和 *使用者群組*，通常輸入發佈環境中，請造訪：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## 疑难解答 {#troubleshooting}

### UGC在JCR中不可見 {#ugc-not-visible-in-jcr}

檢查儲存選項的設定，確認JSRP已設定為預設提供者。 依預設，儲存資源提供者為JSRP。

在所有作者和發佈AEM執行個體上，重新造訪「儲存體設定」主控台或檢查AEM存放庫：

* 在JCR中，如果 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) 節點，這表示儲存提供者為JSRP。
   * 如果srpc節點存在且包含節點 [default設定](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)，defaultconfiguration的屬性應將JSRP定義為預設提供者。

### UGC在作者執行個體上不可見 {#ugc-not-visible-on-author-instance}

這不是錯誤。 JSRP的一個特點是在發佈環境中輸入的社群內容將只會顯示在發佈環境中。

### UGC在發佈執行個體上不可見 {#ugc-not-visible-on-publish-instance}

如果部署了單一發佈執行個體或發佈叢集，請遵循以下指示： [UGC在JCR中不可見](#ugc-not-visible-in-jcr).

如果部署了發佈陣列，JSRP的一個特徵是社群內容將只會顯示在它發佈到的發佈執行個體上。

若要讓任何發佈執行個體都能看到UGC，則需要發佈叢集。
