---
title: 封装令牌支持
seo-title: Encapsulated Token Support
description: 了解AEM中的封装令牌支持。
seo-description: Learn about the Encapsulated Token support in AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: ed2cb35593780cd627c15f493e58d3b68c55519b
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# 封装令牌支持{#encapsulated-token-support}

## 简介 {#introduction}

默认情况下，AEM使用令牌身份验证处理程序来验证每个请求。 但是，要为身份验证请求提供服务，令牌身份验证处理程序要求访问每个请求的存储库。 发生这种情况是因为使用Cookie来维护身份验证状态。 从逻辑上讲，状态需要保留在存储库中，以便验证后续请求。 实际上，这意味着身份验证机制是有状态的。

这对于横向可扩展性尤其重要。 在像下面描述的发布场这样的多实例设置中，无法以最佳方式实现负载平衡。 使用有状态身份验证，持久身份验证状态将仅在用户首次进行身份验证的实例上可用。

![chlimage_1-33](assets/chlimage_1-33a.png)

以下列方案为例：

用户可以在发布实例1上进行身份验证，但如果后续请求转到发布实例2，则该实例没有该持久身份验证状态，因为该状态持久保留在发布实例1和发布实例2的存储库中，并且发布实例2拥有自己的存储库。

这个问题的解决方案是在负载平衡器级别配置粘性连接。 使用粘性连接时，用户始终会被定向到同一发布实例。 因此，不可能实现真正最优的负载平衡。

如果发布实例不可用，则所有在该实例上进行身份验证的用户都将丢失其会话。 这是因为验证身份验证Cookie需要存储库访问权限。

## 使用封装令牌的无状态身份验证 {#stateless-authentication-with-the-encapsulated-token}

水平可扩展性的解决方案是使用AEM中新的封装令牌支持进行无状态身份验证。

封装令牌是一种加密技术，它允许AEM离线安全地创建和验证身份验证信息，而无需访问存储库。 这样，就可以在所有发布实例上发生身份验证请求，而无需粘性连接。 它还有提高身份验证性能的优势，因为不需要访问存储库即可访问每个身份验证请求。

您可以在下方通过MongoMK作者和TarMK发布实例看到如何在地理上分散的部署中这样做：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>请注意，封装令牌与身份验证有关。 它确保无需访问存储库即可验证Cookie。 但是，仍要求用户存在于所有实例上，并且每个实例都可以访问存储在该用户下的信息。
>
>例如，如果在第一个发布实例上创建新用户，则由于封装令牌的工作方式，它将在第二个发布实例上成功进行身份验证。 如果用户在第二个发布实例上不存在，则请求仍将失败。

## 配置封装令牌 {#configuring-the-encapsulated-token}

>[!NOTE]
>在以下情况下，同步用户并依赖令牌身份验证（如SAML和OAuth）的所有身份验证处理程序只能与封装的令牌一起使用：
>
>* 已启用粘性会话，或者
>
>* 同步启动时已在AEM中创建用户。 这意味着在处理程序的情况下，将不支持封装令牌 **创建** 同步过程中的用户。


配置封装令牌时需要考虑以下几个事项：

1. 由于涉及加密技术，所有实例都需要具有相同的HMAC密钥。 从AEM 6.3开始，关键资料不再存储在存储库中，而是存储在实际的文件系统上。 考虑到这一点，复制密钥的最佳方法是将密钥从源实例的文件系统复制到要将密钥复制到的目标实例的文件系统。 请参阅下面的“复制HMAC密钥”下的更多信息。
1. 需要启用封装令牌。 可以通过Web控制台完成此操作。

### 复制HMAC密钥 {#replicating-the-hmac-key}

要跨实例复制密钥，您需要：

1. 访问包含要复制的关键材料的AEM实例，通常是创作实例；
1. 找到 `com.adobe.granite.crypto.file` 捆绑包中的文件。 例如，在此路径下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   此 `bundle.info` 每个文件夹中的文件将标识包名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 复制HMAC和主控文件。
1. 然后，转到要将HMAC密钥复制到的目标实例，并导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 粘贴您之前复制的两个文件。
1. [刷新加密捆绑包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 如果目标实例已在运行。

1. 对要将密钥复制到的所有实例重复上述步骤。

#### 启用封装令牌 {#enabling-the-encapsulated-token}

复制HMAC密钥后，您可以通过Web控制台启用封装令牌：

1. 将浏览器指向 `https://serveraddress:port/system/console/configMgr`
1. 查找名为的条目 **Granite令牌身份验证处理程序Adobe** 然后点击它。
1. 在以下窗口中，勾选 **启用封装令牌支持** 框，然后按 **保存**.
