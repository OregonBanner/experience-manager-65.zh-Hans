---
title: 消息传送Essentials
seo-title: Messaging Essentials
description: 消息传送组件概述
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
ht-degree: 3%

---

# 消息传送Essentials {#messaging-essentials}

此页面记录使用消息传送组件在网站上包含消息传送功能的详细信息。

## 适用于客户端的Essentials {#essentials-for-client-side}

**撰写消息**

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
   <td> <strong>模板</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>参见 <a href="/help/communities/configure-messaging.md" target="_blank">配置消息传送</a></td>
  </tr>
  <tr>
   <td><strong>管理员配置</strong></td>
   <td><a href="/help/communities/messaging.md">配置消息传送</a></td>
  </tr>
 </tbody>
</table>

**消息列表**

（收件箱、已发送和垃圾桶）

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/message box</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>参见 <a href="/help/communities/configure-messaging.md" target="_blank">配置消息传送</a></td>
  </tr>
  <tr>
   <td><strong>管理员配置</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">配置消息传送</a></td>
  </tr>
 </tbody>
</table>

另请参阅 [客户端自定义](/help/communities/client-customize.md)

## 服务器端Essentials {#essentials-for-server-side}

* [配置消息传送](/help/communities/configure-messaging.md)
* [消息传送客户端API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) 对于SCF组件
* [消息传送API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) 服务
* [消息传送端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [服务器端自定义](/help/communities/server-customize.md)

>[!CAUTION]
>
>字符串参数必须 *非* 对于以下MessageBuilder方法，包含结尾斜杠“/”：
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

使用向导创建的社区站点结构在选中时包括消息传送功能。 参见 `User Management` 设置 [社区站点控制台](/help/communities/sites-console.md#user-management).

### 示例代码：消息已接收通知 {#sample-code-message-received-notification}

社交消息功能会引发操作事件，例如 `send`， `marking read`， `marking delete`. 可以捕获这些事件并对事件中包含的数据执行操作。

以下示例是一个事件处理程序，该处理程序监听 `message sent` 事件并使用 `Day CQ Mail Service`.

要尝试使用服务器端示例脚本，您需要一个开发环境以及构建OSGi捆绑包的功能：

1. 以管理员身份登录 ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. 创建 `bundle node`在 `/apps/engage/install` ，例如：

   * 符号名称: `com.engage.media.social.messaging.MessagingNotification`
   * 名称：入门教程消息通知
   * 描述：当用户收到消息时，向用户发送电子邮件通知的示例服务
   * 包: `com.engage.media.social.messaging.notification`

1. 导航到 `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`，然后：

   1. 删除 `Activator.java` 已自动创建类。
   1. 创建类 `MessageEventHandler.java`.
   1. 将下面的代码复制并粘贴到 `MessageEventHandler.java`.

1. 单击 **全部保存**.
1. 导航到 `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`，并添加中编写的所有import语句 `MessageEventHandler.java` 代码。
1. 构建捆绑包。
1. 确保 `Day CQ Mail Service`已配置OSGi服务。
1. 以演示用户身份登录，并向其他用户发送电子邮件。
1. 收件人将收到有关新消息的电子邮件。

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
