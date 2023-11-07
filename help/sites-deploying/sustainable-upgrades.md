---
title: 可持续升级
description: 了解Adobe Experience Manager 6.4中的可持续升级。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# 可持续升级{#sustainable-upgrades}

## Customization Framework {#customization-framework}

### 体系结构（功能/基础架构/内容/应用程序）  {#architecture-functional-infrastructure-content-application}

自定义框架功能旨在帮助减少代码（如API）或内容（如叠加图）的非可扩展区域中的违规，这些区域对升级不友好。

自定义框架包含两个组件： **API表面** 和 **内容分类**.

#### API表面 {#api-surface}

在Adobe Experience Manager (AEM)的早期版本中，许多API通过Uber Jar公开。 其中一些API并非打算供客户使用，而是公开支持各个捆绑包中的AEM功能。 今后，Java™ API将标记为“公用”或“专用”，以向客户指示在升级环境中可以安全使用哪些API。 其他具体包括：

* Java™ API标记为 `Public` 可供自定义实施捆绑包使用和引用。

* 公共API向后兼容兼容兼容包的安装。
* 兼容性包包含一个兼容性Uber JAR，以确保向后兼容性
* Java™ API标记为 `Private` 仅供AEM内部捆绑包使用，而不供自定义捆绑包使用。

>[!NOTE]
>
>的概念 `Private` 和 `Public` 在这种情况下，不应与Java™的公共和私有类的概念混淆。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 内容分类 {#content-classifications}

AEM长期以来使用叠加和Sling资源合并器的主体，允许客户扩展和自定义AEM功能。 为AEM控制台和UI提供支持的预定义功能存储在中 **/libs**. 客户绝不能修改下面的任何内容 **/libs** 但可以在下面添加其他内容 **/apps** 叠加和扩展中定义的功能 **/libs** （有关更多信息，请参阅使用叠加进行开发）。 在将AEM作为中的内容升级时，这仍会导致许多问题 **/libs** 可能会发生更改，从而导致覆盖功能以意外方式中断。 客户还可以通过继承以下方式扩展AEM组件： `sling:resourceSuperType`，或只是引用中的组件 **/libs** 直接通过sling：resourceType。 在引用和覆盖用例时，可能会出现类似的升级问题。

使客户更安全、更轻松地了解 **/libs** 可以安全使用并覆盖中的内容 **/libs** 已分类为以下mixin：

* **公共(granite：PublicArea)**  — 将节点定义为公共节点，以便可以覆盖、继承( `sling:resourceSuperType`)或直接使用( `sling:resourceType`)。 标记为Public的/libs下的节点可以安全升级，并且添加了兼容包。 通常，客户应仅使用标记为“公共”的节点。

* **摘要(granite：AbstractArea)**  — 将节点定义为抽象节点。 节点可以覆盖或继承( `sling:resourceSupertype`)，但不直接使用( `sling:resourceType`)。

* **最终(granite：FinalArea)**  — 将节点定义为最终节点。 最好分类为最终节点的节点不应覆盖或继承。 可通过以下方式直接使用最终节点 `sling:resourceType`. 默认情况下，最终节点下的子节点被视为内部节点。

* ***内部(granite：InternalArea)*** *- *将节点定义为内部节点。 理想情况下，分类为内部节点的节点不应重叠、继承或直接使用。 这些节点仅用于AEM的内部功能

* **无注释**  — 节点根据树层次结构继承分类。 /根默认为Public。 **将父节点分类为“内部”或“最终”的节点也将被视为“内部”节点。**

>[!NOTE]
>
这些策略仅针对基于Sling搜索路径的机制强制执行。 其他领域 **/libs** 例如，客户端库可以标记为 `Internal`，但仍可以与标准clientlib包含一起使用。 在这些情况下，客户必须继续遵守内部分类。

#### CRXDE Lite内容类型指示器 {#crxde-lite-content-type-indicators}

应用于CRXDE Lite的Mixin显示标记为的内容节点和树 `INTERNAL` 显示为灰色（灰显）。 对象 `FINAL`，则只有图标会变暗。 这些节点的子节点也显示为灰色。 在这两种情况下，都会禁用覆盖节点功能。

**公共**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最终**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**内部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**内容运行状况检查**

>[!NOTE]
>
从AEM 6.5开始，Adobe建议使用模式检测器来检测内容访问违规。 模式检测器报告更详细，检测更多问题，并降低误报概率。
>
有关更多信息，请参阅 [使用模式检测器评估升级复杂性](/help/sites-deploying/pattern-detector.md).

AEM 6.5附带运行状况检查，如果以与内容分类不一致的方式使用叠加或引用的内容，该检查会提醒客户。

** Sling/Granite Content Access Check**是一项新的运行状况检查，用于监视存储库以查看客户代码是否未正确访问AEM中的受保护节点。

此扫描 **/apps** 通常需要几秒钟才能完成。

要访问此新的运行状况检查，请执行以下操作：

1. 从AEM主屏幕，导航到 **工具>操作>运行状况报表**
1. 单击 **Sling/Granite内容访问检查**.

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

扫描完成后，将显示一个警告列表，通知最终用户未正确引用了受保护节点：

![屏幕快照–2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

修复违规后，它会返回到绿色状态：

![屏幕快照–2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

运行状况检查显示后台服务收集的信息，每当在所有Sling搜索路径上使用叠加或资源类型时，后台服务就会异步检查这些信息。 如果内容mixin使用不正确，它会报告冲突。
