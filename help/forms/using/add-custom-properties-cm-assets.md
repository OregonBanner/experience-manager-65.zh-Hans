---
title: 将自定义属性添加到通信管理资产
seo-title: Add custom properties to Correspondence Management assets
description: 了解如何将自定义属性添加到通信管理资产。
seo-description: Learn how to add custom properties to Correspondence Management assets.
uuid: 4716e181-d3ea-424b-9544-376cc649bce7
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79437b96-7b57-4581-b7e7-fcaedc3d05de
docset: aem65
feature: Correspondence Management
exl-id: ba2e145d-51ee-4844-a9e1-9927971d25a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4443'
ht-degree: 4%

---

# 将自定义属性添加到通信管理资产{#add-custom-properties-to-correspondence-management-assets}

## 概述 {#overview}

您可以自定义“通信管理”用户界面，并为用户提供量身定制的一组属性和选项卡。 此自定义包括向特定资源类型/字母或所有资源类型和字母添加自定义字段/属性和选项卡。

## 将自定义属性添加到通信管理资产 {#adding-custom-properties-to-correspondence-management-assets}

以下方案显示如何将属性/选项卡添加到通信管理资产和信件：

* 向所有资源类型添加公共属性
* 向所有资源类型添加通用选项卡
* 将自定义属性添加到特定资源类型

通过调整这些方案中的属性、路径和值，您可以根据自己的需求，将自定义属性和选项卡添加到不同的资产集。

### 方案：将公共字段（属性）添加到所有资源类型 {#scenario-adding-a-common-field-property-to-all-the-asset-types}

此场景显示如何将自定义属性添加到所有资产类型（文本、列表、条件和布局片段）和字母。 使用此方案，您可以将属性“收件人的位置”添加到所有资产和字母。 “收件人的位置”属性有助于确定资产或信件与哪个交付地理区域相关。

>[!NOTE]
>
>如果您已添加自定义属性，则该属性会开始显示在资源创建页面上。 要隐藏此类属性，请参阅在资产创建和属性页面上显示/隐藏自定义属性。

![已添加到所有资源类型的自定义属性](assets/lcoationofrecipientsui.png)

完成以下步骤以向所有资源类型和字母添加自定义属性：

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 在apps文件夹中，使用以下步骤创建一个名为css的文件夹，其路径/结构与css文件夹（位于crui文件夹中）类似：

   1. 右键单击以下路径的items文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![覆盖节点](assets/itemsoverlaynode.png)

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **位置：** /apps/

      **匹配节点类型：** 已选择

      ![覆盖节点](assets/cmmetapropertiesoverlaynode.png)

   1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

   1. 单击 **全部保存**.

1. 在新创建的项目文件夹下，使用以下步骤在所有资产（例如：GeoLocation）中为自定义属性添加一个节点：

   1. 右键单击项目文件夹并选择 **创建** > **创建节点**.

      ![在CRX中创建节点](assets/itemscreatenode.png)

   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 地理位置（或您要为此资产提供的名称）

      **类型：** nt：unstructured

      ![创建节点：地理位置](assets/geographicallocationcreatenode.png)

   1. 单击您已创建的新节点（此处为GeoLocation）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为GeoLocation）：

      | **名称** | **类型** | **值** |
      |---|---|---|
      | 字段标签 | 字符串 | 您要为字段/属性提供的名称。 （此处：收件人位置） |
      | name | 字符串 | `./extendedproperties/GeoLocation` （使值与在“项”节点下创建的字段名称相同） |
      | renderReadOnly | 布尔值 | true |
      | sling:resourceType | 字符串 | `granite/ui/components/coral/foundation/form/textfield` |

   1. 单击 **全部保存**.

1. 要查看您的自定义，请将鼠标悬停在资源（文本、列表、条件或布局片段）或信件上，请单击 **查看属性**，然后单击 **编辑**. 新字段（收件人位置）显示在资产/信件属性的“基本”选项卡中。

   >[!NOTE]
   >
   >您可能需要在UI中显示自定义设置之前清除浏览器缓存。

   ![已添加到所有资产的自定义属性](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >您添加的所有资产的公共属性都会显示在资产属性的基本选项卡中。 默认情况下，为所有资源添加的通用属性将显示在属性页面以及资源创建页面上。 要隐藏公共属性，您需要 <!--link to show / hide properties]-->.

