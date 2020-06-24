---
title: 与Adobe Target集成的先决条件
seo-title: 与Adobe Target集成的先决条件
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

作为AEM和Adobe Target [集成的一部分](/help/sites-administering/target.md)，您需要向Adobe Target注册，配置复制代理，并在发布节点上安全活动设置。

## 向Adobe Target注册 {#registering-with-adobe-target}

要将AEM与Adobe Target集成，您必须拥有有效的Adobe Target帐户。 此帐户必须至 **少具有** “审批者”级别权限。 注册Adobe Target时，您会收到客户代码。 您需要客户端代码以及Adobe Target登录名和口令才能将AEM连接到Adobe Target。

客户代码在调用Adobe Target服务器时标识Adobe Target客户帐户。

>[!NOTE]
>
>Target团队还必须启用您的帐户才能使用集成。
>
>如果情况不是这样，请与Adobe客 [户服务部联系](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html)。

## 启用Target复制代理 {#enabling-the-target-replication-agent}

必须在创作实 [例上启用](/help/sites-deploying/replication.md) “测试和Target”复制代理。 请注意，如果您使用nosamplecontent运行模式安装AEM, [则此复](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 制代理在默认情况下不启用。 有关保护生产环境的更多信息，请参阅安 [全核对清单](/help/sites-administering/security-checklist.md)。

1. 在AEM主页中，单击或点按 **工具** > **部署** > **复制**。
1. 单击或点按作 **者上的代理**。
1. 单击或点按测 **试和Target(测试和目标)复** 制代理 **，然后单击或点按**&#x200B;编辑。
1. 选择“启用”选项，然后单击或点 **按确定**。

   >[!NOTE]
   >
   >配置测试和Target复制代理时，在“传输 **”选** 项卡中，URI默认设置为 **tnt:///**。 请勿将此URI替换为 **https://admin.testandtarget.omniture.com**。
   >
   >请注意，如果尝试使用tnt:///测试连接 ****，将引发错误。 这是预期行为，因为此URI仅供内部使用，不应与测试连接 **一起使用**。

## 保护活动设置节点 {#securing-the-activity-settings-node}

You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。

cq: **ActivitySettings节点** ，在CRXDE lite的jcr:content节点 `/content/campaigns/*nameofbrand*`*下， *活动jcr:content节点下可用；* *例如 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`。 此节点仅在目标组件后创建。

活动 **的jcr** :content下的cq:ActivitySettings节点受以下ACL的保护：

* 拒绝所有人
* 允许“目标-活动-作者”的jcr:read,rep:write（作者是此组的成员，开箱即用）
* 允许jcr:read,rep:write for &quot;targetservice&quot;

这些设置确保普通用户无权访问节点属性。 在创作和发布时使用相同的ACL。 有关 [详细信息，请参阅](/help/sites-administering/security.md) “用户管理和安全”。

## 配置AEM Link Externalizer {#configuring-the-aem-link-externalizer}

在Adobe Target中编辑活动时，除非您更改AEM作 **者节** 点上的URL，否则URL将指向localhost。 如果希望导出的内容指向特定发布域，则可以配置AEM Link *Externalizer* 。

>[!NOTE]
>
>另请参阅 [添加云配置](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)。

要配置AEM externalizer:

>[!NOTE]
>
>有关详细信息，请 [参阅将URL外置](/help/sites-developing/externalizer.md)。

1. 导航到位于https://&lt; **server>:&lt;port>/system/console/configMgr的OSGi Web控制台。**
1. 查 **找Day CQ Link Externalizer** ，然后输入创作节点的域。

   ![chlimage_1-120](assets/aem-externalizer-01.png)

