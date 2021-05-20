---
title: 将自定义属性添加到通信管理资产
seo-title: 将自定义属性添加到通信管理资产
description: 了解如何将自定义属性添加到通信管理资产。
seo-description: 了解如何将自定义属性添加到通信管理资产。
uuid: 4716e181-d3ea-424b-9544-376cc649bce7
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79437b96-7b57-4581-b7e7-fcaedc3d05de
docset: aem65
feature: 通信管理
exl-id: ba2e145d-51ee-4844-a9e1-9927971d25a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4462'
ht-degree: 4%

---

# 将自定义属性添加到通信管理资产{#add-custom-properties-to-correspondence-management-assets}

## 概述 {#overview}

您可以自定义通信管理用户界面，并向用户显示一组定制的属性和选项卡。 此自定义设置包括向特定资产类型/字母或所有资产类型和字母添加自定义字段/属性和选项卡。

## 向通信管理资产{#adding-custom-properties-to-correspondence-management-assets}添加自定义属性

以下方案显示了如何向通信管理资产和信件添加属性/选项卡：

* 向所有资产类型添加通用属性
* 为所有资产类型添加通用选项卡
* 向特定资产类型添加自定义属性

通过调整这些情景中的属性、路径和值，您可以根据需要将自定义属性和选项卡添加到不同的资产集中。

### 方案：向所有资产类型{#scenario-adding-a-common-field-property-to-all-the-asset-types}添加公用字段（属性）

此方案显示如何向所有资产类型（文本、列表、条件和布局片段）和字母添加自定义属性。 使用此方案，您可以向所有资产和信件中添加属性“收件人的位置”。 收件人的位置属性有助于确定资产或信件交付的地理区域与之相关。

>[!NOTE]
>
>如果已添加自定义属性，则资产创建页面上会开始显示该属性。 要隐藏此类属性，请参阅在资产创建和属性页面上显示/隐藏自定义属性。

![自定义属性已添加到所有资产类型](assets/lcoationofrecipientsui.png)

完成以下步骤以向所有资产类型和字母添加自定义属性：

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，使用以下步骤创建一个名为css的文件夹，其路径/结构与css文件夹（位于ccrui文件夹中）类似：

   1. 右键单击以下路径中的项目文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![覆盖节点](assets/itemsoverlaynode.png)

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **位置：** /apps/

      **匹配节点类型：** 已选定

      ![覆盖节点](assets/cmmetapropertiesoverlaynode.png)

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

   1. 单击&#x200B;**Save All**。

1. 在新创建的项目文件夹下，为所有资产中的自定义属性添加一个节点(示例：GeoLocation)执行以下步骤：

   1. 右键单击项目文件夹并选择&#x200B;**创建** > **创建节点**。

      ![在CRX中创建节点](assets/itemscreatenode.png)

   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** GeoLocation（或要为此资产提供的名称）

      **类型：** nt:unstructured

      ![创建节点：地理位置](assets/geographicallocationcreatenode.png)

   1. 单击您创建的新节点（此处为GeoLocation）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为GeoLocation）：

      | **名称** | **类型** | **值** |
      |---|---|---|
      | fieldLabel | 字符串 | 要为字段/属性指定的名称。 (此处：收件人位置) |
      | name | 字符串 | `./extendedproperties/GeoLocation` （保留值与您在项目节点下创建的字段名称相同） |
      | renderReadOnly | 布尔型 | true |
      | sling:resourceType | 字符串 | `granite/ui/components/coral/foundation/form/textfield` |

   1. 单击&#x200B;**Save All**。

1. 要查看自定义设置，请将鼠标悬停在资产（文本、列表、条件或布局片段）或信件上，单击&#x200B;**查看属性**，然后单击&#x200B;**编辑**。 新字段（收件人的位置）会显示在资产/信件属性的“基本”选项卡中。

   >[!NOTE]
   >
   >在UI中显示自定义设置之前，您可能需要清除浏览器缓存。

   ![自定义属性已添加到所有资产](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >您添加的所有资产的通用属性都会显示在资产属性的基本选项卡中。 默认情况下，为所有资产添加的通用属性会显示在属性页面和资产创建页面上。 要隐藏常用属性，您需要<!--link to show / hide properties]-->。

### 方案：向自定义属性/字段{#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}添加自定义下拉列表和值

此方案显示了如何向所有资产类型添加自定义属性，以及向其添加下拉值。

