---
title: 可持续升级
seo-title: 可持续升级
description: 了解AEM 6.4中的可持续升级。
seo-description: 了解AEM 6.4中的可持续升级。
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# 可持续升级{#sustainable-upgrades}

## 自定义框架{#customization-framework}

### 架构（功能／基础架构／内容／应用程序）{#architecture-functional-infrastructure-content-application}

自定义框架功能旨在帮助减少非扩展区域的代码（如API）或内容（如叠加）中不易升级的违规。

自定义框架有两个组件：**API Surface**&#x200B;和&#x200B;**内容分类**。

#### API Surface {#api-surface}

在AEM的先前发行版中，许多API通过Uber Jar公开。 这些API中的一些并非客户使用的，但它们暴露在不同捆绑套件中支持AEM功能。 今后，Java API将标为“公共”或“私有”，向客户指示哪些API在升级环境中是安全的。 其他具体信息包括：

* 标记为`Public`的Java API可以由自定义实现包使用和引用。

* 公共API将向后兼容兼容性包的安装。
* 兼容性软件包将包含兼容性Uber JAR，以确保向后兼容性
* 标为`Private`的Java API仅供AEM内部捆绑包使用，不应由自定义捆绑包使用。

>[!NOTE]
>
>在这种情况下，`Private`和`Public`的概念不应与Java的公共类和私有类概念混淆。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 内容分类{#content-classifications}

AEM长期以来一直使用叠加和Sling Resource Merager的原则来允许客户扩展和自定义AEM功能。 为AEM控制台和UI提供支持的预定义功能存储在&#x200B;**/libs**&#x200B;中。 客户永远不得修改&#x200B;**/libs**&#x200B;下的任何内容，但可在&#x200B;**/apps**&#x200B;下添加其他内容，以覆盖和扩展在&#x200B;**/libs**&#x200B;中定义的功能（有关详细信息，请参阅使用叠加进行开发）。 当将AEM升级为&#x200B;**/libs**&#x200B;中的内容时，这仍然会引起许多问题，这些问题可能会发生变化，导致叠加功能以意外方式中断。 客户还可以通过`sling:resourceSuperType`继承扩展AEM组件，或直接通过sling:resourceType引用&#x200B;**/libs**&#x200B;中的组件。 类似的升级问题可能与引用和覆盖用例有关。

为了使客户更安全、更容易地了解&#x200B;**/libs**&#x200B;的哪些区域是安全的，并且将&#x200B;**/libs**&#x200B;中的内容与以下混音进行了分类：

* **公共(granite:PublicArea)** -将节点定义为公共，以便它可以覆盖、继承() `sling:resourceSuperType`或直接() `sling:resourceType`使用。添加兼容性包后，/libs下标为“公共”的节点将安全升级。 一般而言，客户只应利用标记为“公共”的节点。

* **摘要(granite:AbstractArea)** -将节点定义为摘要。节点可以覆盖或继承(`sling:resourceSupertype`)，但不能直接使用(`sling:resourceType`)。

* **Final(granite:FinalArea)** -将节点定义为final。分类为最终理想状态的节点不应被覆盖或继承。 最终节点可以直接通过`sling:resourceType`使用。 默认情况下，最终节点下的子节点被视为内部节点。

* ***内部(granite:InternalArea)*** *- *将节点定义为内部节点。分类为内部理想状态的节点不应被覆盖、继承或直接使用。 这些节点仅用于AEM的内部功能

* **无注释** -节点根据树层次继承分类。默认情况下，/ root为公共。 **父节点分类为“内部”或“最终”的节点也被视为“内部”。**

>[!NOTE]
>
>这些策略仅针对基于Sling搜索路径的机制实施。 **/libs**&#x200B;的其他区域（如客户端库）可标记为`Internal`，但仍可与标准clientlib包含一起使用。 在这些情况下，客户应继续遵守内部分类。

#### CRXDE Lite内容类型指示器{#crxde-lite-content-type-indicators}

在CRXDE Lite中应用的混合将显示标记为`INTERNAL`为灰显的内容节点和树。 对于`FINAL`，图标将灰显。 这些节点的子项也将显示为灰色。 这两种情况下均禁用“叠加节点”功能。

**公共**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最终**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**内部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**内容运行状况检查**

>[!NOTE]
>
>自AEM 6.5起，Adobe建议使用模式检测器检测内容访问违规。 模式检测器报告更加详细，检测问题更多，降低误报概率。
>
>有关详细信息，请参阅[使用模式检测器评估升级复杂性](/help/sites-deploying/pattern-detector.md)。

AEM 6.5附带运行状况检查，以在以与内容分类不一致的方式使用覆盖或引用的内容时提醒客户。

** Sling/Granite内容访问检查**是一项新的运行状况检查，它监视存储库，以查看客户代码是否错误地访问AEM中的受保护节点。

此操作将扫描&#x200B;**/apps**，通常需要几秒才能完成。

要访问此新的运行状况检查，您需要执行以下操作：

1. 从AEM主屏幕，导航到&#x200B;**工具>操作>运行状况报告**
1. 单击&#x200B;**Sling/Granite内容访问检查**，如下所示：

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

扫描完成后，将显示一列表警告，通知未正确引用的受保护节点的最终用户：

![截屏-2018-2-5健康报告](assets/screenshot-2018-2-5healthreports.png)

修复违规后，将返回绿色状态：

![截屏-2018-2-5健康报告违规](assets/screenshot-2018-2-5healthreports-violations.png)

运行状况检查显示由后台服务收集的信息，当所有Sling搜索路径中使用叠加或资源类型时，后台服务会异步检查该信息。 如果内容混合使用不正确，则报告违规。
