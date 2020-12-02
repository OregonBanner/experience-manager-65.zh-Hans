---
title: 封装的令牌支持
seo-title: 封装的令牌支持
description: 了解AEM中的封装令牌支持。
seo-description: 了解AEM中的封装令牌支持。
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
translation-type: tm+mt
source-git-commit: 215f062f80e7abfe35698743ce971394d01d0ed6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---


# 封装的令牌支持{#encapsulated-token-support}

## 简介 {#introduction}

默认情况下，AEM使用令牌身份验证处理程序对每个请求进行身份验证。 但是，为了提供身份验证请求，令牌身份验证处理程序需要对每个请求都访问存储库。 这是因为使用cookies来维护身份验证状态。 逻辑上，状态需要保留在存储库中，以验证后续请求。 实际上，这意味着身份验证机制是有状态的。

这对于水平可伸缩性尤为重要。 在多实例设置中，如下图所示的发布场，无法以最佳方式实现负载平衡。 使用状态身份验证时，保留的身份验证状态仅在用户首次通过身份验证的实例上可用。

![chlimage_1-33](assets/chlimage_1-33a.png)

以下场景为例：

用户可以在发布实例1上对用户进行身份验证，但如果后续请求转到发布实例2，则该实例不具有持久的身份验证状态，因为该状态在发布实例1的存储库中被保留，而发布实例2具有其自己的存储库。

解决方案是在负载平衡器级别配置粘贴连接。 使用粘滞连接时，用户始终被定向到同一发布实例。 因此，不可能实现真正最优的负载平衡。

如果发布实例不可用，在该实例上经过身份验证的所有用户都将丢失其会话。 这是因为验证Cookie需要存储库访问。

## 使用封装的令牌{#stateless-authentication-with-the-encapsulated-token}进行无状态身份验证

水平可伸缩性的解决方案是使用AEM中新的封装令牌支持进行无状态身份验证。

封装令牌是一种密码术，它允许AEM安全地创建和验证脱机身份验证信息，而无需访问存储库。 这样，就可以在所有发布实例上发生身份验证请求，无需粘滞连接。 它还具有提高身份验证性能的优势，因为每次身份验证请求都不需要访问存储库。

您可以在下面的MongoMK作者和TarMK发布实例中了解这在地理上分布的部署中的工作方式：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>请注意，封装令牌与身份验证相关。 它确保无需访问存储库即可验证Cookie。 但是，仍然需要用户存在于所有实例中，并且每个实例都可以访问存储在该用户下的信息。
>
>例如，如果根据封装令牌的工作方式在发布实例编号1上创建了新用户，则将在发布实例编号2上成功对其进行身份验证。 如果第二个发布实例上不存在该用户，则请求仍不成功。


## 配置封装令牌{#configuring-the-encapsulated-token}

>[!NOTE]
>只有在以下情况下，才能使用同步用户和依赖令牌身份验证（如SAML和OAuth）的所有身份验证处理程序才能使用封装的令牌：
>
>* 会话粘滞已启用，或
   >
   >
* 同步开始时，已在AEM中创建用户。 这意味着在同步过程中，如果处理程序&#x200B;**创建**&#x200B;用户，将不支持封装令牌。


在配置封装令牌时，您需要考虑以下几点：

1. 由于涉及密码，所有实例都需要具有相同的HMAC密钥。 自AEM 6.3以来，关键材料不再存储在存储库中，而存储在实际的文件系统中。 考虑到这一点，复制密钥的最佳方法是将它们从源实例的文件系统复制到要复制密钥的目标实例的文件系统。 请参阅下面的“复制HMAC密钥”下的更多信息。
1. 需要启用封装令牌。 这可以通过Web控制台完成。

### 复制HMAC密钥{#replicating-the-hmac-key}

HMAC密钥作为`/etc/key`的二进制属性存在于存储库中。 您可以通过按下视图旁的&#x200B;**链接**&#x200B;单独下载它：

![chlimage_1-35](assets/chlimage_1-35a.png)

为了跨实例复制密钥，您需要：

1. 访问AEM实例，通常是包含要复制的关键材料的作者实例；
1. 在本地文件系统中找到`com.adobe.granite.crypto.file`包。 例如，在此路径下：

   * &lt;author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21

   每个文件夹中的`bundle.info`文件将标识捆绑名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制HMAC和主控文件。
1. 然后，转到要将HMAC密钥重复到的目标实例，并导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴之前复制的两个文件。
1. [如果目标](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 实例已运行，请刷新Crypto Bundle。

1. 对要将密钥复制到的所有实例重复上述步骤。

#### 启用封装令牌{#enabling-the-encapsulated-token}

复制HMAC密钥后，您可以通过Web控制台启用封装令牌：

1. 将浏览器指向`https://serveraddress:port/system/console/configMgr`
1. 查找名为&#x200B;**Day CRX令牌身份验证处理程序**&#x200B;的条目，然后单击它。
1. 在以下窗口中，勾选&#x200B;**启用封装的令牌支持**&#x200B;框，然后按&#x200B;**保存**。

