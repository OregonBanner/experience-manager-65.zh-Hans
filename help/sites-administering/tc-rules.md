---
title: 标识要翻译的内容
description: 了解如何识别需要在Adobe Experience Manager中翻译的内容。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 66%

---

# 标识要翻译的内容{#identifying-content-to-translate}

翻译规则为翻译项目中包含或排除的页面、组件和资源标识要翻译的内容。在翻译页面或资源时，AEM 会提取此内容，以便将其发送到翻译服务。

页面和资源在 JCR 存储库中表示为节点。提取的内容是节点的一个或多个属性值。翻译规则标识包含要提取的内容的属性。

翻译规则以 XML 格式表示，并且可能存储在以下位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

该文件应用于所有翻译项目。

>[!NOTE]
>
>升级到6.4后，建议从/etc移动文件。 请参阅 [AEM 6.5中的常见存储库重组](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) 以了解更多详细信息。

规则包含以下信息：

* 规则应用于的节点的路径。规则也应用于节点的子级。
* 包含要翻译的内容的节点属性的名称。属性可以特定于某个特定的资源类型或所有资源类型。

例如，您可以创建一个规则来翻译作者添加到您页面上所有AEM Foundation文本组件的内容。 此规则可以标识 `foundation/components/text` 组件的 `/content` 节点和 `text` 属性。

已添加一个可用于配置翻译规则的[控制台](#translation-rules-ui)。UI 中的定义将为您填充文件。

有关 AEM 中内容翻译功能的概述，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)。

>[!NOTE]
>
>AEM 支持资源类型和引用属性之间的一对一映射，以便翻译页面上的引用内容。

## 页面、组件和资源的规则语法 {#rule-syntax-for-pages-components-and-assets}

规则是一个 `node` 元素，它包含一个或多个子 `property` 元素以及零个或多个子 `node` 元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

其中每个 `node` 元素均具有以下特性：

* `path` 属性包含应用规则的分支的根节点的路径。
* 子 `property` 元素为所有资源类型标识要翻译的节点属性：

   * `name` 属性包含属性名。
   * 可选 `translate` 属性等于 `false`（如果该属性未翻译）。默认情况下，该值为 `true`。在覆盖以前的规则时，此属性很有用。

* 子 `node` 元素为特定资源类型标识要翻译的节点属性：

   * `resourceType` 属性包含解析为实施资源类型的组件的路径。
   * 子 `property` 元素标识要翻译的节点属性。按照与节点规则的子 `property` 元素相同的方式使用此节点。

以下示例规则导致为 `/content` 节点下的所有页面翻译所有 `text` 属性的内容。该规则适用于任何将内容存储在中的组件。 `text` 属性，如foundation文本组件和foundation图像组件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下示例翻译了所有 `text` 属性，并翻译foundation图像组件的其他属性。 如果其他组件具有同名属性，则该规则不适用于它们。

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="foundation/components/textimage">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## 用于从页面提取资源的规则语法  {#rule-syntax-for-extracting-assets-from-pages}

使用以下规则语法可包含嵌入在组件中或从组件中引用的资源：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每个 `assetNode` 元素均具有以下特性：

* 一个 `resourceType` 属性，代表解析为组件的路径。
* 一个 `assetReferenceAttribute` 属性，代表存储资源二进制文件（用于嵌入资源）的属性的名称或引用资源的路径.