### 方案：将自定义下拉列表和值添加到自定义属性/字段 {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

此方案显示如何将自定义属性添加到所有资源类型并向其中添加下拉值。

1. 右键单击以下路径的items文件夹并选择 **覆盖节点**：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. 在新创建的覆盖节点(/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items)下，为需要创建下拉列表的每个属性（字段）创建一个节点（此处） `geographicallocation`nt：unstructured类型的。
1. 将以下属性添加到节点（此处为geographicallocation），然后单击 **全部保存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>价值</strong></td>
   </tr>
   <tr>
      <td>字段标签</td>
      <td>字符串</td>
      <td>您要为字段/属性提供的名称。 （此处：地理分配）</td>
   </tr>
   <tr>
      <td>name</td>
      <td>字符串</td>
      <td>。/extendedproperties/geographicallocation（保持值与在items节点下创建的字段名称相同）</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>布尔值</td>
      <td>true</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>字符串</td>
      <td>granite/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. 在属性节点（此处为geographicallocation）下，添加名为的新节点 `items`. 在项节点下，为下拉列表中的值分别添加一个节点。 作为优秀实践，请将第一个节点添加为空白以用作下拉列表的默认值，并添加一个选项供用户指定该字段的不含值。 要添加多个选项/下拉值，请重复以下步骤：

   1. 右键单击资产节点（此处为geographicallocation）并选择 **创建** > **创建节点**.
   1. 输入字段名称作为 `item1,` 将文字保持为nt：unstructured，然后单击 **确定**.
   1. 将以下属性添加到新创建的节点（此处为item1），然后单击 **全部保存**：

      <table>
         <tbody>
         <tr>
          <td><strong>名称</strong></td>
          <td><strong>类型</strong></td>
          <td><strong>价值</strong></td>
         </tr>
         <tr>
          <td>text</td>
          <td>字符串</td>
          <td>这是用户可见的下拉选项的值。 将其保留为空则为空白（默认）值，或者输入值，例如 <strong>国际</strong> 或 <strong>在我们内部</strong>.<br /> </td>
         </tr>
         <tr>
          <td>值</td>
          <td>字符串</td>
          <td>存储在CRXDE中的文本值。 输入任意唯一关键字。 <br /> </td>
         </tr>
         </tbody>
   </table>

   ![自定义dropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

自定义下拉列表在资源属性中显示如下：

![drop-down_customization](assets/drop-down_customization.png)

### 方案：所有资源类型的“常用”选项卡 {#scenario-common-tab-for-all-asset-types}

此场景显示如何向所有资源类型（文本、列表、条件和布局片段）和字母添加自定义选项卡“收件人”。 在“收件人”选项卡中，您可以计划放置与收件人相关的所有自定义属性。

![为所有资源类型添加了自定义选项卡](assets/recipientstab.png)

使用以下过程，您可以向所有资源添加带有字段的选项卡：

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 在apps文件夹中，使用以下步骤创建一个名为cmmetadataproperties的文件夹，其路径/结构与cmmetadataproperties文件夹（位于内容文件夹中）类似：

   1. 右键单击以下路径的cmmetadataproperties文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![覆盖节点](assets/cmmetadatapropertiesoverlaynode.png)

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

      ![在CRX中创建的覆盖文件夹结构](assets/cmmetadatapropertiesappsfolder.png)

      单击 **全部保存**.

1. 在cmmetadataproperties文件夹下，添加一个节点，用于使用以下步骤为所有资产（例如：commontab）创建自定义选项卡：

   1. 右键单击cmmetadataproperties文件夹并选择 **创建** > **创建节点**.

      ![创建节点](assets/cmmetadatapropertiescreatenode.png)

   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** commontab（或您要为此属性提供的名称）

      **类型：** nt：unstructured

   1. 单击已创建的新节点（此处为commontab）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为commontab）：

      <table>
         <tbody>
         <tr>
          <td><strong>名称</strong></td>
          <td><strong>类型</strong></td>
          <td><strong>价值</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>字符串</td>
          <td>要为该列指定的名称。 （此处：收件人）</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>字符串</td>
          <td>granite/ui/components/coral/foundation/container<br /> </td>
   </tr>
         </tbody>
       </table>

   1. 单击 **全部保存**.

1. 对于在上一步中创建的选项卡节点（此处为commontab），请使用以下步骤创建一个名为item的节点：

   1. 右键单击相关节点（此处为“常用”选项卡）并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 个项目

      **类型：** nt：unstructured

   1. 单击 **全部保存：**

1. 在上一步创建的“项”节点（位于“commontab”下）中，使用以下步骤在“自定义”选项卡（位于“commontab”下）中添加用于创建列的节点（此处为“列1”）（要添加更多列，请重复此步骤）：

   1. 右键单击项目节点并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** Column1 （或您要为节点指定的名称 — 此名称不会显示在用户界面中。）

      **类型：** nt：unstructured

   1. 将以下属性添加到节点（此处为Column1），然后单击 **全部保存**：

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>价值</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字符串</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 在上一步中创建的节点（此处为Column1）中，使用以下步骤添加一个名为项的节点：

   1. 右键单击节点（此处为Column1）并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 个项目

      **类型：** nt：unstructured

   1. 单击 **全部保存**.

1. 要在自定义选项卡中创建字段（此处为“收件人”），请添加节点（此处为“地理位置”）。 此属性对应于您创建的列。 使用以下步骤创建字段（要创建更多字段/节点，请重复这些步骤。）: 

   1. 右键单击项目节点并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 地理位置（或字段属性的其他名称）

      **类型：** nt：unstructured

   1. 将以下属性添加到字段节点（此处为GeographicLocation），然后单击 **全部保存**.

      | **名称** | **类型** | **值** |
      |---|---|---|
      | 字段标签 | 字符串 | 收件人的位置（或您希望为字段提供的名称）。 |
      | name | 字符串 | 。/extendedproperties/GeographicLocation |
      | renderReadOnly | 布尔值 | true |
      | sling:resourceType | 字符串 | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. 要为信件添加此选项卡，请创建一个覆盖文件夹，其路径/结构类似于以下项目文件夹，路径如下：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   要为字母或其他资源创建叠加，请通过以下路径替换 [assettype] 包含文本、条件、列表、datadictionary或片段：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. 右键单击以下路径的items文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。将创建文件夹。 单击 **全部保存**.

1. 在新创建的项目文件夹中，为资源中的自定义选项卡（此处为mytab — 此名称未显示在用户界面中）添加一个节点，请执行以下步骤：

   1. 右键单击项目文件夹并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** mytab（或您要为此属性提供的名称）

      **类型：** nt：unstructured

   1. 单击已创建的新节点（此处为mytab）。 CRX显示节点的属性。
   1. 将以下两个属性添加到节点（此处为customtab）：

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>价值</strong></td>
         </tr>
         <tr>
           <td>路径<br /> </td>
           <td>字符串</td>
           <td>fd/cm/ma/gui/content/cmmetadataproperties/commontab<br /> </td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字符串</td>
           <td>granite/ui/components/coral/foundation/include<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 单击 **全部保存**.

1. 要查看您的自定义设置，请将鼠标悬停在相关资产（此处为字母）上，单击“查看属性”，然后单击 **编辑**. 新选项卡（收件人）和字段（收件人位置）将显示在用户界面中。

   >[!NOTE]
   >
   >您可能需要在UI中显示自定义设置之前清除浏览器缓存。

   ![添加到字母的自定义选项卡](assets/recipientstab-1.png)

### 方案：为特定资源类型添加自定义属性 {#scenario-adding-custom-properties-for-specific-asset-types}

此场景显示如何将属性添加到特定资源类型，例如为所有文本资源添加字段。 使用此过程，您可以将属性添加到以下项之一：

* 文本
* 条件
* 列表
* 布局片段
* 数据字典
* 书信

例如，只有文本资产需要添加属性“收件人的位置”，以标识资产相关的地理区域。  ![添加到资源的自定义属性](assets/newtabui.png)

要将属性添加到资源类型，请完成以下步骤：

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 要在资源类型（如文本）中创建选项卡，请在apps文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [资产类型] =文本、条件、列表、信件、数据字典或片段

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径的items文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      例如，如果要为文本资产创建属性，请选择以下文件夹：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![覆盖节点](assets/textitemstabsitemsoverlaynode1.png)

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[资产类型]/items/tab/items

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

      单击 **全部保存**.

1. 在新创建的项目文件夹中，使用以下步骤为资源中的自定义选项卡添加节点（例如： customtab）：

   1. 右键单击项目文件夹并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** customtab（或您要为此属性提供的名称）

      **类型：** nt：unstructured

   1. 单击已创建的新节点（此处为“自定义”选项卡）。 CRX显示节点的属性。
   1. 将以下两个属性添加到节点（此处为customtab）：

      | **名称** | **类型** | **值** |
      |---|---|---|
      | sling:resourceType | 字符串 | granite/ui/components/coral/foundation/container |
      | jcr:title | 字符串 | 用户界面上的字段名称（此处为“我的”选项卡） |

   1. 单击 **全部保存**.

1. 在上一步中创建的节点（此处为“自定义”选项卡）中，使用以下步骤添加一个名为项的节点：

   1. 右键单击节点（此处为“自定义”选项卡）并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 个项目

      **类型：** nt：unstructured

   1. 单击 **全部保存**.

1. 在上一步中创建的项节点（在“自定义”选项卡下）中，使用以下步骤在“自定义”选项卡中添加用于创建列的节点（此处为Column1）（要添加更多列，请重复此步骤）：

   1. 右键单击项目节点并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** Column1（或您要为节点提供的名称）

      **类型：** nt：unstructured

   1. 将以下属性添加到节点（此处为Column1），然后单击 **全部保存**.

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>价值</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字符串</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 对于您创建的每个列（如上一步中的Column1所指定），使用以下步骤创建一个名为item的节点：

   1. 右键单击相关的列节点（此处为Column1）并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 个项目

      **类型：** nt：unstructured

   1. 单击 **全部保存：**

1. 对于创建的每个列，在items节点下创建一个节点，以在用户界面的新选项卡中创建字段。 重复此步骤以在列中创建更多字段：

   1. 右键单击相关节点（此处为Column1下的项），然后选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 您选择的名称（此处为“地理位置”）

      **类型：** nt：unstructured

   1. 将以下属性添加到节点，然后单击 **全部保存**.

      | **名称** | **类型** | **值** |
      |---|---|---|
      | 字段标签 | 字符串 | 收件人的位置（或您希望为字段提供的名称）。 |
      | name | 字符串 | `./extendedproperties/GeoLocation` |
      | renderReadOnly | 布尔值 | true |
      | sling:resourceType | 字符串 | granite/ui/components/coral/foundation/form/textfield |

1. 要查看您的自定义设置，请将鼠标悬停在相关资产（此处为文本）上，单击“查看属性”，然后单击 **编辑**. 新选项卡和字段（收件人位置）将显示在用户界面中。

   >[!NOTE]
   >
   >您可能需要在UI中显示自定义设置之前清除浏览器缓存。

   ![添加到特定资源的自定义属性](assets/newtabui-1.png)

### 在资产创建页面上显示自定义属性 {#display-custom-properties-on-the-asset-creation-page}

默认情况下，添加到新选项卡的自定义属性仅在属性页面上可见，而在资产创建页面上不可见，因为资产创建页面没有选项卡布局。 要在资源创建页面上显示自定义属性以及其他属性，您需要执行以下操作：

1. 右键单击以下路径的items文件夹并选择 **覆盖节点**：

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 确保“覆盖节点”对话框具有以下字母值。 对于其他资源类型，路径如下表所示：

   **路径：** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr：content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items

   **位置：** /apps/

   **匹配节点类型：** 已选择

   根据资源类型，路径需要如下：

   | **资产/文档类型** | **要添加的路径** |
   |---|---|
   | 文本 | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr：content/body/items/form/items/textwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | 列表 | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr：content/body/items/form/items/listwizard/items/editproperties/items/properties/items/tables/items/tab1/items |
   | 条件 | /libs/fd/cm/ma/gui/content/createasset/createcondition/jcr：content/body/items/form/items/conditionwizard/items/editproperties/items/properties/items/tables/items/tab1/items |
   | 片段 | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr：content/body/items/form/items/fragmentwizard/items/properties/items/properties/items/tables2/items/tab1/items |
   | 书信 | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr：content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items |

1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

1. 在您创建的覆盖项节点下，创建一个名为col4（或任何其他名称）的节点，然后单击 **全部保存**.

   例如，下面是为字母创建的覆盖节点。

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 将以下属性添加到新创建的节点（此处为col4），然后单击 **全部保存**：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>价值</strong></td>
  </tr>
  <tr>
   <td>路径</td>
   <td>字符串</td>
   <td><p>此路径是指向在中创建的列的指针：</p>
    <ul>
     <li>对于所有资产类型的通用选项卡： /apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>适用于不同资产类型的不同属性： /apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tables/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字符串</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappearinginmainproperties](assets/customfieldappearinginmainproperties.png)

