---
title: 封装的令牌支持
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
source-git-commit: 32e2a30d9f3327d26b81a07730ace04e4e68b0d1
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# 封装的令牌支持{#encapsulated-token-support}

## 简介 {#introduction}

默认情况下，AEM使用令牌身份验证处理程序来验证每个请求。 但是，为了提供身份验证请求，令牌身份验证处理程序需要访问每个请求的存储库。 之所以出现这种情况，是因为使用Cookie维护身份验证状态。 从逻辑上讲，需要在存储库中保留状态以验证后续请求。 实际上，这意味着身份验证机制是有状态的。

这对于横向扩展性来说尤为重要。 在多实例设置中（如下面所示的发布场），无法以最佳方式实现负载平衡。 通过有状态身份验证，持久身份验证状态将仅在用户首次进行身份验证的实例上可用。

![chlimage_1-33](assets/chlimage_1-33a.png)

以下方案为例：

用户可能在发布实例1上进行了身份验证，但如果后续请求转到发布实例2，则该实例没有持久的身份验证状态，因为该状态会保留在发布实例1的存储库中，而发布实例2具有其自己的存储库。

解决方案是在负载平衡器级别配置置顶连接。 通过粘性连接，用户将始终定向到同一发布实例。 因此，无法真正地实现最佳负载平衡。

如果发布实例不可用，则在该实例上经过身份验证的所有用户都将丢失其会话。 这是因为验证身份验证Cookie需要存储库访问。

## 使用封装的令牌进行无状态身份验证 {#stateless-authentication-with-the-encapsulated-token}

水平可扩展性解决方案是使用AEM中新的封装令牌支持进行无状态身份验证。

封装令牌是一段密码学，它允许AEM在脱机时安全地创建和验证身份验证信息，而无需访问存储库。 这样，就可以在所有发布实例上发生身份验证请求，而无需粘性连接。 它还具有提高身份验证性能的优势，因为无需为每个身份验证请求访问存储库。

您可以在下面的MongoMK作者和TarMK发布实例中，了解在地理上分散的部署中这项功能的工作原理：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>请注意，封装令牌与身份验证有关。 它可确保无需访问存储库即可验证Cookie。 但是，仍然需要用户存在于所有实例上，并且每个实例都可以访问存储在该用户下的信息。
>
>例如，如果由于封装令牌的工作方式而在发布实例号1上创建了新用户，则该用户将在发布实例号2上成功进行身份验证。 如果用户在第二个发布实例上不存在，则请求仍将不成功。

## 配置封装令牌 {#configuring-the-encapsulated-token}

>[!NOTE]
>只有符合以下条件时，所有可同步用户并依赖令牌身份验证（如SAML和OAuth）的身份验证处理程序才能与封装的令牌一起使用：
>
>* 会话会置顶，或
>
>* 同步开始时，已在AEM中创建用户。 这意味着在处理程序 **创建** 用户。


在配置封装令牌时，您需要考虑以下几项：

1. 由于涉及的密码学，所有实例都需要具有相同的HMAC密钥。 自AEM 6.3起，关键材料不再存储在存储库中，而是存储在实际的文件系统中。 考虑到这一点，复制密钥的最佳方法是将它们从源实例的文件系统复制到要将密钥复制到的目标实例的文件系统。 请参阅下面“复制HMAC密钥”下的更多信息。
1. 需要启用封装令牌。 这可以通过Web控制台来完成。

### 复制HMAC密钥 {#replicating-the-hmac-key}

HMAC密钥以的二进制属性存在 `/etc/key` 中。 您可以通过按 **视图** 链接：

![chlimage_1-35](assets/chlimage_1-35a.png)

要跨实例复制密钥，您需要：

1. 访问包含要复制的关键材料的AEM实例，通常是创作实例；
1. 找到 `com.adobe.granite.crypto.file` 包。 例如，在以下路径下：

   * &lt;author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21

   的 `bundle.info` 每个文件夹中的文件将标识包名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制HMAC和主控文件。
1. 然后，转到要将HMAC密钥复制到的目标实例，然后导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴您之前复制的两个文件。
1. [刷新加密包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 目标实例已在运行时。

1. 对要将密钥复制到的所有实例重复上述步骤。

#### 启用封装令牌 {#enabling-the-encapsulated-token}

复制HMAC密钥后，您可以通过Web控制台启用封装令牌：

1. 将您的浏览器指向 `https://serveraddress:port/system/console/configMgr`
1. 查找名为 **AdobeGranite令牌身份验证处理程序** 然后单击它。
1. 在以下窗口中，勾选 **启用封装令牌支持** 框和按 **保存**.
