---
title: 标识要翻译的内容
seo-title: Identifying Content to Translate
description: 瞭解如何識別需要翻譯的內容。
seo-description: Learn how to identify content that needs translating.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 66%

---

# 标识要翻译的内容{#identifying-content-to-translate}

翻译规则为翻译项目中包含或排除的页面、组件和资产标识要翻译的内容。在翻译页面或资产时，AEM 会提取此内容，以便将其发送到翻译服务。

页面和资产在 JCR 存储库中表示为节点。提取的内容是节点的一个或多个属性值。翻譯規則會識別包含要擷取之內容的屬性。

翻译规则以 XML 格式表示，并且可能存储在以下位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

该文件应用于所有翻译项目。

>[!NOTE]
>
>升級至6.4後，建議從/etc移動檔案。 另請參閱 [AEM 6.5中的常見存放庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) 以取得更多詳細資料。

规则包含以下信息：

* 规则应用于的节点的路径。规则也应用于节点的子级。
* 包含要翻译的内容的节点属性的名称。属性可以特定于某个特定的资源类型或所有资源类型。

例如，您可以建立規則來轉譯作者新增至您頁面上所有AEM Foundation Text元件的內容。 此规则可以标识 `foundation/components/text` 组件的 `/content` 节点和 `text` 属性。

已添加一个可用于配置翻译规则的[控制台](#translation-rules-ui)。UI 中的定义将为您填充文件。

有关 AEM 中内容翻译功能的概述，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)。

>[!NOTE]
>
>AEM 支持资源类型和引用属性之间的一对一映射，以便翻译页面上的引用内容。

## 页面、组件和资产的规则语法 {#rule-syntax-for-pages-components-and-assets}

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

以下示例规则导致为 `/content` 节点下的所有页面翻译所有 `text` 属性的内容。此規則適用於任何將內容儲存在 `text` 屬性，例如foundation Text元件和foundation Image元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下範例會轉譯所有 `text` 屬性，也會轉譯foundation Image元件的其他屬性。 如果其他组件具有同名属性，则该规则不适用于它们。

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

## 用于从页面提取资产的规则语法  {#rule-syntax-for-extracting-assets-from-pages}

使用以下规则语法可包含嵌入在组件中或从组件中引用的资产：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每个 `assetNode` 元素均具有以下特性：

* 一个 `resourceType` 属性，代表解析为组件的路径。
* 一个 `assetReferenceAttribute` 属性，代表存储资产二进制文件（用于嵌入资产）的属性的名称或引用资产的路径.

下列範例會從foundation Image元件中擷取影像：

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 覆盖规则 {#overriding-rules}

translation_rules.xml檔案包含 `nodelist` 具有多個子項的元素 `node` 元素。 AEM 从上到下读取节点列表。如果有多个规则针对同一节点，则使用文件中较低位置的规则。例如，以下规则导致翻译 `text` 属性中的所有内容，但页面的 `/content/mysite/en` 分支除外：

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

從這裡，您可以 **新增內容**. 這可讓您新增路徑。

![chlimage_1-57](assets/chlimage_1-57.jpeg)

之后，您需要选择上下文，然后单击&#x200B;**编辑**。该操作将打开翻译规则编辑器。

![chlimage_1-58](assets/chlimage_1-58.jpeg)

您可透過UI變更下列4個屬性： `isDeep`， `inherit`， `translate` 和 `updateDestinationLanguage`.

**isDeep** 此屬性適用於節點篩選器，預設為true。 它检查节点（或其祖先）是否在过滤器中包含具有指定属性值的属性。如果为 false，则仅检查当前节点。

例如，即使父節點具有屬性，子節點也會新增到翻譯作業中 `draftOnly` 設為true可標幟草稿內容。 此时 `isDeep` 将发挥作用，并检查父节点是否已将属性 `draftOnly` 设置为 true 并排除这些子节点。

在編輯器中，您可以核取/取消核取 **深入** 在 **篩選器** 標籤。

![chlimage_1-59](assets/chlimage_1-59.jpeg)

以下範例是產生以下專案的xml： **深入** 未在UI中勾選：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**繼承** 這適用於屬性。 依預設，每個屬性都會被繼承，但如果您不想讓某個屬性在子項上被繼承，則可以將該屬性標示為false，以便只將該屬性套用到該特定節點。

在 UI 中，您可以在&#x200B;**属性**&#x200B;选项卡中选中/取消选中 **Inherit**。

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**轉換** translate屬性僅用於指定是否翻譯屬性。

在 UI 中，您可以在&#x200B;**属性**&#x200B;选项卡中选中/取消选中 **Translate**。

**updateDestinationLanguage** 此屬性用於沒有文字但有語言代碼的屬性，例如jcr：language。 用户不会翻译文本，而是进行从源到目标的语言区域设置。不会发送此类属性进行翻译。

在UI中，您可以勾選/取消勾選 **轉換** 在 **屬性** 標籤，但用於以語言程式碼為值的特定屬性。

为了帮助阐明 `updateDestinationLanguage` 和 `translate` 之间的区别，以下提供了仅具有两个规则的上下文的简单示例：

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml 中的结果将如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手动编辑规则文件 {#editing-the-rules-file-manually}

與AEM一起安裝的translation_rules.xml檔案包含一組預設的翻譯規則。 您可以编辑该文件以支持翻译项目的要求。例如，您可以添加规则以翻译自定义组件的内容。

如果您編輯translation_rules.xml檔案，請在內容封裝中保留備份復本。 安裝AEM Service Pack或重新安裝某些AEM套件可將目前的translation_rules.xml檔案取代為原始檔案。 要在此情况下恢复您的规则，您可以安装包含备份副本的包。

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
