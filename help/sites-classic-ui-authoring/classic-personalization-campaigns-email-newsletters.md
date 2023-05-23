---
title: 發佈電子郵件給電子郵件服務提供者
seo-title: Publishing an Email to Email Service Providers
description: 您可以將電子報發佈到電子郵件服務，例如ExactTarget和Silverpop Engage。
seo-description: You can publish newsletters to e-mail services such as ExactTarget and Silverpop Engage.
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 3%

---

# 發佈電子郵件給電子郵件服務提供者{#publishing-an-email-to-email-service-providers}

您可以將電子報發佈到電子郵件服務，例如ExactTarget和Silverpop Engage。 本檔案說明如何設定AEM以將Newsletter發佈至這些電子郵件服務。

>[!NOTE]
>
>您必須先設定服務提供者，才能建立及發佈電子郵件。 另請參閱 [設定ExactTarget](/help/sites-administering/exacttarget.md) 和 [設定Silverpop Engage](/help/sites-administering/silverpop.md) 以取得詳細資訊。

若要將電子郵件發佈至電子郵件服務提供者，您必須執行下列步驟：

1. 建立電子郵件。
1. 將電子郵件服務設定套用至電子郵件。
1. 發佈電子郵件。

>[!NOTE]
>
>如果您更新電子郵件提供者、進行快速測試或傳送電子報，如果電子報未先發佈至發佈執行個體，或發佈執行個體無法使用，則這些作業會失敗。 請務必發佈您的Newsletter，並確保Publish執行個體已啟動且執行中。

## 建立電子郵件 {#creating-an-email}

您可以使用在行銷活動下建立您要發佈至電子郵件服務的電子郵件或電子報 **Geometrixx電子報** 範本。 您也可以使用 **Geometrixx Outdoors電子郵件** 範本。 電子郵件/電子報範例根據 **Geometrixx Outdoors電子郵件** 範本位於 `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`.

若要建立發佈至已設定電子郵件服務的新電子郵件：

