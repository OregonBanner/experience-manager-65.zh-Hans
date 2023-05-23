---
title: 傳訊要點
seo-title: Messaging Essentials
description: 傳訊元件概觀
seo-description: Messaging component overview
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 2%

---

# 傳訊要點 {#messaging-essentials}

本頁會記錄使用傳訊元件的詳細資訊，以便在網站上包含傳訊功能。

## 適用於使用者端的Essentials {#essentials-for-client-side}

**撰寫訊息**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>另請參閱 <a href="/help/communities/configure-messaging.md" target="_blank">設定傳訊</a></td>
  </tr>
  <tr>
   <td><strong>管理員設定</strong></td>
   <td><a href="/help/communities/messaging.md">設定傳訊</a></td>
  </tr>
 </tbody>
</table>

**訊息清單**

（收件匣、已傳送和垃圾桶）

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messageBox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>另請參閱 <a href="/help/communities/configure-messaging.md" target="_blank">設定傳訊</a></td>
  </tr>
  <tr>
   <td><strong>管理員設定</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">設定傳訊</a></td>
  </tr>
 </tbody>
</table>

另請參閱 [使用者端自訂](/help/communities/client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [設定傳訊](/help/communities/configure-messaging.md)
* [傳訊使用者端API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) 適用於SCF元件
* [傳訊API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) 服務
* [傳訊端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [伺服器端自訂](/help/communities/server-customize.md)

>[!CAUTION]
>
>字串引數必須 *not* 包含下列MessageBuilder方法的結尾斜線「/」：
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>例如：
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### 社区站点 {#community-site}

使用精靈建立的社群網站結構，在選取時包含傳訊功能。 另請參閱 `User Management` 設定 [社群網站主控台](/help/communities/sites-console.md#user-management).

### 範常式式碼：訊息已接收通知 {#sample-code-message-received-notification}

社交訊息功能會擲回作業事件，例如 `send`， `marking read`， `marking delete`. 您可以擷取這些事件，並對事件中包含的資料採取動作。

以下範例是事件處理常式的範例，它會偵聽 `message sent` 事件並傳送電子郵件給所有郵件收件者，使用 `Day CQ Mail Service`.

若要嘗試伺服器端範例指令碼，您需要開發環境和建置OSGi套件的功能：

1. 以管理員身分登入 ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. 建立 `bundle node`在 `/apps/engage/install` 具有任意名稱，例如：

   * 符号名称: `com.engage.media.social.messaging.MessagingNotification`
   * 名稱：快速入門教學課程訊息通知
   * 說明：當使用者收到訊息時，傳送電子郵件通知給使用者的範例服務
   * 包: `com.engage.media.social.messaging.notification`

1. 導覽至 `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`，然後：

   1. 刪除 `Activator.java` 類別已自動建立。
   1. 建立類別 `MessageEventHandler.java`.
   1. 將下列程式碼複製並貼到 `MessageEventHandler.java`.

1. 按一下 **全部儲存**.
1. 導覽至 `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`，並新增所有匯入陳述式，如中所寫入 `MessageEventHandler.java` 程式碼。
1. 建置套件組合。
1. 確定 `Day CQ Mail Service`OSGi服務已設定。
1. 以示範使用者身分登入，並傳送電子郵件給其他使用者。
1. 收件者會收到有關新訊息的電子郵件。

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
