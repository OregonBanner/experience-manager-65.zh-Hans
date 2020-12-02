---
title: 识别要翻译的内容
seo-title: 识别要翻译的内容
description: 了解如何识别需要翻译的内容。
seo-description: 了解如何识别需要翻译的内容。
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---


# 标识要翻译的内容{#identifying-content-to-translate}

翻译规则可标识要翻译包含在翻译项目中或从中排除的页面、组件和资产的内容。 当页面或资产被翻译时，AEM会提取此内容，以便将其发送到翻译服务。

页面和资产在JCR存储库中表示为节点。 提取的内容是节点的一个或多个属性值。 翻译规则标识包含要提取的内容的属性。

翻译规则以XML格式表示，并存储在以下可能的位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

该文件适用于所有翻译项目。

>[!NOTE]
>
>升级到6.4后，建议将文件从/etc移动。 有关详细信息，请参阅AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)中的[公共存储库重组。

规则包括以下信息：

* 应用规则的节点的路径。 该规则也适用于节点的后代。
* 包含要翻译的内容的节点属性的名称。 该属性可以特定于特定资源类型或所有资源类型。

例如，您可以创建一个规则，该规则将作者添加的内容转换到您页面上的所有AEM foundation Text组件。 规则可以标识`/content`节点和`foundation/components/text`组件的`text`属性。

已添加一个[控制台](#translation-rules-ui)，用于配置转换规则。 UI中的定义将为您填充文件。

有关AEM中内容翻译功能的概述，请参阅[多语言站点内容翻译](/help/sites-administering/translation.md)。

>[!NOTE]
>
>AEM支持资源类型和引用属性之间的一对一映射，以转换页面上引用的内容。

## 页面、组件和资产的规则语法{#rule-syntax-for-pages-components-and-assets}

规则是`node`元素，其中包含一个或多个子元素`property`和零个或多个子元素`node`:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

这些`node`元素中的每个元素都具有以下特征：

* `path`属性包含规则所应用分支的根节点的路径。
* 子`property`元素标识要转换的所有资源类型的节点属性：

   * `name`属性包含属性名称。
   * 如果属性未转换，则可选的`translate`属性等于`false`。 默认情况下，该值为`true`。 此属性在覆盖以前的规则时很有用。

* 子`node`元素标识要转换的节点属性以用于特定资源类型：

   * `resourceType`属性包含解析到实现资源类型的组件的路径。
   * 子`property`元素标识要转换的节点属性。 以与节点规则的子`property`元素相同的方式使用此节点。

以下示例规则导致对`/content`节点下的所有页面转换所有`text`属性的内容。 该规则对于在`text`属性中存储内容的任何组件（如基础文本组件和基础图像组件）都有效。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下示例转换所有`text`属性的内容，还转换基础图像组件的其他属性。 如果其他组件具有同名属性，则规则不适用于这些组件。

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

## 从页面{#rule-syntax-for-extracting-assets-from-pages}提取资产的规则语法

使用以下规则语法包括嵌入在组件中或从组件引用的资产：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每个`assetNode`元素具有以下特性：

* 一个`resourceType`属性，它等于解析到组件的路径。
* 一个`assetReferenceAttribute`属性，它等于存储资产二进制文件（对于嵌入式资产）或引用资产路径的属性的名称。

以下示例从基础图像组件中提取图像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆盖规则{#overriding-rules}

translation_rules.xml文件由`nodelist`元素组成，其中包含多个子元素`node`。 AEM从上到下读取节点列表。 当多个规则目标同一节点时，将使用文件中较低的规则。 例如，以下规则导致除页面的`/content/mysite/en`分支外，`text`属性中的所有内容都要进行翻译：

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## 筛选属性{#filtering-properties}

可以使用`filter`元素过滤具有特定属性的节点。

例如，以下规则导致除属性`draft`设置为`true`的节点外，`text`属性中的所有内容都要进行转换。

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻译规则UI {#translation-rules-ui}

控制台也可用于配置翻译规则。

要访问它：

1. 导航到&#x200B;**工具**，然后导航到&#x200B;**常规**。

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. 选择&#x200B;**转换配置**。

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

从此处，您可以&#x200B;**添加上下文**。 这允许您添加路径。

![chlimage_1-57](assets/chlimage_1-57.jpeg)

然后，您需要选择上下文，然后单击&#x200B;**编辑**。 这将打开翻译规则编辑器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

您可以通过UI更改以下4个属性：`isDeep`、`inherit`、`translate`和`updateDestinationLanguage`。

**isDeep** 此属性适用于节点过滤器，默认情况下为true。它检查节点（或其祖先）是否包含筛选器中具有指定属性值的属性。 如果为false，则仅检查当前节点。

例如，子节点将添加到转换作业中，即使父节点将属性`draftOnly`设置为true来标记草稿内容。 此处`isDeep`开始播放，并检查父节点是否具有属性`draftOnly`作为true并排除这些子节点。

在编辑器中，可以选中／取消选中&#x200B;**过滤器**&#x200B;选项卡中的&#x200B;**深**。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下是在UI中未选中&#x200B;**Is Deep**&#x200B;时生成的xml的示例：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**继** 承这适用于属性。默认情况下，每个属性都是继承的，但如果您希望某些属性不在子项上继承，则可以将该属性标记为false，以便它仅应用于该特定节点。

在UI中，可以选中／取消选中&#x200B;**属性**&#x200B;选项卡中的&#x200B;**继承**。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**转** 换属性仅用于指定是否转换属性。

在UI中，可以选中／取消选中&#x200B;**属性**&#x200B;选项卡中的&#x200B;**转换**。

**updateDestinationLanguage** 此属性用于没有文本但语言代码的属性，例如jcr:language。用户不是在翻译文本，而是在从源到目标的语言区域设置。 此类属性不会发送以进行翻译。

在UI中，您可以在&#x200B;**属性**&#x200B;选项卡中选中／取消选中&#x200B;**转换**，但对于具有语言代码作为值的特定属性。

为了帮助阐明`updateDestinationLanguage`和`translate`之间的区别，以下是仅包含两个规则的上下文的一个简单示例：

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml中的结果将如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手动编辑规则文件{#editing-the-rules-file-manually}

随AEM一起安装的translation_rules.xml文件包含一组默认的转换规则。 您可以编辑文件以支持翻译项目的要求。 例如，您可以添加规则，以便转换自定义组件的内容。

如果编辑translation_rules.xml文件，请在内容包中保留一个备份副本。 安装AEM service pack或重新安装某些AEM包可以将当前translation_rules.xml文件替换为原始文件。 要在这种情况下恢复规则，可以安装包含备份副本的包。

>[!NOTE]
>
>创建内容包后，每次编辑文件时都重新构建该包。

## 翻译规则文件示例{#example-translation-rules-file}

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

