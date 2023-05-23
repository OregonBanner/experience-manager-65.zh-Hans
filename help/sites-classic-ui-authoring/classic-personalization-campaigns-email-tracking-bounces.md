---
title: 追蹤退信電子郵件
seo-title: Tracking Bounced Emails
description: 當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 傳送電子報回這些地址。 AEM可以管理這些跳出，並在超過設定的跳出計數器後停止傳送電子報到這些地址。
seo-description: When you send a newsletter to many users, there are usually some invalid emails addresses in the list. Sending newsletters to those addresses bounce back. AEM is capable of managing those bounces and can stop sending newsletters to those addresses after the configured bounce counter is exceeded.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 追蹤退信電子郵件{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe不打算進一步增強追蹤由AEM SMTP服務傳送的已開啟/已退回電子郵件。
>
>建議如下 [使用Adobe Campaign及其AEM整合](/help/sites-administering/campaign.md).

當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 傳送電子報回這些地址。 AEM可以管理這些跳出，並在超過設定的跳出計數器後停止傳送電子報到這些地址。 依預設，跳出率會設為3，但可設定。

若要設定AEM以追蹤彈回電子郵件，請設定AEM以輪詢接收彈回電子郵件的現有信箱。 通常，此位置是您指定傳送Newsletter的來源電子郵件地址。 AEM會輪詢此收件匣，並匯入位於輪詢設定中所指定路徑下方的所有電子郵件。 然後會觸發工作流程，以搜尋使用者內退信的電子郵件地址，並相應地更新使用者的bounceCounter屬性值。 超過設定的最大彈回數後，使用者會從Newsletter清單中移除。

## 設定摘要匯入工具 {#configuring-the-feed-importer}

摘要匯入工具可讓您重複地將外部來源的內容匯入存放庫。 使用摘要匯入工具的這個設定，AEM會檢查寄件者的信箱是否有退回的電子郵件。

若要設定摘要匯入工具來追蹤彈回電子郵件，請執行下列動作：

1. 在 **工具**，選取摘要匯入工具。

1. 按一下 **新增** 以建立設定。

   ![chlimage_1](assets/chlimage_1a.png)

1. 選取型別，並將資訊新增至輪詢URL，以便您設定主機和連線埠，藉此新增設定。 此外，將一些郵件和通訊協定特定的引數新增到URL查詢中。 設定為每天至少輪詢一次。

   所有設定都需要輪詢URL中下列專案的相關資訊：

   `username`：用於連線的使用者名稱

   `password`：用來連線的密碼

   此外，您可以根據通訊協定來設定特定設定。

   **POP3設定屬性：**

   `pop3.leave.on.server`：定義是否要將訊息留在伺服器上。 設為true會在伺服器上保留訊息，否則則為false。 預設為true。

   **POP3範例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | 透過SSL使用pop3連線至連線埠995上的GMail （使用者/密碼），依預設會在伺服器上留下訊息 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP設定屬性：**

   可讓您設定要搜尋的標幟。

   `imap.flag.SEEN`：設定新增/未檢視訊息為false，已讀取訊息為true

   另請參閱 [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) 以取得完整的旗標清單。

   **IMAP範例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | 透過SSL使用IMAP連線至具有使用者/密碼的連線埠993上的GMail。 僅依預設取得新訊息。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | 使用IMAP over SSL連線至具有使用者/密碼的GMail 993，只會看到訊息。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | 使用IMAP over SSL連線至具有使用者/密碼的GMail 993，已讀取或收到新訊息。 |

1. 保存配置。

## 設定Newsletter服務元件 {#configuring-the-newsletter-service-component}

在設定摘要匯入工具後，請設定「寄件者」位址和「跳出」計數器。

若要設定Newsletter服務：

1. 在OSGi主控台中，位於 `<host>:<port>/system/console/configMgr`，導覽至 **MCM電子報**.

1. 完成時設定服務並儲存變更。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   可設定下列設定來調整行為：

   | 彈回計數器最大值(max.bounce.count) | 定義在傳送Newsletter時直到使用者被省略之前的跳出次數。 將此值設為0，會完全停用退信檢查。 |
   |---|---|
   | 活動無快取(sent.activity.nocache) | 定義快取設定以用於電子報傳送活動 |

   儲存後，Newsletter MCM服務會執行以下操作：

   * 在成功傳送Newsletter時將活動寫入使用者隱藏的資料流。
   * 在偵測到跳出且使用者跳出計數器變更時寫入活動。
