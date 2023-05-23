---
title: 存储配置
seo-title: Storage Configuration
description: 如何存取儲存設定主控台
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 3%

---

# 存储配置 {#storage-configuration}

儲存設定是識別為社群內容（也稱為使用者產生的內容，UGC）選擇的儲存空間的手段。

此設定會通知AEM Communities程式碼，存取UGC時將使用儲存資源提供者(SRP)的實作，且必須反映部署AEM時建立的拓撲。

如需儲存選項和部署拓撲的討論，請造訪：

* [社群內容存放區](working-with-srp.md)
* [建議的拓撲](topologies.md)

## 儲存設定主控台 {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

在製作環境中，存取儲存設定主控台。

* 在全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 儲存設定]**

若要選取預設JCR以外的儲存選項：

* 选择选项
* 正確設定

   * 檢視詳細資訊 [選取MSRP](msrp.md#select-msrp)
   * 檢視詳細資訊 [選取DSRP](dsrp.md#select-dsrp)
   * 檢視詳細資訊 [選取ASRP](asrp.md#select-asrp)

* 選取 **[!UICONTROL 提交]**.

### 關於JCR儲存 {#about-jcr-storage}

請注意，如果未進行選取，預設為AEM存放庫JCR。

JCR是 *not* 作者和發佈環境共用的公用存放區。 社群內容只會從建立它的作者或發佈環境中可見。

造訪 [JCR存放區](jsrp.md) 以取得其他資訊。

>[!NOTE]
>
>節點不存在 `srpc` 在 `/etc/socialconfig` 表示預設值 [JCR存放區](jsrp.md).