自定义属性、语言，显示在UI中用于创建书信

## 自定义列表视图以显示自定义属性 {#customize-the-list-view-to-show-custom-properties}

将自定义属性添加到通信管理资产后，您需要在CRX/DE中进行进一步更改，以确保自定义属性显示在通信管理UI中。

完成以下步骤以在通信管理的资产列表UI中显示自定义属性：

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 在apps文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径上的columns文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/lists/columns

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

      单击 **全部保存**.

1. 对于创建的每个属性，在列节点下创建一个节点，以在用户界面中创建列。 重复此步骤可在UI中创建更多列：

   1. 右键单击相关节点（列）并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 您选择的名称（此处为“地理位置”）

      **类型：** nt：unstructured

   1. 将以下属性添加到节点，然后单击 **全部保存**.

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>价值</strong></td>
         </tr>
         <tr>
           <td>jcr:primaryType</td>
           <td>名称</td>
           <td><p>nt:unstructured</p> </td>
         </tr>
         <tr>
           <td>jcr:title</td>
           <td>字符串</td>
           <td><p>地理位置</p> <p>此值在UI中显示为列标题。 </p> </td>
         </tr>
         <tr>
           <td>可排序</td>
           <td>布尔值</td>
           <td><p>true</p> <p>值为true表示用户可以对此列中的值进行排序。 </p> </td>
         </tr>
         </tbody>
       </table>

