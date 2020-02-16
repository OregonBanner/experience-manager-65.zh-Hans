---
title: 与Adobe target集成的先决条件
seo-title: 与Adobe target集成的先决条件
description: 了解与Adobe Target集成的先决条件。
seo-description: 了解与Adobe Target集成的先决条件。
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# 与Adobe target集成的先决条件{#prerequisites-for-integrating-with-adobe-target}

作为AEM和Adobe [Target集成的一部分](/help/sites-administering/target.md)，您需要向Adobe Target注册，在发布节点上配置复制代理和安全活动设置。

## 向Adobe Target注册 {#registering-with-adobe-target}

要将AEM与Adobe Target集成，您必须拥有有效的Adobe target帐户。 此帐户必须至少具 **有批准者** 级别的权限。 当您向Adobe Target注册时，您会收到一个客户端代码。 您需要客户端代码和Adobe target登录名和密码才能将AEM连接到Adobe Target。

客户端代码在调用Adobe Target服务器时标识Adobe target客户帐户。

>[!NOTE]
>
>要使用集成，Target团队还必须启用您的帐户。
>
>
>如果不是这样，请联系 [Adobe Target客户关怀](https://marketing.adobe.com/resources/help/en_US/target/target/r_problem.html)。

## 启用目标复制代理 {#enabling-the-target-replication-agent}

必须在创作实 [例上启用](/help/sites-deploying/replication.md) Test和Target复制代理。 请注意，如果您使用nosamplecontent运行模式安装AEM，则此复制代 [理在默认情况下](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 不启用。 有关保护生产环境的更多信息，请参阅安 [全清单](/help/sites-administering/security-checklist.md)。

1. 在AEM主页上，单击或点按工 **具** > **Deployment** > **Replication**。
1. 单击或点按作 **者上的代理**。
1. 单击或点按测 **试和目标（测试和目标）复制代理** ，然后单击或点按编 **辑**。
1. 选择“已启用”选项，然后单击或点按 **确定**。

   >[!NOTE]
   >
   >配置Test和Target复制代理时，在“传输 **** ”选项卡中，默认情况下将URI设置为 **tnt:///**。 请勿将此URI替换为 **https://admin.testandtarget.omniture.com**。
   >
   >请注意，如果尝试使用tnt:///测试连接 ****，将引发错误。 这是预期行为，因为此URI仅供内部使用，不应与测试连接一 **起使用**。

## 保护“活动设置”节点 {#securing-the-activity-settings-node}

You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。

**cq:ActivitySettings节点**&#x200B;在CRXDE lite中的活动jcr`/content/campaigns/*nameofbrand*`**:content节点下的*下可用；*例如 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`。 此节点仅在您定位组件后创建。

活 **** 动的jcr:content下的cq:ActivitySettings节点受以下ACL的保护：

* 拒绝所有人
* 允许“target-activity-authors”的jcr:read,rep:write（author是该组的一个现成成员）
* 允许jcr:read,rep:write for &quot;targetservice&quot;

这些设置可确保普通用户无权访问节点属性。 在创作和发布时使用相同的ACL。 有关更 [多信息，请参阅用户管理](/help/sites-administering/security.md) 和安全性。

## 配置AEM Link Externalizer {#configuring-the-aem-link-externalizer}

在Adobe Target中编辑活动时，除非您更改AEM作者节 **点上的** URL，否则URL将指向localhost。 如果希望导出的内容指向特定的发布域，则可以配置AEM Link Externalizer ** 。

>[!NOTE]
>
>另请参阅 [添加云配置](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)。

要配置AEM externalizer，请执行以下操作：

>[!NOTE]
>
>有关详细信息，请参 [阅将URL外置](/help/sites-developing/externalizer.md)。

1. 导航到位于https://&lt;server>:&lt;port>/system/console/configMgr的OSGi web控 **制台。**
1. 查 **找Day CQ Link Externalizer** ，然后输入创作节点的域。

   ![chlimage_1-120](assets/aem-externalizer-01.png)

