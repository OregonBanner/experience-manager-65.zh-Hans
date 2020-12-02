---
title: 与Adobe Target整合的先决条件
seo-title: 与Adobe Target整合的先决条件
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
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 3%

---


# 与Adobe Target集成的先决条件{#prerequisites-for-integrating-with-adobe-target}

作为AEM和Adobe Target](/help/sites-administering/target.md)集成的[的一部分，您需要向Adobe Target注册，配置复制代理，并在发布节点上安全活动设置。

## 向Adobe Target注册{#registering-with-adobe-target}

要将AEM与Adobe Target集成，您必须拥有有效的Adobe Target帐户。 此帐户必须至少具有&#x200B;**审批者**&#x200B;级别权限。 当你向Adobe Target注册时，你会收到一个客户代码。 您需要客户端代码和Adobe Target登录名和密码才能将AEM连接到Adobe Target。

客户代码在调用Adobe Target服务器时标识Adobe Target客户帐户。

>[!NOTE]
>
>目标团队还必须启用您的帐户才能使用集成。
>
>如果不是，请联系[Adobe客户服务中心](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html)。

## 启用目标复制代理{#enabling-the-target-replication-agent}

必须在创作实例上启用测试和目标[复制代理](/help/sites-deploying/replication.md)。 请注意，如果您使用[ nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent)运行模式安装AEM，则此复制代理在默认情况下不处于启用状态。 有关保护生产环境的详细信息，请参阅[安全清单](/help/sites-administering/security-checklist.md)。

1. 在AEM主页上，单击或点按&#x200B;**工具** > **部署** > **复制**。
1. 单击或点按&#x200B;**作者上的代理**。
1. 单击或点按&#x200B;**测试和目标(测试和目标)**&#x200B;复制代理，然后单击或点按&#x200B;**编辑**。
1. 选择“启用”选项，然后单击或点按&#x200B;**确定**。

   >[!NOTE]
   >
   >配置测试和目标复制代理时，在&#x200B;**传输**&#x200B;选项卡中，默认情况下将URI设置为&#x200B;**tnt:///**。 请勿将此URI替换为&#x200B;**https://admin.testandtarget.omniture.com**。
   >
   >请注意，如果尝试使用&#x200B;**tnt:///**&#x200B;测试连接，将引发错误。 这是预期行为，因为此URI仅供内部使用，不应与&#x200B;**测试连接**&#x200B;一起使用。

## 保护活动设置节点{#securing-the-activity-settings-node}

必须保护发布实例上的活动设置节点&#x200B;**cq:ActivitySettings**，以使普通用户无法访问它。 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。

**cq:ActivitySettings**&#x200B;节点在CRXDE lite的`/content/campaigns/*nameofbrand*`* *活动jcr:contentnode;* *例如`/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`下。 此节点仅在目标组件后创建。

活动的jcr:content下的&#x200B;**cq:ActivitySettings**&#x200B;节点受以下ACL保护：

* 拒绝所有人
* 允许“目标-活动-作者”的jcr:read,rep:write（作者是此组的成员，开箱即用）
* 允许jcr:read,rep:write for &quot;targetservice&quot;

这些设置确保普通用户无权访问节点属性。 在创作和发布时使用相同的ACL。 有关详细信息，请参阅[用户管理和安全](/help/sites-administering/security.md)。

## 配置AEM Link Externalizer {#configuring-the-aem-link-externalizer}

在Adobe Target编辑活动时，URL将指向&#x200B;**localhost**，除非您更改AEM创作节点上的URL。 如果希望导出的内容指向特定的&#x200B;*publish*&#x200B;域，可以配置AEM Link Externalizer。

>[!NOTE]
>
>另请参阅[添加云配置](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)。

配置AEM externalizer:

>[!NOTE]
>
>有关详细信息，请参阅[将URL外部化](/help/sites-developing/externalizer.md)。

1. 导航到位于&#x200B;**https://&lt;server>的OSGi Web控制台：&lt;port>/system/console/configMgr.**
1. 查找&#x200B;**Day CQ Link Externalizer**&#x200B;并输入创作节点的域。

   ![chlimage_1-120](assets/aem-externalizer-01.png)