1. 在apps文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径上的columns文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

      单击 **全部保存**.

1. 从以下位置复制childlistpage.jsp文件：

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   将文件粘贴到以下位置：

   /apps//fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/。

1. 打开childlistpage.jsp文件(/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp)并进行以下更改：

   1. 将以下内容添加到文件的第19行（在版权声明之后）。

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. 将获取每个自定义属性的值的函数的以下代码添加到文件末尾：

      ```jsp
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. 在开始之前添加以下内容 &lt;tr> 标记(&lt;tr attrs.build=&quot;&quot;>>)：

      ```jsp
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      在代码中，“地理位置”是您在创建自定义节点/字段时在name属性中设置的值。 在创建自定义节点/字段时，您使用指定了属性的名称。/extendedproperties/前缀： 。/extendedproperties/GeoLocation. 在代码中，前缀不是必需的。

   1. 要在UI中显示新属性，请在结束tr (&lt;/tr>)标记：

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      要添加更多列，请重复步骤6.3和6.4。

   1. 单击 **全部保存**.

1. 要查看您的自定义，请打开文档片段或已添加自定义属性的字母的列表视图。

   对于所有资源类型，将显示在此过程中添加的UI列和属性。 但是，只能为您最初添加自定义属性的资产类型输入和显示这些属性中的值。

   例如，使用方案：为特定资源类型添加自定义属性将自定义属性添加到文本资源，您只能为文本资源输入自定义属性。 但是，如果您在UI中显示该自定义属性，则会为所有资源类型显示该列。

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. （可选）默认情况下，新列作为UI中的最后一列显示。 要使列显示在特定位置，请将以下属性添加到列节点：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>价值</strong></td>
  </tr>
  <tr>
   <td>sling：orderBefore</td>
   <td>字符串</td>
   <td><p>位于路径“/libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/list/columns”的列节点的名称，在该路径之前，自定义列需要显示在UI中。</p> <p>在本例中，如果您希望地理位置列显示在“版本”列之前（左侧），请将属性sling：orderBefore添加到位于路径“/apps/fd/cm/ma/gui/content/cmassets/jcr：content/views/list/columns/GeoLocation”的GeoLocation节点，并将属性的值设置为version。</p> </td>
  </tr>
 </tbody>
