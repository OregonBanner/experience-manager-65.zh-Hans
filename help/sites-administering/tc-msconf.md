---
title: 連線到Microsoft&reg； Translator
description: 瞭解如何將AEM連結至Microsoft&reg； Translator。
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 11%

---

# 正在連線到Microsoft® Translator{#connecting-to-microsoft-translator}

建立Microsoft® Translator雲端服務的設定，以使用您的Microsoft® Translation帳戶來翻譯AEM頁面內容、社群內容或資產。

| 属性 | 描述 |
|---|---|
| 翻译标签 | 翻译服务的显示名称。 |
| 翻译属性 | （可选）对于用户生成的内容，为已翻译文本旁边显示的属性，例如 `Translations by Microsoft`。 |
| 工作区 ID | （選用）要使用的自訂Microsoft® Translator引擎ID。 |
| 订阅密钥 | 您的Microsoft® Translator Microsoft®訂閱金鑰。 |

建立設定後，您必須 [啟動它](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

下列程式會使用觸控最佳化UI來建立Microsoft® Translator設定。

1. 在邊欄上，按一下或點選「工具>Cloud Services」。
1. 在Microsoft® Translator區域中，選取「顯示設定」。
1. 按一下「可用設定」旁的+連結。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 为您的配置键入标题。標題會識別Cloud Services控制檯和頁面屬性下拉式清單中的設定。 預設名稱是根據標題。 （可选）键入一个名称以用于存储该配置的存储库节点。使用儲存庫節點路徑的Parent Configuration屬性的預設值。
1. 单击创建。
1. 在出現的對話方塊中，輸入屬性的值，然後按一下「確定」。

## Microsoft® TranslatorCloud Service設定範例 {#sample-microsoft-translator-cloud-service-configurations}

下列Microsoft® Translator雲端服務設定會與Geometrixx範例一起安裝。 某些範例設定使用試用的Microsoft®翻譯帳戶，每月最多允許2,000,000個免費翻譯的字元。

### Microsoft® Translator試用授權 {#microsoft-translator-trial-license}

Microsoft® Translator試用版授權設定是隨Geometrixx Outdoors範例套件一起安裝的範例設定。 此設定使用Microsoft® Translator帳戶，該帳戶具有每月允許2,000,000個已翻譯字元的免費訂閱。

### Microsoft® Translator試用版授權 — 戶外Geometrixx {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft® Translator試用版授權 — Geometrixx-outdoors設定是隨Geometrixx Outdoors安裝的設定範例。 此設定使用與Microsoft® Translator試用授權設定相同的免費Microsoft® Translator帳戶。 此帳戶提供免費訂閱，每月可允許2,000,000個已翻譯字元。

此Microsoft® Translator設定已針對與Geometrixx Outdoors範例網站的內容型別搭配使用進行最佳化。

### 升級Microsoft® Translator試用授權設定 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft®翻譯設定頁面提供指向Microsoft®網站的便利連結，以取得足以用於生產系統的帳戶訂閱。

1. 在邊欄上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在Microsoft® Translator區域中，按一下或點選「 Show Configurations 」，然後按一下或點選「 Microsoft® Translator Trial License (Microsoft® Translation Configuration) 」。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在設定頁面上，按一下升級訂閱。 使用開啟的Microsoft®網頁來設定您的帳戶。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自訂Microsoft® Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft®翻譯設定頁面提供指向Microsoft®網站的便利連結，以便自訂Microsoft® Translator引擎。 ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. 在邊欄上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在Microsoft® Translator區域中，按一下或點選「 Show Configurations 」，然後按一下或點選您要自訂的設定。
1. 在設定頁面上，按一下「自訂轉換器」。 使用開啟的Microsoft®網頁來自訂您的服務。

## 激活 Translator 服务配置 {#activating-the-translator-service-configurations}

若要支援復寫至發佈執行個體的翻譯內容，請啟用雲端服務設定。 若要啟用儲存Microsoft® Translator或協力廠商雲端服務設定的存放庫節點，請使用以下方法 [啟動完整截面（樹狀結構）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). 这些节点位于以下父节点的下方：

* Microsoft®翻譯服務：/libs/settings/cloudconfigs/translation/msft-translation
* 協力廠商翻譯： /etc/cloudservices/machine-translation