以下示例从foundation图像组件中提取图像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆盖规则 {#overriding-rules}

translation_rules.xml文件包含 `nodelist` 带多个子项的元素 `node` 元素。 AEM 从上到下读取节点列表。如果有多个规则针对同一节点，则使用文件中较低位置的规则。例如，以下规则导致翻译 `text` 属性中的所有内容，但页面的 `/content/mysite/en` 分支除外：

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## 筛选属性 {#filtering-properties}

您可以使用 `filter` 元素筛选具有特定属性的节点。

例如，以下规则导致翻译 `text` 属性中的所有内容，但属性 `draft` 设置为 `true` 的节点除外。

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻译规则 UI {#translation-rules-ui}

控制台也可用于配置翻译规则。

要访问它，请执行以下操作：

1. 依次导航到&#x200B;**工具**&#x200B;和&#x200B;**常规**。

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. 选择&#x200B;**翻译配置**。

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

从这里，您可以 **添加上下文**. 这允许您添加路径。

![chlimage_1-57](assets/chlimage_1-57.jpeg)

之后，您需要选择上下文，然后单击&#x200B;**编辑**。该操作将打开翻译规则编辑器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

您可以通过用户界面更改以下4个属性： `isDeep`， `inherit`， `translate` 和 `updateDestinationLanguage`.

**isDeep** 此属性适用于节点过滤器，默认情况下为true。 它检查节点（或其祖先）是否在过滤器中包含具有指定属性值的属性。如果为 false，则仅检查当前节点。

例如，即使父节点具有属性，子节点也会添加到翻译作业中 `draftOnly` 设置为true可标记草稿内容。 此时 `isDeep` 将发挥作用，并检查父节点是否已将属性 `draftOnly` 设置为 true 并排除这些子节点。

在编辑器中，您可以选中/取消选中 **深** 在 **过滤器** 选项卡。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下是以下情况下生成的xml的示例 **深** 未在UI中选中：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**inherit** 这适用于属性。 默认情况下，每个属性都会被继承，但如果您希望某个属性不在子项上继承，则可以将该属性标记为false，以便仅将该属性应用于该特定节点。

在 UI 中，您可以在&#x200B;**属性**&#x200B;选项卡中选中/取消选中 **Inherit**。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**translate** translate属性仅用于指定是否翻译属性。

在 UI 中，您可以在&#x200B;**属性**&#x200B;选项卡中选中/取消选中 **Translate**。

**updatedestinationlanguage** 此属性用于没有文本但有语言代码的属性，例如jcr：language。 用户不会翻译文本，而是进行从源到目标的语言区域设置。不会发送此类属性进行翻译。

在UI中，您可以选中/取消选中 **Translate** 在 **属性** 选项卡，但适用于将语言代码作为值的特定属性。

为了帮助阐明 `updateDestinationLanguage` 和 `translate` 之间的区别，以下提供了仅具有两个规则的上下文的简单示例：

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml 中的结果将如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手动编辑规则文件 {#editing-the-rules-file-manually}

随AEM一起安装的translation_rules.xml文件包含一组默认的翻译规则。 您可以编辑该文件以支持翻译项目的要求。例如，您可以添加规则以翻译自定义组件的内容。

如果编辑translation_rules.xml文件，请在内容包中保留备份副本。 安装AEM Service Pack或重新安装某些AEM包可将当前translation_rules.xml文件替换为原始文件。 要在此情况下恢复您的规则，您可以安装包含备份副本的包。

>[!NOTE]
>
>创建内容包后，每次编辑文件时都会重新构建包。

## 示例翻译规则文件 {#example-translation-rules-file}

```xml
<nodelist>
    <!-- translation rules for Geometrixx Demo site (example) -->
    <node path="/content/geometrixx">
        <!-- list all node properties that should be translated -->
        <property name="jcr:title" /> <!-- translation workflows running on content saved in /content/geometrixx, will extract jcr:title values independent of the component. -->
        <property name="jcr:description" />
        <node resourceType ="foundation/components/image"> <!-- translation workflows running on content saved in /content/geometrixx, will extract alternateText values only for Image component. -->
            <property name="alternateText"/>
        </node>
        <node resourceType ="geometrixx/components/title">
            <property name="richText"/>
            <property name="jcr:title" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract jcr:title for Title component, but instead use richText. -->
        </node>
        <node pathContains="/cq:annotations">
            <property name="text" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract text if part of cq:annotations node. -->
        </node>
    </node>
    <!-- translation rules for Geometrixx Outdoors site (example) -->
    <node path="/content/geometrixx-outdoors">
        <node resourceType ="foundation/components/image">
            <property name="alternateText"/>
            <property name="jcr:title" />
        </node>
        <node resourceType ="geometrixx-outdoors/components/title">
            <property name="richText"/>
        </node>
    </node>
    <!-- translation rules for ASSETS (example) -->
    <node path="/content/dam">
        <!-- configure list of metadata properties here -->
        <property name="dc:title" />
        <property name="dc:description" />
    </node>
    <!-- translation rules for extracting ASSETS from SITES content, configure all components that embed or reference assets -->
    <assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/video" assetReferenceAttribute="asset"/>
    <assetNode resourceType="foundation/components/download" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/mobileimage" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="wcm/foundation/components/image" assetReferenceAttribute="fileReference"/>
</nodelist>
```