</table>

添加sling：orderBefore属性以指定列位置时，还需要更新对应项的顺序 &lt;td> 在此过程的步骤6.4中指定的标记。 例如，在这种情况下，您需要确保 &lt;td> “地理位置”标记放置在 &lt;td> “版本”列的标记：

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## 启用自定义属性搜索 {#enable-search-for-custom-properties}

默认情况下，全文搜索不包含您使用CRX/DE添加到UI的自定义属性。

要在搜索中包含自定义属性，您需要允许为自定义属性编制索引。

要允许为自定义属性编制索引，请完成以下步骤：

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 转到 `/oak:index/cmLucene`并添加名为的节点 **聚合** 在它下面。

   1. 右键单击cmLucene文件夹并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 聚合

      **类型：** nt：unstructured

   1. 单击 **全部保存**.

1. 在新创建的聚合文件夹下，添加节点cm：resource。 在cm：resource下，添加一个名为include0的节点。

   1. 右键单击聚合文件夹并选择 **创建** > **创建节点**. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** cm：resource

      **类型：** nt：unstructured

   1. 右键单击cm：resource文件夹并选择 **创建** > **创建节点**. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** include0

      **类型：** nt：unstructured

   1. 单击已创建的新节点（此处为include0）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为include0）：

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>价值</strong></td>
         </tr>
         <tr>
           <td>路径</td>
           <td>字符串</td>
           <td>extendedproperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 单击 **全部保存**.

