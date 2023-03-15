---
title: 可持续升级
seo-title: Sustainable Upgrades
description: 了解AEM 6.4中的可持续升级。
seo-description: Learn about sustainable upgrades in AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# 可持续升级{#sustainable-upgrades}

## 自定义框架 {#customization-framework}

### 体系结构（功能/基础架构/内容/应用程序）  {#architecture-functional-infrastructure-content-application}

Customization Framework功能旨在帮助减少代码（如API）或内容（如叠加图）的非可扩展区域中对升级不友好的违规。

自定义框架有两个组件： **API表面** 和 **内容分类**.

#### API表面 {#api-surface}

在AEM的早期版本中，许多API通过Uber Jar公开。 其中一些API不是为了供客户使用，而是为了支持捆绑包中的AEM功能。 今后，Java API将标记为“公用”或“专用”，以向客户指示在升级环境中可以安全使用哪些API。 其他具体包括：

* Java API标记为 `Public` 可供自定义实施捆绑包使用和引用。

* 公共API将向后兼容兼容兼容包的安装。
* 兼容性包将包含兼容性Uber JAR，以确保向后兼容性
* Java API标记为 `Private` 仅供AEM内部捆绑包使用，不应由自定义捆绑包使用。

>[!NOTE]
>
>的概念 `Private` 和 `Public` 在这种情况下，不应混淆于Java的公共类和私有类的概念。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 内容分类 {#content-classifications}

长期以来，AEM一直使用叠加和Sling资源合并器的主体来允许客户扩展和自定义AEM功能。 为AEM控制台和UI提供支持的预定义功能存储在中 **/libs**. 客户绝不能修改下面的任何内容 **/libs** 但可以在下添加其他内容 **/apps** 叠加和扩展中定义的功能 **/libs** （有关更多信息，请参阅使用叠加进行开发）。 在将AEM作为中的内容升级时，这仍会导致许多问题 **/libs** 可能会发生更改，从而导致叠加功能以意外方式中断。 客户还可以通过以下方式通过继承来扩展AEM组件 `sling:resourceSuperType`，或只是引用中的组件 **/libs** 直接通过sling：resourceType。 引用和覆盖用例可能会出现类似的升级问题。

为了让客户更安全、更轻松地了解 **/libs** 可以安全地使用和叠加中的内容 **/libs** 已分类为以下mixin：

* **公共(granite：PublicArea)**  — 将节点定义为公共节点，以便可以覆盖、继承( `sling:resourceSuperType`)或直接使用( `sling:resourceType`)。 标记为Public的/libs下的节点可以安全升级，并添加兼容包。 通常，客户应仅利用标记为“公共”的节点。

* **摘要(granite：AbstractArea)**  — 将节点定义为抽象节点。 节点可以覆盖或继承( `sling:resourceSupertype`)，但不能直接使用( `sling:resourceType`)。

* **最终(granite：FinalArea)**  — 将节点定义为最终节点。 最好分类为最终节点的节点不应覆盖或继承。 可通过以下方式直接使用最终节点 `sling:resourceType`. 默认情况下，最终节点下的子节点被视为内部节点。

* ***内部(granite：InternalArea)*** *- *将节点定义为内部节点。 最好分类为内部节点的节点不应被覆盖、继承或直接使用。 这些节点仅用于AEM的内部功能

* **无注释**  — 节点根据树层次结构继承分类。 /根默认为Public。 **父项被分类为“内部”或“最终”的节点也将被视为“内部”节点。**

>[!NOTE]
>
>这些策略仅针对基于Sling搜索路径的机制执行。 其他领域 **/libs** 类似于客户端库，可标记为 `Internal`，但仍可以与标准clientlib包含一起使用。 在这些情况下，客户应继续遵守内部分类，这一点很重要。

#### CRXDE Lite内容类型指示器 {#crxde-lite-content-type-indicators}

应用于CRXDE Lite的Mixin将显示标记为的内容节点和树 `INTERNAL` 显示为灰色。 对象 `FINAL` 只有图标呈灰显状态。 这些节点的子项也将显示为灰色。 在这两种情况下，“覆盖节点”功能都将被禁用。

**公共**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最终**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**内部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**内容运行状况检查**

>[!NOTE]
>
>从AEM 6.5开始，Adobe建议使用模式检测器来检测内容访问违规。 模式检测器报告更详细，可检测更多问题并降低误报概率。
>
>有关更多信息，请参阅 [使用模式检测器评估升级复杂性](/help/sites-deploying/pattern-detector.md).

AEM 6.5将随附运行状况检查，如果覆盖或引用的内容的使用方式与内容分类不一致，该检查将提醒客户。

** Sling/Granite Content Access Check**是一种新的运行状况检查，可监视存储库以查看客户代码是否未正确访问AEM中的受保护节点。

这将扫描 **/apps** 通常需要几秒钟才能完成。

要访问此新的运行状况检查，您需要执行以下操作：

1. 从AEM主屏幕，导航到 **工具>操作>运行状况报表**
1. 单击 **Sling/Granite内容访问检查** 如下所示：

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

扫描完成后，将显示一个警告列表，通知最终用户未正确引用了受保护的节点：

![屏幕快照–2018-2-5运行状况报告](assets/screenshot-2018-2-5healthreports.png)

修复违规后，它将返回到绿色状态：

![屏幕快照–2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

运行状况检查显示后台服务收集的信息，每当在所有Sling搜索路径上使用叠加或资源类型时，后台服务就会异步检查这些信息。 如果内容mixin使用不正确，它会报告违规。
