---
title: 透過電子郵件傳送表單提交通知
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms可讓您設定電子郵件提交動作，在提交表單時傳送確認給使用者。
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 透過電子郵件傳送表單提交通知 {#sending-a-form-submission-acknowledgement-via-email}

## 最適化表單資料提交 {#adaptive-form-data-submission}

調適型表單提供數種現成可用的表單 [提交動作](../../forms/using/configuring-submit-actions.md) 將表單資料提交至不同端點的工作流程。

例如， **[!UICONTROL 傳送電子郵件]** 提交動作會在成功提交最適化表單時傳送電子郵件。 您也可以將其設定為傳送電子郵件中的表單資料和PDF。

本文詳細說明在最適化表單及其提供的不同設定上啟用電子郵件動作的步驟。

>[!NOTE]
>
>您也可以使用 **[!UICONTROL 透過電子郵件傳送PDF]** 選項可透過電子郵件將完成的表單作為PDF附件傳送。 此動作可用的設定選項與以下動作可用的選項相同： **[!UICONTROL 傳送電子郵件]** 動作。 電子郵件PDF動作僅適用於XFA型最適化表單

## 傳送電子郵件動作 {#email-action}

「傳送電子郵件」動作可讓作者在成功提交最適化表單時，自動傳送電子郵件給一或多個收件者。

>[!NOTE]
>
>若要使用「傳送電子郵件」動作，您必須依照中的說明設定AEM郵件服務 [設定郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service).

### 在最適化表單上啟用傳送電子郵件動作 {#enabling-email-action-on-an-adaptive-form}

1. 在中開啟最適化表單 **[!UICONTROL 編輯]** 模式。

1. 在 **[!UICONTROL 內容]** 標籤，點選 **[!UICONTROL 表單容器]** 並點選 ![設定](assets/configure-icon.svg) 以檢視最適化表單屬性。

1. 在 **[!UICONTROL 提交]** 區段，選取 **[!UICONTROL 傳送電子郵件]** 從 **[!UICONTROL 提交動作]** 下拉式清單。

   ![提交動作](assets/submission-actions.png)

1. 在中指定有效的電子郵件ID **[!UICONTROL 至]**， **[!UICONTROL CC]**、和 **[!UICONTROL 密件副本]** 欄位。

   在中指定電子郵件的主旨與內文 **[!UICONTROL 主旨]** 和 **[!UICONTROL 電子郵件範本]** 欄位。

   您也可以在欄位中指定變數預留位置，在這種情況下，當一般使用者成功提交表單時會處理欄位的值。 如需詳細資訊，請參閱 [使用最適化表單欄位名稱來動態建立電子郵件內容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   選取 **[!UICONTROL 包含附件]** 如果表單包含檔案附件，而您想要將這些檔案附加至電子郵件中。

   >[!NOTE]
   >
   >如果您選擇 **[!UICONTROL 透過電子郵件傳送PDF]** 選項，您必須選取「包含附件」選項。

1. 按一下 ![儲存](assets/save_icon.svg) 以儲存變更。

### 使用最適化表單欄位名稱來動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

調適型表單中的欄位名稱稱為預留位置，可在使用者提交表單後，以該欄位的值取代。

在 **[!UICONTROL 傳送電子郵件]** 動作，則可以使用執行動作時所處理的預留位置。 這表示電子郵件的標題(例如 **[!UICONTROL 至]**， **[!UICONTROL CC]**， **[!UICONTROL 密件副本]**， **[!UICONTROL 主旨]**)會在使用者提交表單時產生。

若要定義預留位置，請指定 `${<field name>}` 在欄位中選取 **[!UICONTROL 傳送電子郵件]** 作為提交動作。

例如，如果表單包含 **[!UICONTROL 電子郵件地址]** 欄位，已命名 `email_addr`，若要擷取使用者的電子郵件ID，您可以在 **[!UICONTROL 至]**， **[!UICONTROL CC]**，或 **[!UICONTROL 密件副本]** 欄位。

`${email_addr}`

當使用者提交表單時，會傳送電子郵件至在中輸入的電子郵件ID `email_addr` 表單的欄位。

>[!NOTE]
>
>您可以在以下位置找到欄位名稱： **[!UICONTROL 編輯]** 欄位的對話方塊。

變數預留位置也可用在 **[!UICONTROL 主旨]** 和 **[!UICONTROL 電子郵件範本]** 欄位。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位無法當作變數預留位置使用。