1. 转到以下位置的属性并在其下添加节点位置： `/oak:index/cmLucene/indexRules/cm:resource/properties`

   对要添加到搜索的每个自定义属性重复此步骤。

   1. 右键单击属性文件夹并选择 **创建** > **创建节点**.
   1. 确保“创建节点”对话框具有以下值，然后单击 **确定**：

      **名称：** 位置（或要添加到搜索的自定义属性的名称）

      **类型：** nt：unstructured

   1. 单击已创建的新节点（此处为位置）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为位置）：

      | **名称** | **类型** | **值** |
      |---|---|---|
      | 已分析 | 字符串 | true |
      | name | 字符串 | extendedProperties/location（或要添加到搜索中的属性的名称） |
      | propertyIndex | 布尔值 | true |
      | useInSuggest | 布尔值 | true |

   1. 单击 **全部保存**.

1. 现在，您可以在全文搜索中使用自定义属性值来查找相关资产。

>[!NOTE]
>
>如果您仍然无法搜索，可能是因为索引问题。 对于重新索引，请转到以下节点并将属性“re-index”的值更改为true：
>
>/oak：index/cmLucene&quot; ，并更改属性的值

## 更改搜索页面的默认视图 {#change-default-view-of-the-search-page}

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 在apps文件夹中，创建一个名为list的文件夹，其路径/结构类似于位于/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views中的列表文件夹：

   1. 右键单击以下路径的items文件夹并选择 **覆盖节点**：

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

   1. 单击 **全部保存**.

1. 在新创建的节点列表，添加以下属性并单击 **全部保存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>价值</strong></td>
   </tr>
   <tr>
      <td>sling：orderBefore<br /> </td>
      <td>字符串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 自定义项会在列表视图中显示所有控制台(包括Forms和文档、Assets和Sites)的搜索结果。

## 更改资源页面的默认视图 {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>这些步骤会更改所有控制台(如Forms和文档、资源和站点)的默认视图。

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 在apps文件夹中，创建一个名为list的文件夹，其路径/结构类似于位于以下位置的列表文件夹：

   /libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/

   1. 右键单击以下路径的items文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/list

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构是在apps文件夹中创建的。

   1. 单击 **全部保存**.

1. 在新创建的节点列表，添加以下属性并单击 **全部保存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>价值</strong></td>
   </tr>
   <tr>
      <td>sling：orderBefore<br /> </td>
      <td>字符串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 清除浏览器Cookie或使用浏览器的无痕模式查看资产。 默认情况下，资源页面会显示在卡片布局中。

## 在资产创建和属性页面上显示/隐藏自定义属性 {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

要显示或隐藏自定义属性，请完成以下步骤：

1. 在自定义属性节点（如geographicallocation）下，创建一个名为“granite：rendercondition”、类型为“nt：unstructured”的新节点。
1. 将以下属性添加到节点并单击 **全部保存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>价值</strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>字符串</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. 要在资源创建页面上隐藏此属性，请将以下属性添加到该属性并单击 **全部保存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>价值</strong></td>
   </tr>
   <tr>
      <td>hideOncreate<br /> </td>
      <td>布尔值</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

1. 要在资产的属性页面上隐藏自定义属性，请将以下属性添加到其中，然后单击 **全部保存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>价值</strong></td>
   </tr>
   <tr>
      <td>隐藏编辑<br /> </td>
      <td>布尔值</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

   要再次显示值，请将属性值重置为 `false` 或删除属性条目。
