---
title: 使用連結
seo-title: Using Liking
description: 新增和設定連結元件
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---

# 使用連結 {#using-liking}

此 `Liking` 元件是實用工具，可讓使用者對特定內容發表意見，例如論壇中的評論。 使用 `Liking` 元件時，成員會選取心形圖示來表示正面意見。

## 新增連結至頁面 {#adding-liking-to-a-page}

若要新增 `Liking` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Liking`

並將其拖曳至頁面上某個位置，例如使用者喜歡的相對於該功能的位置。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-liking.md#essentials-for-client-side) 包含，這就是 `Liking` 元件隨即出現。

![liking-component](assets/liking-component.png)

## 設定連結 {#configuring-liking}

選取已放置的 `Liking` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文字和標籤]** 索引標籤中，指定用來記錄「讚」的屬性。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 正面响应标签]**

   (*必填*)正面回應的屬性名稱。

* **[!UICONTROL 负面响应标签]**

   (*必填*)負面回應的屬性名稱。

* **[!UICONTROL 标签名称]**

   (*必填*)此投票元件例項的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成员 {#members}

成員可隨時變更其喜好。

### 匿名 {#anonymous}

不支援匿名連結。 網站訪客必須註冊（成為會員）並登入才能參與點讚。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [按一下Essentials](essentials-liking.md) 適用於開發人員的頁面。
