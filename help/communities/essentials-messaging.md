---
title: Messaging Essentials
seo-title: Messaging Essentials
description: 消息组件概述
seo-description: 消息组件概述
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---


# Messaging Essentials {#messaging-essentials}

本页文档了使用消息组件在网站上包含消息传递功能的详细信息。

## 客户端{#essentials-for-client-side}的必备工具

**撰写消息**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
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
   <td>请参阅<a href="/help/communities/configure-messaging.md" target="_blank">配置消息</a></td>
  </tr>
  <tr>
   <td><strong>管理员配置</strong></td>
   <td><a href="/help/communities/messaging.md">配置消息</a></td>
  </tr>
 </tbody>
</table>

**消息列表**

（用于收件箱、已发送和垃圾桶）

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
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
   <td>请参阅<a href="/help/communities/configure-messaging.md" target="_blank">配置消息</a></td>
  </tr>
  <tr>
   <td><strong>管理员配置</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">配置消息</a></td>
  </tr>
 </tbody>
</table>

另请参阅[客户端自定义](/help/communities/client-customize.md)

## 服务器端{#essentials-for-server-side}的必备工具

* [配置消息传递](/help/communities/configure-messaging.md)
* [用于SCF组](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) 件的消息客户端API
* [服务](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) 的消息传递API
* [消息终结点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [服务器端自定义](/help/communities/server-customize.md)

>[!CAUTION]
>
>字符串参数必须&#x200B;*不*&#x200B;包含以下MessageBuilder方法的尾随斜杠“/”:
>
>* `setInboxPath`()
>* `setSentItemsPath`()

>
>
例如：
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### 社区站点 {#community-site}

使用向导创建的社区站点结构在选中时包括消息功能。 请参阅[社区站点控制台](/help/communities/sites-console.md#user-management)的`User Management`设置。

### 示例代码：收到的消息通知{#sample-code-message-received-notification}

社交消息功能会为操作抛出事件，例如`send`、`marking read`、`marking delete`。 可以捕获这些事件并对事件中包含的数据采取操作。

以下示例是事件处理函数，它监听`message sent`事件，并使用`Day CQ Mail Service`向所有消息收件人发送电子邮件。

要试用服务器端示例脚本，您需要开发环境和构建OSGi捆绑包的能力：

1. 以管理员身份登录到` [CRXDE|Lite](https://localhost:4502/crx/de)`。
1. 在`/apps/engage/install`中创建具有任意名称的`bundle node`，如：

   * 符号名称: `com.engage.media.social.messaging.MessagingNotification`
   * 名称：入门教程消息通知
   * 描述：用于在用户收到消息时向其发送电子邮件通知的示例服务
   * 包: `com.engage.media.social.messaging.notification`

1. 导航到`/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`，然后：

   1. 删除自动创建的`Activator.java`类。
   1. 创建类`MessageEventHandler.java`。
   1. 将下面的代码复制并粘贴到`MessageEventHandler.java`中。

1. 单击&#x200B;**保存全部**。
1. 导航到`/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`，并添加在`MessageEventHandler.java`代码中编写的所有import语句。
1. 构建捆绑包。
1. 确保已配置`Day CQ Mail Service`OSGi服务。
1. 以演示用户身份登录，并向其他用户发送电子邮件。
1. 收件人收到有关新消息的电子邮件。

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

