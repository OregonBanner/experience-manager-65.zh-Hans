---
title: 使用AEM翻譯工作流程將最適化表單和記錄檔案本地化
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: 瞭解如何使用AEM翻譯工作流程將最適化表單和記錄檔案本地化。
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 15%

---

# 使用AEM翻譯工作流程將最適化表單和記錄檔案本地化 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可協助您跨地理區域提供更廣泛的受眾。 Adobe Experience Manager翻譯工作流程可協助您將最適化表單及其記錄檔案本地化。 您可以使用 **機器翻譯** 或 **人工翻譯** 將最適化表單本地化。

本文說明搭配最適化表單和記錄檔案使用AEM翻譯工作流程的流程。

## 使用機器翻譯將最適化表單和記錄檔案當地語系化 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以最適化表單和記錄檔案翻譯您的內容。 AEM Forms已預先設定為使用Microsoft Translator的試用版進行機器翻譯。 執行以下步驟，為您的最適化表單和記錄檔案啟用機器翻譯：

1. 在AEM Forms UI上，選取表單，然後點選 **新增字典** 選項。
1. 在 **新增字典至翻譯專案** 熒幕中，選取 **建立新的翻譯專案** 或 **新增至現有翻譯專案** 選項。
1. 在 **專案標題** 欄位中，指定標題。 例如，`Government Reference Site - German locale.`
1. 在 **目標語言** 欄位，指定地區設定(例如， `German(de)`)，然後按一下 **完成**. 您可以指定多個地區設定。 表單已轉譯為 **目標語言** 欄位。
1. 在「新增的字典」對話方塊中，按一下 **開啟專案**. 在「專案」畫面中，開啟新建立的專案。
1. 按一下 **橢圓** 在底部 **翻譯摘要** 圖磚。 「翻譯摘要」畫面隨即開啟。
1. 按一下 **編輯** 圖示於 **翻譯摘要** 畫面。 開啟 **翻譯** 標籤並選取中的機器翻譯 **翻譯方法** 畫面。 選取適當的 **翻譯提供者** 和 **雲端設定**. 按一下 **完成** 圖示加以檢視。
1. 於 **翻譯工作** 圖磚，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 圖示，然後按一下 **開始**. 圖磚的狀態會變更為「草稿」。 翻譯完成後，狀態會變更為 **準備好審查**. 幾分鐘後重新整理頁面並驗證狀態。
1. 在狀態變更為 **準備好審查** 於 **翻譯工作** 圖磚，在瀏覽器視窗中開啟表單。 此時會顯示表單的當地語系化版本。

   >[!NOTE]
   >
   >* 在瀏覽器視窗中開啟表單的當地語系化版本之前，請確定瀏覽器的地區設定已設定為符合表單的地區設定。 例如，如果表單已翻譯成德文(de)語言，則將瀏覽器的地區設定設為德文(de)。
   >* 最適化表單元件不支援由右至左(RTL)語言。 例如，希伯來文。


   除了最適化表單外，自動產生的記錄檔案也會本地化。

   如需記錄檔案設定和組態的詳細資訊，請參閱：

[记录文档模板配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[記錄檔案設定](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自訂記錄檔案的品牌資訊](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 並確保瀏覽器地區設定與您使用機器語言將最適化表單本地化的語言設定相同。 瀏覽器地區設定有助於記錄檔案中的品牌資訊本地化。
1. 若要檢視本地化記錄檔案，請點選「產生預覽」。 記錄檔案PDF會產生，並在瀏覽器的新索引標籤中開啟。

## 使用人工翻譯將最適化表單及其記錄檔案本地化 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人工翻譯中，內容會傳送給翻譯提供者，並由專業翻譯人員進行翻譯。 完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与 AEM 集成时，内容会在 AEM 和翻译提供商之间自动发送。

對於翻譯，包含XLIFF格式檔案的字典會與專業譯者共用。 字典中包含每個地區設定的個別XLIFF檔案。 每個XLIFF檔案都包含文字，這些文字會針對對應的本地化文字顯示給一般使用者及預留位置。

執行以下步驟，使用人工翻譯將表單及其記錄檔案本地化：

1. [将 AEM 连接到翻译服务提供商](/help/sites-administering/tc-tic.md)和[创建翻译集成框架配置](/help/sites-administering/tc-tic.md)。

1. [将语言母版页面关联到](/help/sites-administering/tc-tic.md)翻译服务和框架配置。

1. [标识要翻译的内容类型](/help/sites-administering/tc-rules.md)。

1. 通过创作语言母版并创建语言副本的根页面来[准备内容以进行翻译](/help/sites-administering/tc-prep.md)。

1. [创建翻译项目](/help/sites-administering/tc-manage.md)以收集要翻译的内容并准备翻译过程。

1. 使用翻译项目[管理内容翻译过程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 最適化表單元件不支援由右至左(RTL)語言。 例如，希伯來文。
>

