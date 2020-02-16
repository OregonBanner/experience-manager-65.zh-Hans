---
title: 将自定义属性添加到Correportence Management资产
seo-title: 将自定义属性添加到Correportence Management资产
description: 了解如何向Correponse Management资产添加自定义属性。
seo-description: 了解如何向Correponse Management资产添加自定义属性。
uuid: 4716e181-d3ea-424b-9544-376cc649bce7
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79437b96-7b57-4581-b7e7-fcaedc3d05de
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 将自定义属性添加到Correportence Management资产{#add-custom-properties-to-correspondence-management-assets}

## 概述 {#overview}

您可以自定义Correponsement Management用户界面，并为用户提供一组定制的属性和选项卡。 此自定义包括向特定资产类型／字母或所有资产类型和字母添加自定义字段／属性和选项卡。

## 将自定义属性添加到Correponse Management资产 {#adding-custom-properties-to-correspondence-management-assets}

以下场景显示了如何向Correptence Management资产和信函添加属性／选项卡：

* 向所有资产类型添加公用属性
* 向所有资产类型添加公用选项卡
* 向特定资产类型添加自定义属性

通过调整这些场景中的属性、路径和值，您可以根据需要向不同的资产集添加自定义属性和选项卡。

### 场景：向所有资产类型添加公用字段（属性） {#scenario-adding-a-common-field-property-to-all-the-asset-types}

此方案显示如何将自定义属性添加到所有资产类型（文本、列表、条件和布局片段）和字母中。 使用此方案，您可以向所有资产和字母添加一个属性“收件人的位置”。 收件人位置属性有助于确定资产或信函的交付地理区域。

>[!NOTE]
>
>如果已添加自定义属性，则该属性将开始显示在资产创建页面上。 要隐藏此类属性，请参阅在资产创建和属性页面上显示／隐藏自定义属性。

![自定义属性已添加到所有资产类型](assets/lcoationofrecipientsui.png)

完成以下步骤，向所有资产类型和字母添加自定义属性：

1. 转到并 `https://[server]:[port]/[ContextPath]/crx/de` 以管理员身份登录。
1. 在apps文件夹中，使用以下步骤创建一个名为css的文件夹，其路径／结构与css文件夹（位于ccrui文件夹中）类似：

   1. 右键单击以下路径中的项目文件夹，然后选择“叠 **加节点”**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![叠加节点](assets/itemsoverlaynode.png)

   1. 确保“叠加节点”对话框具有以下值：

      **** 路径：/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **** 位置：/apps/

      **** 匹配节点类型：已选择

      ![叠加节点](assets/cmmetapropertiesoverlaynode.png)

   1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

   1. 单击“ **全部保存**”。

1. 在新创建的项目文件夹下，为所有资产中的自定义属性添加一个节点(示例：GeoLocation)，执行以下步骤：

   1. 右键单击项目文件夹，然后选择“ **创建** ”>“ **创建节点”**。

      ![在CRX中创建节点](assets/itemscreatenode.png)

   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：GeoLocation（或要为此属性提供的名称）

      **** 类型：nt:unstructured

      ![创建节点：GeoLocation](assets/geographicallocationcreatenode.png)

   1. 单击您创建的新节点（此处为GeoLocation）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为GeoLocation）:

      | **名称** | **类型** | **值** |
      |---|---|---|
      | fieldLabel | 字符串 | 要为字段／属性指定的名称。 (此处：收件人位置) |
      | 名称 | 字符串 | `./extendedproperties/GeoLocation` （保留值与您在项目节点下创建的字段名称相同） |
      | renderReadOnly | 布尔型 | true |
      | sling:resourceType | 字符串 | `granite/ui/components/coral/foundation/form/textfield` |

   1. 单击“ **全部保存**”。

1. 要查看自定义，请将指针悬停在资产（文本、列表、条件或布局片段）或字母上，单击“查 **看属性**”，然后单击“ **编辑”**。 新字段（收件人的位置）显示在资产／信函属性的“基本”选项卡中。

   >[!NOTE]
   >
   >在UI中显示自定义之前，您可能需要清除浏览器缓存。

   ![自定义属性已添加到所有资产](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >您添加的所有资产的通用属性显示在资产属性的基本选项卡中。 默认情况下，为所有资产添加的公用属性显示在属性页面和资产创建页面上。 要隐藏常用属性，您需要 <!--link to show / hide properties]-->。

### 场景：向自定义属性／字段添加自定义下拉列表和值 {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

此方案显示如何向所有资产类型添加自定义属性并向其添加下拉值。

1. 右键单击以下路径中的项目文件夹，然后选择“叠 **加节点”**:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. 在新创建的叠加节点(/apps/fd/cm/ma/gui/content/cmetaproperties/commonataproperties/col1/items)下，为需要为其创建nt:unstructured类型下拉框(此处 `geographicallocation`)的每个属性（字段）创建一个节点。
1. 将以下属性添加到节点（此处为地理分配），然后单击“全 **部保存”**:

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
      <td>要为字段／属性指定的名称。 (此处：地理分配)</td>
   </tr>
   <tr>
      <td>名称</td>
      <td>字符串</td>
      <td>./extendedproperties/geographicallocation（使值与您在项目节点下创建的字段名保持相同）</td>
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

1. 在属性节点（此处为地理分配）下，添加一个名称为新节点 `items`。 在项节点下，为下拉框中的值分别添加一个节点。 作为一种最佳实践，将第一个节点添加为空白，以用作下拉框的默认值，并为用户指定字段的无值选项。 要添加多个选项／下拉值，请重复以下步骤：

   1. 右键单击属性节点（此处为地理分配），然后选择“创 **建** ”>“ **创建节点”**。
   1. 输入字段名称，将类型保 `item1,` 留为nt:unstructured，然后单击“确 **定”**。
   1. 将以下属性添加到新创建的节点（此处为item1），然后单击“全 **部保存”**:

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
          <td>这是用户可见的下拉选项的值。 将其留空（默认）值或输入值，如 <strong>International</strong> 或 <strong>Within US</strong>。<br /> </td>
         </tr>
         <tr>
          <td>value</td>
          <td>字符串</td>
          <td>存储在CRXDE中的文本值。 输入任意唯一关键字。 <br /> </td>
         </tr>
         </tbody>
   </table>

   ![自定义dropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

自定义下拉列表在资产属性中显示如下：

![drop_down_customization](assets/drop-down_customization.png)

### 场景：所有资产类型的公用选项卡 {#scenario-common-tab-for-all-asset-types}

此方案显示如何将自定义选项卡“收件人”添加到所有资产类型（文本、列表、条件和布局片段）和字母中。 在“收件人”选项卡中，您可以计划放置与收件人相关的所有自定义属性。

![为所有资产类型添加的自定义选项卡](assets/recipientstab.png)

使用以下过程，您可以向所有资产添加包含字段的选项卡：

1. 转到并 `https://[server]:[port]/[ContextPath]/crx/de` 以管理员身份登录。
1. 在apps文件夹中，使用以下步骤创建一个名为cmmetadataproperties的文件夹，其路径／结构与cmmetadataproperties文件夹（位于内容文件夹中）类似：

   1. 右键单击以下路径中的cmmetadataproperties文件夹，然后选择“ **叠加节点”**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![叠加节点](assets/cmmetadatapropertiesoverlaynode.png)

   1. 确保“叠加节点”对话框具有以下值：

      **** 路径：/libs/fd/cm/ma/gui/content/cmmetadataproperties

      **** 位置：/apps/

      **** 匹配节点类型：已选择

   1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

      ![在CRX中创建的叠加文件夹结构](assets/cmmetadatapropertiesappsfolder.png)

      单击“ **全部保存**”。

1. 在cmmetadataproperties文件夹下，添加一个节点，用于为所有资产创建自定义选项卡(示例：（公用选项卡）:

   1. 右键单击cmetadataproperties文件夹，然后选择 **创建** >创 **建节点**。

      ![创建节点](assets/cmmetadatapropertiescreatenode.png)

   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：commontab（或要为此属性提供的名称）

      **** 类型：nt:unstructured

   1. 单击您创建的新节点（此处为公用选项卡）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处为公用选项卡）:

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

   1. 单击“ **全部保存**”。

1. 对于在上一步（此处为公用选项卡）中创建的选项卡节点，请使用以下步骤创建一个名为item的节点：

   1. 右键单击相关节点（此处为公用选项卡），然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：项目

      **** 类型：nt:unstructured

   1. 单击“ **全部保存”:**

1. 在上一步中创建的项目节点（公用选项卡下）中，使用以下步骤在自定义选项卡（公用选项卡）中添加一个用于创建列的节点（此处为列1）（要添加更多列，请重复此步骤）:

   1. 右键单击项目节点，然后选择“创 **建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：Column1（或要为节点提供的名称——此名称不显示在用户界面中。）

      **** 类型：nt:unstructured

   1. 将以下属性添加到节点（此处为Column1），然后单击“全 **部保存”**:

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

1. 在您在上一步（此处为Column1）中创建的节点中，使用以下步骤添加一个名为items的节点：

   1. 右键单击节点（此处为Column1），然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：项目

      **** 类型：nt:unstructured

   1. 单击“ **全部保存**”。

1. 要在自定义选项卡（此处为收件人）中创建字段，请添加一个节点（此处为GeoralicLocation）。 此属性与您创建的列相对应。 使用以下步骤创建字段（要创建更多字段／节点，请重复这些步骤。）: 

   1. 右键单击项目节点，然后选择“创 **建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：GeoralicationLocation（或字段属性的其他名称）

      **** 类型：nt:unstructured

   1. 将以下属性添加到字段节点（此处为GeographicalLocation），然后单击“全 **部保存”**。

      | **名称** | **类型** | **值** |
      |---|---|---|
      | fieldLabel | 字符串 | 收件人的位置（或要为字段指定的名称）。 |
      | 名称 | 字符串 | ./extendedproperties/GeoralLocation |
      | renderReadOnly | 布尔型 | true |
      | sling:resourceType | 字符串 | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. 要为“字母”添加此选项卡，请在以下路径中创建一个路径／结构的叠加文件夹，该文件夹类似于以下项目文件夹：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   要为字母或其他资产创建叠加，请使用以下路径，方法是将资 [产类型替换为文本] 、条件、列表、dataditionary或片段：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. 右键单击以下路径中的项目文件夹，然后选择“叠 **加节点”**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. 确保“叠加节点”对话框具有以下值：

      **路径:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **** 位置：/apps/

      **** 匹配节点类型：已选择

   1. 单击&#x200B;**确定**。文件夹已创建。 单击“ **全部保存**”。

1. 在新创建的项目文件夹中，使用以下步骤为资产中的自定义选项卡添加一个节点（此处为mytab —— 此名称不显示在用户界面中）:

   1. 右键单击项目文件夹，然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：mytab（或要为此属性提供的名称）

      **** 类型：nt:unstructured

   1. 单击您创建的新节点（此处为mytab）。 CRX显示节点的属性。
   1. 将以下两个属性添加到节点（此处为自定义选项卡）:

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

   1. 单击“ **全部保存**”。

1. 要查看自定义，请将指针悬停在相关资产（此处为字母）上，单击查看属性，然后单击 **编辑**。 新选项卡（收件人）和字段（收件人的位置）显示在用户界面中。

   >[!NOTE]
   >
   >在UI中显示自定义之前，您可能需要清除浏览器缓存。

   ![添加到字母的自定义选项卡](assets/recipientstab-1.png)

### 场景：为特定资产类型添加自定义属性 {#scenario-adding-custom-properties-for-specific-asset-types}

此方案显示如何将属性添加到特定资产类型，如向所有文本资产添加字段。 使用此过程，您可以向以下任一位置添加属性：

* 文本
* 条件
* 列表
* 布局片段
* 数据字典
* 书信

例如，您只要向文本资产添加属性“收件人位置”，以标识资产与哪个地理区域相关。  ![向资产添加的自定义属性](assets/newtabui.png)

要向资产类型添加属性，请完成以下步骤：

1. 转到并 `https://[server]:[port]/[ContextPath]/crx/de` 以管理员身份登录。
1. 要在资产类型（如文本）中创建选项卡，请在应用程序文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [AssetType] =文本、条件、列表、字母、dataditionary或片段

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径中的项目文件夹，然后选择“叠 **加节点”**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      例如，如果要为文本资产创建属性，请选择以下文件夹：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![叠加节点](assets/textitemstabsitemsoverlaynode1.png)

   1. 确保“叠加节点”对话框具有以下值：

      **** 路径：/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items

      **** 位置：/apps/

      **** 匹配节点类型：已选择

   1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

      单击“ **全部保存**”。

1. 在新创建的项目文件夹中，为资产中的自定义选项卡添加一个节点(示例：customtab)。

   1. 右键单击项目文件夹，然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：customtab（或要为此属性提供的名称）

      **** 类型：nt:unstructured

   1. 单击您创建的新节点（此处为自定义选项卡）。 CRX显示节点的属性。
   1. 将以下两个属性添加到节点（此处为自定义选项卡）:

      | **名称** | **类型** | **值** |
      |---|---|---|
      | sling:resourceType | 字符串 | granite/ui/components/coral/foundation/container |
      | jcr:title | 字符串 | 用户界面上字段的名称（此处为“我的”选项卡） |

   1. 单击“ **全部保存**”。

1. 在您在上一步中创建的节点（此处为自定义选项卡）中，使用以下步骤添加一个名为items的节点：

   1. 右键单击节点（此处为自定义选项卡），然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：项目

      **** 类型：nt:unstructured

   1. 单击“ **全部保存**”。

1. 在上一步中创建的项目节点（在customtab下）中，使用以下步骤在自定义选项卡中添加一个用于创建列的节点（此处为Column1）（要添加更多列，请重复此步骤）:

   1. 右键单击项目节点，然后选择“创 **建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：Column1（或要给节点的名称）

      **** 类型：nt:unstructured

   1. 将以下属性添加到节点（此处为Column1），然后单击“全 **部保存”**。

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

1. 对于您创建的每列（如上一步中指定的，在此列1中），使用以下步骤创建一个名为item的节点：

   1. 右键单击相关的列节点（此处为Column1），然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：项目

      **** 类型：nt:unstructured

   1. 单击“ **全部保存”:**

1. 对于创建的每列，在“项目”节点下创建一个节点，用于在用户界面的新选项卡中创建字段。 重复此步骤以在列中创建更多字段：

   1. 右键单击相关节点（此处项目位于Column1下），然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：您选择的名称（此处为GeoLocation）

      **** 类型：nt:unstructured

   1. 将以下属性添加到节点，然后单击“全 **部保存”**。

      | **名称** | **类型** | **值** |
      |---|---|---|
      | fieldLabel | 字符串 | 收件人的位置（或要为字段指定的名称）。 |
      | 名称 | 字符串 | `./extendedproperties/GeoLocation` |
      | renderReadOnly | 布尔型 | true |
      | sling:resourceType | 字符串 | granite/ui/components/coral/foundation/form/textfield |

1. 要查看自定义，请将指针悬停在相关资产（此处为文本）上，单击查看属性，然后单击 **编辑**。 新选项卡和字段（收件人的位置）显示在用户界面中。

   >[!NOTE]
   >
   >在UI中显示自定义之前，您可能需要清除浏览器缓存。

   ![添加到特定资产的自定义属性](assets/newtabui-1.png)

### 在“资产创建”页面上显示自定义属性 {#display-custom-properties-on-the-asset-creation-page}

默认情况下，添加到新选项卡的自定义属性仅在属性页面上可见，而在资产创建页面上不可见，因为资产创建页面没有选项卡布局。 要在资产创建页面上显示自定义属性以及其他属性，您需要执行以下操作：

1. 右键单击以下路径中的项目文件夹，然后选择“叠 **加节点”**:

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 确保“叠加节点”对话框具有以下字母值。 对于其他资产类型，下表中给出了路径：

   **** 路径：/libs/fd/cm/ma/gui/content/createasset/createleter/jcr:content/body/items/form/items/letterWizard/items/properties/properties/items/letterproperties/items

   **** 位置：/apps/

   **** 匹配节点类型：已选择

   根据资产的类型，路径必须包括以下内容：

   | **资产／文档类型** | **要添加的路径** |
   |---|---|
   | 文本 | /libs/fd/cm/gui/content/createasset/createtext/jcr:content/body/items/form/items/textwizard/items/editproperties/properties/items/tabs/items/tab1/items/tab1/items |
   | 列表 | /libs/fd/cm/gui/content/createasset/createlist/jcr:content/body/items/form/items/listwizard/items/editproperties/properties/items/tabs/items/tab1/items/tab1/items |
   | 条件 | /libs/fd/cm/gui/content/createasset/createcondition/jcr:content/body/items/form/orconditionwizard/items/editproperties/items/properties/items/tabs/items/tab1/items/tab1/items |
   | 片段 | /libs/fd/cm/gui/content/createasset/createfragment/jcr:content/body/items/form/items/fragmentwizard/items/properties/properties/items/tabs2/items/tabs2/tab1/items |
   | 书信 | /libs/fd/cm/ma/gui/content/createasset/createleter/jcr:content/body/items/form/items/letterWizard/items/properties/properties/items/letterproperties/items |

1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

1. 在您创建的叠加项目节点下，创建名称为col4的节点（或任何其他名称），然后单击“全 **部保存”**。

   例如，下面是为字母创建的叠加节点。

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 将以下属性添加到新创建的节点（此处为第4列），然后单击“全 **部保存”**:

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
   <td><p>此路径是指向在以下位置创建的列的指针：</p>
    <ul>
     <li>对于所有资产类型的公用选项卡：/apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>对于不同资产类型的不同属性：/apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字符串</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappageinmainproperties](assets/customfieldappearinginmainproperties.png)

自定义属性，语言，显示在用于创建字母的UI中

## 自定义列表视图以显示自定义属性 {#customize-the-list-view-to-show-custom-properties}

在将自定义属性添加到Correporse Management资产后，您需要在CRX/DE中做进一步的更改，以确保自定义属性显示在Correporse Management UI中。

完成以下步骤以在Correponse Management的资产列表UI中显示自定义属性：

1. 转到并 `https://[server]:[port]/[ContextPath]/crx/de` 以管理员身份登录。
1. 在应用程序文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径中的列文件夹，然后选择“叠 **加节点”**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. 确保“叠加节点”对话框具有以下值：

      **** 路径：/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns

      **** 位置：/apps/

      **** 匹配节点类型：已选择

   1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

      单击“ **全部保存**”。

1. 对于创建的每个属性，在列节点下创建一个节点，以在用户界面中创建列。 重复此步骤以在UI中创建更多列：

   1. 右键单击相关节点（列），然后选择“创 **建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：您选择的名称（此处为GeoralicalLocation）

      **** 类型：nt:unstructured

   1. 将以下属性添加到节点，然后单击“全 **部保存”**。

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
           <td><p>true</p> <p>值true表示用户可以对此列中的值进行排序。 </p> </td>
         </tr>
         </tbody>
       </table>

1. 在应用程序文件夹中创建以下文件夹结构：

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   以下是创建此文件夹结构的步骤：

   1. 右键单击以下路径中的列文件夹，然后选择“叠 **加节点”**:

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. 确保“叠加节点”对话框具有以下值：

      **** 路径：/libs/fd/cm/ma/gui/components/admin/childpagerer/childlistpage

      **** 位置：/apps/

      **** 匹配节点类型：已选择

   1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

      单击“ **全部保存**”。

1. 从以下位置复制childlistpage.jsp文件：

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   将文件粘贴到以下位置：

   /apps//fd/cm/ma/gui/components/admin/childpagerer/childlistpage/

1. 打开childlistpage.jsp文件(/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp)并进行以下更改：

   1. 将以下内容添加到文件的第19行（在copyright语句之后）。

      ```
      <%@page import="java.util.Map"%>
      ```

   1. 将获取每个自定义属性值的函数的以下代码添加到文件末尾：

      ```
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

   1. 在&lt;tr>标记(&lt;tr &lt;%= attrs.build()%>>)开始之前添加以下内容：

      ```
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

      在代码中，GeoLocation是您在创建自定义节点／字段时在name属性中设置的值。 在创建自定义节点／字段时，您使用指定了属性的名称。/extendedproperties/前缀：./extendedproperties/GeoLocation。 在代码中，前缀不是必需的。

   1. 要在UI中显示新属性，请在结束tr(&lt;/tr>)标签之前添加一个TD标签：

      ```
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      要添加更多列，请重复步骤6.3和6.4。

   1. 单击“ **全部保存**”。

1. 要查看自定义，请打开文档片段或已在其中添加自定义属性的字母的列表视图。

   此过程中添加的UI列和属性将针对所有资产类型显示。 但是，这些属性中的值只能为最初为其添加自定义属性的资产类型输入和显示。

   例如，使用方案：为特定资产类型添加自定义属性，您可以向文本资产添加自定义属性，您只能为文本资产输入自定义属性。 但是，如果您在UI中显示该自定义属性，则所有资产类型都会显示该列。

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. （可选）默认情况下，新列在UI中显示为最后一列。 要使列显示在特定位置，请向列节点添加以下属性：

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
   <td><p>路径“/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns”的列节点名称，此前需要在UI中显示自定义列。</p> <p>在此，如果希望“地理位置”列显示在“版本”列的前面（左侧），请将属性sling:orderBefore添加到路径“”/apps/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns/GeoLocation”的GeoLocation节点中，并将属性值设置为版本。</p> </td>
  </tr>
 </tbody>
</table>

当您添加sling:orderBefore属性以指定列位置时，您还需要更新在此过程的步骤6.4中指定的相应&lt;td>标记的顺序。 例如，在这种情况下，您需要确保“地理位置”的&lt;td>标签放在“版本”列的&lt;td>标签之前：

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## 启用自定义属性搜索 {#enable-search-for-custom-properties}

默认情况下，全文搜索不包括您使用CRX/DE添加到UI的自定义属性。

要在搜索中包含自定义属性，您需要允许对自定义属性进行索引。

要允许对自定义属性进行索引，请完成以下步骤：

1. 转到并 `https://[server]:[port]/[ContextPath]/crx/de` 以管理员身份登录。
1. 转到并 `/oak:index/cmLucene`在其下添加一个名 **为agges** 的节点。

   1. 右键单击cmLucene文件夹，然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：聚合

      **** 类型：nt:unstructured

   1. 单击“ **全部保存**”。

1. 在新创建的聚合文件夹下，添加一个节点cm:resource。 在cm:resource下，添加一个名为include0的节点。

   1. 右键单击聚合文件夹，然后选择 **创建** >创 **建节点**。 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：cm：资源

      **** 类型：nt:unstructured

   1. 右键单击cm:resource文件夹，然后选择 **创建** > **创建节点**。 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：include 0

      **** 类型：nt:unstructured

   1. 单击您创建的新节点（此处包括0）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处包括0）:

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

   1. 单击“ **全部保存**”。

1. 转到位于以下位置的属性，并在其下添加一个节点位置： `/oak:index/cmLucene/indexRules/cm:resource/properties`

   对要添加到搜索的每个自定义属性重复此步骤。

   1. 右键单击属性文件夹，然后选择“ **创建** ”>“ **创建节点”**。
   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **** 名称：位置（或要添加到搜索的自定义属性的名称）

      **** 类型：nt:unstructured

   1. 单击您创建的新节点（此处）。 CRX显示节点的属性。
   1. 将以下属性添加到节点（此处位置）:

      | **名称** | **类型** | **值** |
      |---|---|---|
      | 分析 | 字符串 | true |
      | 名称 | 字符串 | extendedProperties/location（或要添加到搜索的属性的名称） |
      | propertyIndex | 布尔型 | true |
      | useInSubset | 布尔型 | true |

   1. 单击“ **全部保存**”。

1. 现在，您可以在全文搜索中使用自定义属性值来查找相关资产。

>[!NOTE]
>
>如果您仍无法搜索，则可能是由于索引问题。 要重新编制索引，请转到以下节点，并将属性“re-index”的值更改为true:
>
>/oak:index/cmLucene”和属性的更改值

## 更改搜索页面的默认视图 {#change-default-view-of-the-search-page}

1. 转到并 `https://[server]:[port]/[ContextPath]/crx/de` 以管理员身份登录。
1. 在apps文件夹中，创建一个名为list的文件夹，其路径／结构与位于/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views中的列表文件夹类似：

   1. 右键单击以下路径中的项目文件夹，然后选择“叠 **加节点”**:

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. 确保“叠加节点”对话框具有以下值：

      **** 路径：/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **** 位置：/apps/

      **** 匹配节点类型：已选择

   1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

   1. 单击“ **全部保存**”。

1. 在新创建的节点中，列出，添加以下属性，然后单击“全 **部保存”**:

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

1. 自定义操作会在“列表”视图中显示所有控制台的搜索结果，包括表单和文档、资产和站点。

## 更改资产页面的默认视图 {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>这些步骤更改了所有控制台（如“表单”和“文档”、“资产”和“站点”）的默认视图。

1. 转到并 `https://[server]:[port]/[ContextPath]/crx/de` 以管理员身份登录。
1. 在apps文件夹中，创建一个名为list的文件夹，其路径／结构与位于以下位置的列表文件夹类似：

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/

   1. 右键单击以下路径中的项目文件夹，然后选择“叠 **加节点”**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. 确保“叠加节点”对话框具有以下值：

      **** 路径：/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list

      **** 位置：/apps/

      **** 匹配节点类型：已选择

   1. 单击&#x200B;**确定**。文件夹结构将在apps文件夹中创建。

   1. 单击“ **全部保存**”。

1. 在新创建的节点中，列出，添加以下属性，然后单击“全 **部保存”**:

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

1. 清除浏览器cookies或使用浏览器的隐姓埋名模式查看资产。 默认情况下，资产页面显示在卡布局中。

## 在“资产创建”和“属性”页面上显示／隐藏自定义属性 {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

要显示或隐藏自定义属性，请完成以下步骤：

1. 在自定义属性节点（如地理分配）下，创建一个名为“granite:rendercondition”且类型为“nt:unstructured”的新节点。
1. 将以下属性添加到节点，然后单击“全 **部保存”**:

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

1. 要在资产创建页面上隐藏此属性，请向其添加以下属性，然后单击全 **部保存**:

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

1. 要隐藏资产属性页面上的自定义属性，请向其添加以下属性，然后单击全 **部保存**:

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

   要再次显示这些值，请将属性值重置为或 `false` 删除属性条目。