1. 前往 **網站** 然後 **行銷活動**. 選取行銷活動。
1. 按一下 **新增** 以開啟 **建立頁面** 視窗。
1. 輸入標題、名稱，然後選取 **Geometrixx電子報** 範本清單中的範本。
1. 单击&#x200B;**创建**。
1. 開啟已建立的電子郵件。
1. 切換到設計模式以選取您要顯示在Sidekick中的元件。
1. 切換到編輯模式並開始新增內容(文字、影像、 [電子郵件工具](#adding-exacttarget-email-tools-to-your-email)， [個人化變數](#adding-text-and-personalization-tool-to-your-e-mail)，等等)至您的電子郵件。

### 將ExactTarget電子郵件工具新增至您的電子郵件 {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>本節專屬於ExactTarget服務。

此 **電子郵件工具** ExactTarget的元件可為您的電子郵件/電子報新增更多電子郵件功能。

1. 開啟電子郵件以發佈至ExactTarget。
1. 新增元件 **ET — 電子郵件工具** 使用sidekick移至您的頁面。 在「編輯」模式中開啟元件。

   ![chlimage_1](assets/chlimage_1.gif)

1. 從「 」中選取選項 **選項** 功能表：

<table>
 <tbody>
  <tr>
   <td>邮寄地址(必需)</td>
   <td>此元件會在您的電子郵件中插入貴組織的實體郵寄地址。</td>
  </tr>
  <tr>
   <td>个人资料中心(必需)</td>
   <td>設定檔中心是一個網頁，訂閱者可以在這裡輸入和維護您保留的有關他們的個人資訊。</td>
  </tr>
  <tr>
   <td>以网页的形式查看电子邮件</td>
   <td>此元件可讓使用者以網頁的形式檢視電子郵件。</td>
  </tr>
  <tr>
   <td>隐私政策</td>
   <td>此元件會在電子郵件中插入隱私權原則的連結。<br /> </td>
  </tr>
  <tr>
   <td>取消订阅中心</td>
   <td>提供使用者取消訂閱郵寄清單的選項。</td>
  </tr>
  <tr>
   <td>订阅中心</td>
   <td>訂閱中心是一個網頁，訂閱者可以在這裡控制從您的組織收到的訊息。</td>
  </tr>
  <tr>
   <td>跟踪电子邮件打开次数</td>
   <td>可讓您使用ExactTarget追蹤功能的隱藏元件。<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此 **選項** 下拉式功能表只有在將ExactTarget設定套用至電子郵件時才會填入。 另請參閱 [套用電子郵件服務設定至電子郵件設定](#applying-e-mail-service-configuration-to-e-mail-settings) 以取得詳細資訊。

1. 將電子郵件發佈至ExactTarget。

   包含電子郵件工具的電子郵件可用於已設定的ExactTarget帳戶。

>[!NOTE]
>
>* 只有當使用傳送電子郵件時，電子郵件工具中的URL才會被其實際值取代（在收到的電子郵件中） **簡單傳送** 或 **引導式傳送** 但不是 **測試傳送**.
>
>* 需要兩種電子郵件工具： **郵寄地址（必填）** 和 **設定檔中心（必要）**. 將電子郵件發佈至ExactTarget時，這兩個電子郵件工具會預設新增至每封郵件的底部。
>


### 新增文字和個人化工具至您的電子郵件 {#adding-text-and-personalization-tool-to-your-e-mail}

您可以在電子郵件中新增個人化欄位，方法是新增 **文字和個人化** 元件至頁面：

1. 開啟要發佈至電子郵件服務的電子郵件。
1. 若要啟用電子郵件服務中的個人化欄位，請在設定電子郵件服務時新增框架設定。 另請參閱 [設定Silverpop Engage](/help/sites-administering/silverpop.md) 和 [設定精確目標](/help/sites-administering/exacttarget.md) 以取得詳細資訊。
1. 新增元件 **文字與個人化** 從副手那裡。 此元件是Newsletter群組的一部分。 在編輯模式中開啟此元件。

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 從下拉式選單中選取欄位並按一下，以將所需的個人化欄位新增至文字 **插入**.
1. 按一下 **確定** 完成。

## 套用電子郵件服務設定至電子郵件設定 {#applying-e-mail-service-configuration-to-e-mail-settings}

若要將您的電子郵件服務設定套用至電子報：

1. 建立電子郵件服務設定。
1. 開啟您的電子郵件/電子報。
1. 按一下以開啟電子郵件/電子報設定 **設定** 或按一下 **中的頁面屬性** 副手。
1. 按一下 **新增服務** 在 **Cloud Services** 標籤。 您會看到服務清單。 選取您需要的設定 —  **ExactTarget** 或 **Silverpop**  — 從下拉式清單中。

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. 单击&#x200B;**确定**。

## 發佈電子郵件至電子郵件服務 {#publishing-emails-to-email-service}

電子郵件/電子報可以依照下列步驟發佈至您的電子郵件服務：

1. 開啟電子郵件。
1. 發佈電子郵件之前，請確定您已套用正確的設定至電子郵件。
1. 单击&#x200B;**发布**。如此將可開啟 **將Newsletter發佈到電子郵件服務提供者** 視窗。
1. 填入 **Newsletter名稱** 欄位。 電子郵件/電子報會以此名稱發佈至電子郵件服務提供者。 如果未提供電子郵件名稱，則會使用AEM中電子報的頁面名稱來發佈電子郵件。
1. 单击&#x200B;**发布**。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   如果成功，AEM會確認您可以在ExactTarget或Silverpop Engage中檢視電子郵件。

   若為ExactTarget，只要按一下「 」，即可檢視已發佈的電子郵件 **檢視已發佈的電子郵件**. 這會將您直接導向ExactTarget中發佈的Newsletter ([https://members.exacttarget.com/](https://members.exacttarget.com/).)。

>[!NOTE]
>
>如果電子郵件/電子報的發佈名稱與電子郵件/電子報的發佈名稱相同，則不會取代先前的電子郵件/電子報。 而是以相同名稱建立新的電子郵件/電子報（但兩個電子報的ID不同）。
>
>將電子郵件/電子報發佈到電子郵件服務提供者也會將電子郵件/電子報發佈到AEM發佈執行個體。

### 更新已發佈的電子郵件 {#updating-a-published-e-mail}

此 **更新** 「發佈」對話方塊上的按鈕可讓您更新已發佈至電子郵件服務提供者的電子報。 如果電子報尚未發佈，而且 **更新** 已按一下按鈕，a **Newsletter未發佈** 訊息隨即顯示。

若要更新已發佈的電子郵件：

1. 開啟先前已發佈至電子郵件服務提供者的電子郵件/電子報，您要在變更電子郵件/電子報後重新發佈。
1. 单击&#x200B;**发布**。此 **將Newsletter發佈至電子郵件服務提供者** 視窗隨即顯示。 单击&#x200B;**更新**。

   若要檢查電子郵件/電子報是否已在ExactTarget上更新，請按一下 **檢視已發佈的電子郵件**. 這會將您導向至ExactTarget中已發佈的電子郵件。

   若要檢查Silverpop電子郵件服務上的電子郵件/電子報是否已更新，請造訪Silverpop Engage網站。