1. 右键单击以下路径中的项目文件夹，然后选择&#x200B;**覆盖节点**:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. 在新创建的叠加节点下(/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items)
为需要为其创建nt:unstructured类型下拉列表（此处为`geographicallocation`）的每个属性（字段）创建一个节点。
1. 将以下属性添加到节点（此处为“地理分配”），然后单击&#x200B;**Save All**:

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>fieldLabel</td>
      <td>字符串</td>
      <td>要为字段/属性指定的名称。 (此处：地理分配)</td>
   </tr>
   <tr>
      <td>name</td>
      <td>字符串</td>
      <td>./extendedproperties/geographicallocation（保留值与在“项目”节点下创建的字段名称相同）</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>布尔型</td>
      <td>true</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>字符串</td>
      <td>granite/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. 在属性节点（此处为“地理分配”）下，添加一个名为`items`的新节点。 在“项目”节点下，为下拉列表中的值分别添加一个节点。 最佳做法是将第一个节点添加为空白，以用作下拉菜单的默认值，并为用户提供一个选项以指定字段的任何值。 要添加多个选项/下拉值，请重复以下步骤：

   1. 右键单击属性节点（此处为“地理分配”），然后选择&#x200B;**创建** > **创建节点**。
   1. 输入字段名称(`item1,`)，将类型保留为nt:unstructured，然后单击&#x200B;**OK**。
   1. 将以下属性添加到新创建的节点（此处为项目1），然后单击&#x200B;**Save All**:

      <table>
         <tbody>
         <tr>
          <td><strong>名称</strong></td>
          <td><strong>类型</strong></td>
          <td><strong>值</strong></td>
         </tr>
         <tr>
          <td>文本</td>
          <td>字符串</td>
          <td>这是用户可见的下拉选项的值。 将其留空（默认）值，或输入值，如<strong>International</strong>或<strong>Within US</strong>.<br /> </td>
         </tr>
         <tr>
          <td>选定</td>
          <td>字符串</td>
          <td>存储在CRXDE中的文本值。 输入任何唯一关键词。<br /> </td>
         </tr>
         </tbody>
   </table>

   ![customizationdropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

自定义下拉列表在资产属性中如下所示：

![drop_down_customization](assets/drop-down_customization.png)

### 方案：所有资产类型{#scenario-common-tab-for-all-asset-types}的“常用”选项卡

此方案显示如何向所有资产类型（文本、列表、条件和布局片段）和字母添加自定义选项卡“收件人”。 在“收件人”选项卡中，您可以计划放置与收件人相关的所有自定义属性。

![为所有资产类型添加了自定义选项卡](assets/recipientstab.png)

按照以下过程，您可以向所有资产添加包含字段的选项卡：

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，使用以下步骤创建一个名为cmmetadataproperties的文件夹，其路径/结构与cmmetadataproperties文件夹（位于内容文件夹中）类似：

   1. 右键单击以下路径中的cmmetadataproperties文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![覆盖节点](assets/cmmetadatapropertiesoverlaynode.png)

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **位置：** /apps/

      **匹配节点类型：** 已选定

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

      ![在CRX中创建的叠加文件夹结构](assets/cmmetadatapropertiesappsfolder.png)

      单击&#x200B;**Save All**。

1. 在cmmetadataproperties文件夹下，添加一个节点，用于为所有资产创建自定义选项卡(示例：（常用选项卡）执行以下步骤：

   1. 右键单击cmmetadataproperties文件夹，然后选择&#x200B;**创建** > **创建节点**。

      ![创建节点](assets/cmmetadatapropertiescreatenode.png)

   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** commontab（或要为此资产提供的名称）

      **类型：** nt:unstructured

   1. 单击您创建的新节点（此处为“常用”选项卡）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为“常用”选项卡）：

      <table>
         <tbody>
         <tr>
          <td><strong>名称</strong></td>
          <td><strong>类型</strong></td>
          <td><strong>值</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>字符串</td>
          <td>要为列指定的名称。 (此处：收件人)</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>字符串</td>
          <td>granite/ui/components/coral/foundation/container<br /> </td>
   </tr>
         </tbody>
       </table>

   1. 单击&#x200B;**Save All**。

1. 对于在最后一步中创建的选项卡节点（此处为“常用”选项卡），请使用以下步骤创建一个名为“项目”的节点：

   1. 右键单击相关节点（此处为“常用”选项卡），然后选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 项目

      **类型：** nt:unstructured

   1. 单击&#x200B;**全部保存：**

1. 在上一步中创建的“项目”节点（在“公用”选项卡下）中，使用以下步骤（要添加更多列，请重复此步骤），在“自定义”选项卡（“公用”选项卡）中添加用于创建列的节点（此处为“列1”）：

   1. 右键单击项目节点并选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** Column1（或要为节点提供的名称 — 此名称不会显示在用户界面中。）

      **类型：** nt:unstructured

   1. 将以下属性添加到节点（此处为Column1），然后单击&#x200B;**Save All**:

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字符串</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 在上一步中创建的节点（此处为Column1）中，使用以下步骤添加一个名为“项目”的节点：

   1. 右键单击节点（此处为Column1），然后选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 项目

      **类型：** nt:unstructured

   1. 单击&#x200B;**Save All**。

1. 要在自定义选项卡（此处为“收件人”）中创建字段，请添加节点（此处为“地理位置”）。 此属性对应于您创建的列。 使用以下步骤创建字段（要创建更多字段/节点，请重复这些步骤。）: 

   1. 右键单击项目节点并选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** GeoricalLocation（或字段属性的其他名称）

      **类型：** nt:unstructured

   1. 将以下属性添加到字段节点（此处为GeoralLocation），然后单击&#x200B;**Save All**。

      | **名称** | **类型** | **值** |
      |---|---|---|
      | fieldLabel | 字符串 | 收件人的位置（或要为字段指定的名称）。 |
      | name | 字符串 | ./extendedproperties/GeographicLocation |
      | renderReadOnly | 布尔型 | true |
      | sling:resourceType | 字符串 | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. 要为“信件”添加此选项卡，请在以下路径中创建一个路径/结构与以下项目文件夹类似的叠加文件夹：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   要为字母或其他资产创建叠加，请使用以下路径：将[assettype]替换为文本、条件、列表、数据字典或片段：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. 右键单击以下路径中的项目文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **位置：** /apps/

      **匹配节点类型：** 已选定

   1. 单击&#x200B;**确定**。随即会创建文件夹。 单击&#x200B;**Save All**。

1. 在新创建的“项目”文件夹中，使用以下步骤在资产中为自定义选项卡添加节点（此处为mytab — 此名称不显示在用户界面中）：

   1. 右键单击项目文件夹并选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** mytab（或要为此资产提供的名称）

      **类型：** nt:unstructured

   1. 单击您创建的新节点（此处为mytab）。 CRX显示节点的属性。
   1. 将以下两个属性添加到节点（此处为customtab）：

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>值</strong></td>
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

   1. 单击&#x200B;**Save All**。

1. 要查看自定义设置，请将鼠标悬停在相关资产（此处为信件）上，单击查看属性，然后单击&#x200B;**编辑**。 用户界面中会显示新的选项卡（收件人）和字段（收件人的位置）。

   >[!NOTE]
   >
   >在UI中显示自定义设置之前，您可能需要清除浏览器缓存。

   ![自定义选项卡已添加到字母](assets/recipientstab-1.png)

### 方案：为特定资产类型{#scenario-adding-custom-properties-for-specific-asset-types}添加自定义属性

此方案显示了如何向特定资产类型添加资产，例如向所有文本资产添加字段。 使用此过程，您可以向以下任一位置添加属性：

* 文本
* 条件
* 列表
* 布局片段
* 数据字典
* 书信

例如，仅对文本资产，您需要添加一个属性“收件人位置”来标识资产与哪个地理区域相关。  ![已向资产添加自定义属性](assets/newtabui.png)

要向资产类型添加资产，请完成以下步骤：

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 要在资产类型（如文本）中创建选项卡，请在应用程序文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [AssetType]  = text、condition、list、letter、datictionary或fragment

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径中的项目文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      例如，如果要为文本资产创建属性，请选择以下文件夹：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![覆盖节点](assets/textitemstabsitemsoverlaynode1.png)

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items

      **位置：** /apps/

      **匹配节点类型：** 已选定

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

      单击&#x200B;**Save All**。

1. 在新创建的项目文件夹中，为资产的自定义选项卡添加一个节点(示例：customtab)执行以下步骤：

   1. 右键单击项目文件夹并选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** customtab（或要为此资产提供的名称）

      **类型：** nt:unstructured

   1. 单击您创建的新节点（此处为“自定义”选项卡）。 CRX显示节点的属性。
   1. 将以下两个属性添加到节点（此处为customtab）：

      | **名称** | **类型** | **值** |
      |---|---|---|
      | sling:resourceType | 字符串 | granite/ui/components/coral/foundation/container |
      | jcr:title | 字符串 | 用户界面上的字段名称（此处为“我的”选项卡） |

   1. 单击&#x200B;**Save All**。

1. 在上一步中创建的节点（此处为“自定义”选项卡）中，使用以下步骤添加一个名为“项目”的节点：

   1. 右键单击节点（此处为“自定义”选项卡），然后选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 项目

      **类型：** nt:unstructured

   1. 单击&#x200B;**Save All**。

1. 在上一步中创建的项目节点（在customtab下）中，使用以下步骤（要添加更多列，请重复此步骤），在自定义选项卡中添加用于创建列的节点（此处为Column1）：

   1. 右键单击项目节点并选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** Column1（或要为节点提供的名称）

      **类型：** nt:unstructured

   1. 将以下属性添加到节点（此处为Column1），然后单击&#x200B;**Save All**。

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字符串</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 对于您创建的每列（如上一步中指定的 — 此处为Column1），请使用以下步骤创建一个名为item的节点：

   1. 右键单击相关列节点（此处为Column1），然后选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 项目

      **类型：** nt:unstructured

   1. 单击&#x200B;**全部保存：**

1. 对于创建的每个列，在“项目”节点下创建一个节点，用于在用户界面的新选项卡中创建字段。 重复此步骤以在列中创建更多字段：

   1. 右键单击相关节点（此处项目位于Column1下），然后选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 您选择的名称（此处为GeoLocation）

      **类型：** nt:unstructured

   1. 将以下属性添加到节点，然后单击&#x200B;**Save All**。

      | **名称** | **类型** | **值** |
      |---|---|---|
      | fieldLabel | 字符串 | 收件人的位置（或要为字段指定的名称）。 |
      | name | 字符串 | `./extendedproperties/GeoLocation` |
      | renderReadOnly | 布尔型 | true |
      | sling:resourceType | 字符串 | granite/ui/components/coral/foundation/form/textfield |

1. 要查看自定义设置，请将鼠标悬停在相关资产（此处为文本）上，单击查看属性，然后单击&#x200B;**编辑**。 用户界面中会显示新的选项卡和字段（收件人的位置）。

   >[!NOTE]
   >
   >在UI中显示自定义设置之前，您可能需要清除浏览器缓存。

   ![自定义属性已添加到特定资产](assets/newtabui-1.png)

### 在资产创建页面{#display-custom-properties-on-the-asset-creation-page}上显示自定义属性

默认情况下，添加到新选项卡的自定义属性仅在属性页面上可见，而在资产创建页面上则不可见，因为资产创建页面没有选项卡布局。 要在资产创建页面上显示自定义属性以及其他属性，您需要执行以下操作：

1. 右键单击以下路径中的项目文件夹，然后选择&#x200B;**覆盖节点**:

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 对于字母，请确保“覆盖节点”对话框具有以下值。 对于其他资产类型，下表提供了路径：

   **路径：** /libs/fd/cm/ma/gui/content/createasset/createter/jcr:content/body/items/form/items/letterWizard/items/properties/properties/items/letterproperties/items

   **位置：** /apps/

   **匹配节点类型：** 已选定

   根据资产类型，路径需要为：

   | **资产/文档类型** | **要添加的路径** |
   |---|---|
   | 文本 | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr:content/body/items/form/items/textwizard/items/editproperties/items/properties/tabs/items/tab1/items |
   | 列表 | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr:content/body/items/form/items/listwizard/items/editproperties/items/properties/tabs/items/tab1/items |
   | 条件 | /libs/fd/cm/ma/gui/content/createasset/createcondition/jcr:content/body/items/form/items/conditionwizard/items/editproperties/items/properties/tabs/items/tab1/items |
   | 片段 | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr:content/body/items/form/items/fragmentwizard/items/properties/properties/items/tabs2/items/tab1/items |
   | 书信 | /libs/fd/cm/ma/gui/content/createasset/createteletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items/letterproperties/items |

1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

1. 在您创建的覆盖项目节点下，创建名称为col4（或任何其他名称）的节点，然后单击&#x200B;**Save All**。

   例如，下面是为字母创建的覆盖节点。

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 将以下属性添加到新创建的节点（此处为col4），然后单击&#x200B;**Save All**:

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>路径</td>
   <td>字符串</td>
   <td><p>此路径是指向在中创建的列的指针：</p>
    <ul>
     <li>对于所有资产类型的常用选项卡：/apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>对于不同资产类型的不同属性：/apps/fd/cm/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字符串</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldapperinginmainproperties](assets/customfieldappearinginmainproperties.png)

自定义属性语言，显示在用于创建信件的UI中

## 自定义列表视图以显示自定义属性{#customize-the-list-view-to-show-custom-properties}

在向通信管理资产中添加自定义属性后，您需要在CRX/DE中进行进一步的更改，以确保自定义属性显示在通信管理UI中。

完成以下步骤以在通信管理的资产列表UI中显示自定义属性：

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在应用程序文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径的列文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns

      **位置：** /apps/

      **匹配节点类型：** 已选定

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

      单击&#x200B;**Save All**。

1. 对于创建的每个属性，在列节点下创建一个节点，以在用户界面中创建列。 重复此步骤以在UI中创建更多列：

   1. 右键单击相关节点（列）并选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 您选择的名称（此处为GeoralLocation）

      **类型：** nt:unstructured

   1. 将以下属性添加到节点，然后单击&#x200B;**Save All**。

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>值</strong></td>
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
           <td>布尔型</td>
           <td><p>true</p> <p>值为true表示用户可以对此列中的值进行排序。 </p> </td>
         </tr>
         </tbody>
       </table>

1. 在应用程序文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径的列文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage

      **位置：** /apps/

      **匹配节点类型：** 已选定

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

      单击&#x200B;**Save All**。

1. 从以下位置复制childlistpage.jsp文件：

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   将文件粘贴到以下位置：

   /apps//fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/。

1. 打开childlistpage.jsp文件(/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp)并进行以下更改：

   1. 将以下内容添加到文件的第19行（在copyright语句之后）。

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. 将获取每个自定义属性值的函数的以下代码添加到文件末尾：

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

   1. 在&lt;tr>标记(&lt;tr &lt;%= attrs.build()%>>)的开始之前添加以下内容：

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

      在代码中， GeoLocation是您在创建自定义节点/字段时在name属性中设置的值。 在创建自定义节点/字段时，您使用指定属性的名称。/extendedproperties/前缀：./extendedproperties/GeoLocation。 在代码中，前缀不是必需的。

   1. 要在UI中显示新属性，请在结束tr(&lt;/tr>)标记之前添加TD标记，如下所示：

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      要添加更多列，请重复步骤6.3和6.4。

   1. 单击&#x200B;**Save All**。

1. 要查看自定义设置，请打开文档片段或在其中添加了自定义属性的信件的列表视图。

   此时会为所有资产类型显示在此过程中添加的UI列和属性。 但是，这些属性中的值只能为最初为其添加自定义属性的资产类型输入和显示。

   例如，使用方案：为您向文本资产添加自定义属性的特定资产类型添加自定义属性时，您只能为文本资产输入自定义属性。 但是，如果您在UI中显示该自定义属性，则列将显示所有资产类型。

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. （可选）默认情况下，新列在UI中显示为最后一列。 要使列显示在特定位置，请将以下属性添加到列节点：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>sling:orderBefore</td>
   <td>字符串</td>
   <td><p>路径“/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns”的列节点名称，自定义列需要在UI中显示之前。</p> <p>在此，如果您希望“地理位置”列显示在“版本”列的前面（左侧），请将属性sling:orderBefore添加到路径为“”/apps/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns/GeoLocation”的“地理位置”节点，并将属性值设置为“版本”。</p> </td>
  </tr>
 </tbody>
</table>

当您添加sling:orderBefore属性以指定列位置时，还需要更新在此过程的步骤6.4中指定的相应&lt;td>标记的顺序。 例如，在这种情况下，您需要确保地理位置的&lt;td>标记放在版本列的&lt;td>标记之前：

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## 启用对自定义属性的搜索{#enable-search-for-custom-properties}

默认情况下，全文搜索不包括您使用CRX/DE添加到UI中的自定义属性。

要在搜索中包含自定义属性，您需要允许为自定义属性添加索引。

要允许索引自定义属性，请完成以下步骤：

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 转到`/oak:index/cmLucene`并在其下添加一个名为&#x200B;**aggregates**&#x200B;的节点。

   1. 右键单击cmLucene文件夹，然后选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 聚合

      **类型：** nt:unstructured

   1. 单击&#x200B;**Save All**。

1. 在新创建的聚合文件夹下，添加节点cm:resource。 在cm:resource下，添加一个名为include0的节点。

   1. 右键单击聚合文件夹，然后选择&#x200B;**创建** > **创建节点**。 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** cm:resource

      **类型：** nt:unstructured

   1. 右键单击cm:resource文件夹并选择&#x200B;**创建** > **创建节点**。 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** include0

      **类型：** nt:unstructured

   1. 单击已创建的新节点（此处为include0）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为include0）：

      <table>
         <tbody>
         <tr>
           <td><strong>名称</strong></td>
           <td><strong>类型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>路径</td>
           <td>字符串</td>
           <td>extendedProperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 单击&#x200B;**Save All**。

1. 转到以下位置的属性，并在其下添加节点位置：`/oak:index/cmLucene/indexRules/cm:resource/properties`

   对要添加到搜索的每个自定义属性重复此步骤。

   1. 右键单击属性文件夹并选择&#x200B;**创建** > **创建节点**。
   1. 确保“创建节点”对话框具有以下值，然后单击&#x200B;**OK**:

      **名称：** 位置（或要添加到搜索的自定义属性的名称）

      **类型：** nt:unstructured

   1. 单击已创建的新节点（此处为位置）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为位置）：

      | **名称** | **类型** | **值** |
      |---|---|---|
      | 分析 | 字符串 | true |
      | name | 字符串 | extendedProperties/location（或要添加到搜索的属性的名称） |
      | propertyIndex | 布尔型 | true |
      | useInSowket | 布尔型 | true |

   1. 单击&#x200B;**Save All**。

1. 现在，您可以在全文搜索中使用自定义属性值来查找相关资产。

>[!NOTE]
>
>如果您仍然无法搜索，则可能是因为索引问题。 要重新编入索引，请转到以下节点，并将属性“re-index”的值更改为true:
>
>/oak:index/cmLucene”和属性的更改值

## 更改搜索页面的默认视图{#change-default-view-of-the-search-page}

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，创建一个名为list的文件夹，其路径/结构与位于/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views中的列表文件夹类似：

   1. 右键单击以下路径中的项目文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **位置：** /apps/

      **匹配节点类型：** 已选定

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

   1. 单击&#x200B;**Save All**。

1. 在新创建的节点列表中，添加以下属性，然后单击&#x200B;**Save All**:

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>字符串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 自定义设置会在“列表”视图中显示所有控制台的搜索结果，包括“Forms”和“文档”、“资产”和“站点”。

## 更改资产页面的默认视图{#change-default-view-of-the-assets-page}

>[!NOTE]
>
>这些步骤会更改所有控制台(如“Forms”和“文档”、“资产”和“站点”)的默认视图。

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，创建一个名为list的文件夹，其路径/结构与位于以下位置的列表文件夹类似：

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/

   1. 右键单击以下路径中的项目文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list

      **位置：** /apps/

      **匹配节点类型：** 已选定

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

   1. 单击&#x200B;**Save All**。

1. 在新创建的节点列表中，添加以下属性，然后单击&#x200B;**Save All**:

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>字符串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 清除浏览器Cookie或使用浏览器的隐身模式查看资产。 默认情况下，资产页面会显示在卡片布局中。

## 在资产创建和属性页面{#show-hide-custom-properties-on-asset-creation-and-properties-pages}中显示/隐藏自定义属性

要显示或隐藏自定义属性，请完成以下步骤：

1. 在自定义属性节点（如地理分配）下，创建一个名为“granite:rendercondition”且类型为“nt:unstructured”的新节点。
1. 将以下属性添加到节点，然后单击&#x200B;**Save All**:

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>字符串</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. 要在资产创建页面中隐藏此属性，请向其添加以下属性，然后单击&#x200B;**全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>hideOnCreate<br /> </td>
      <td>布尔型</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

1. 要在资产的属性页面上隐藏自定义属性，请向其添加以下属性，然后单击&#x200B;**全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名称</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>hideOnEdit<br /> </td>
      <td>布尔型</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

   要再次显示值，请将属性值重置为`false`或删除属性条目。
