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

---


# 可持续升级{#sustainable-upgrades}

## 自定义框架 {#customization-framework}

### 架构（功能／基础架构／内容／应用程序） {#architecture-functional-infrastructure-content-application}

自定义框架功能旨在帮助减少在不易升级的代码（如API）或内容（如叠加）的非可扩展区域中的违规行为。

自定义框架有两个组件： **API Surface** 和内 **容分类**。

#### API Surface {#api-surface}

在AEM的早期版本中，许多API都通过Uber Jar公开。 其中一些API并非旨在供客户使用，但是会跨捆绑套件提供对AEM功能的支持。 今后，Java API将标记为“公共”或“私有”，以向客户指示哪些API在升级环境中是安全的。 其他具体信息包括：

* 标为的Java API可 `Public` 以由自定义实施包使用和引用。

* 公共API将向后兼容于兼容性包的安装。
* 兼容性包中将包含一个兼容性Uber JAR，以确保向后兼容性
* 标记为的Java API `Private` 仅供AEM内部捆绑包使用，不应由自定义捆绑包使用。

>[!NOTE]
>
>在这种情 `Private` 况下 `Public` ，不应将Java的公共类和私人类的概念混为一谈。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 内容分类 {#content-classifications}

AEM长期以来一直使用叠加和Sling Resource Mergare的主体来允许客户扩展和自定义AEM功能。 为AEM控制台和UI提供支持的预定义功能存储在 **/libs中**。 客户永远不得修改 **/libs下的任何内容** ，但可以在/apps下添加其他内容以叠加和扩展 **/libs中定义的功能****** （有关详细信息，请参阅使用Overlays开发）。 这仍在将AEM升级为 **/libs中的内容时导致许多问题** ，因为这些问题可能会更改，从而导致叠加功能以意外方式中断。 客户还可以通过继承扩展AEM组 `sling:resourceSuperType`件，或直接通过sling:resourceType在 **/libs** 中引用组件。 类似的升级问题可能会通过引用和覆盖使用案例发生。

为了使客户更安全、更轻松地了解哪些 **/libs区域是安全的，并且****** /libs中的内容已通过以下混音进行了分类：

* **公共(granite:PublicArea)** -将节点定义为公共，以便它可以覆盖、继承( `sling:resourceSuperType`)或直接使用( `sling:resourceType`)。 在/libs下标为“公共”的节点下添加兼容性包后，升级将是安全的。 通常，客户只应利用标记为“公共”的节点。

* **摘要(granite:AbstractArea)** -将节点定义为摘要。 节点可以覆盖或继承( `sling:resourceSupertype`)，但不能直接使用( `sling:resourceType`)。

* **Final(granite:FinalArea)** -将节点定义为final。 分类为最终理想状态的节点不应被覆盖或继承。 最终节点可以直接通过使 `sling:resourceType`用。 默认情况下，最终节点下的子节点被视为内部节点。

* ***内部(granite:InternalArea)*** *- *将节点定义为内部。 归类为内部理想情况的节点不应被覆盖、继承或直接使用。 这些节点仅用于AEM的内部功能

* **无注释** -节点会基于树层次继承分类。 默认情况下，/ root为“公共”。 **父节点分类为“内部”或“最终”的节点也应视为“内部”。**

>[!NOTE]
>
>这些策略仅针对基于Sling搜索路径的机制实施。 客户端库 **等其他区域** /lib可能标记为 `Internal`，但仍可与标准clientlib包含一起使用。 在这些情况下，客户应继续遵守内部分类。

#### CRXDE Lite内容类型指示器 {#crxde-lite-content-type-indicators}

在CRXDE lite中应用的混音将显示标记为灰显的内容节 `INTERNAL` 点和树。 仅 `FINAL` 图标灰显。 这些节点的子项也将显示为灰色。 在这两种情况下，叠加节点功能都被禁用。

**公共**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**内部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**内容运行状况检查**

>[!NOTE]
>
>自AEM 6.5起，Adobe建议使用图案检测器检测内容访问违规。 模式检测器报告更加详细，检测问题更多，减少误报概率。
>
>有关详细信息，请参 [阅使用模式检测器评估升级复杂性](/help/sites-deploying/pattern-detector.md)。

AEM 6.5将附带运行状况检查，以提醒客户以与内容分类不符的方式使用覆盖或引用的内容。

** Sling/Granite内容访问检查**是一项新的运行状况检查，它监视存储库以查看客户代码在AEM中访问受保护的节点时是否错误。

这将扫描 **/应用程序** ，通常需要几秒钟才能完成。

要访问此新的运行状况检查，您需要执行以下操作：

1. 从AEM主屏幕中，导航到工具> **操作>运行状况报告**
1. 单击“ **Sling/Granite内容访问检查** ”，如下所示：

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

扫描完成后，受保护节点的最终用户将收到引用不当的警告列表：

![截屏-2018-2-5健康报告](assets/screenshot-2018-2-5healthreports.png)

修复违规后，将返回绿色状态：

![截屏-2018-2-5健康报告违规](assets/screenshot-2018-2-5healthreports-violations.png)

运行状况检查显示由后台服务收集的信息，每当跨所有Sling搜索路径使用叠加或资源类型时，后台服务会异步检查这些信息。 如果内容混音使用不正确，则报告违规。
