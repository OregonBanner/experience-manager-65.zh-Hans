---
title: 通信管理中的自定义特殊字符
description: 了解如何在通信管理中添加自定义特殊字符。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# 通信管理中的自定义特殊字符{#custom-special-characters-in-correspondence-management}

## 概述 {#overview}

通信管理已内置对210个特殊字符的默认支持，您可以轻松插入信件。

例如，可以插入以下特殊字符：

* 货币符号，如€、@和£
* 数学符号，例如∑、√、∂和^
* 标点符号如&quot;和&quot;

您可以在字母中插入特殊字符：

* 在 [文本编辑器](/help/forms/using/document-fragments.md#createtext)
* 在 [通信中的可编辑内联模块](../../forms/using/create-correspondence.md#managecontent)

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

管理员可以通过自定义添加对更多/自定义特殊字符的支持。 本文介绍了如何添加对其他自定义特殊字符的支持。

## 在通信管理中添加或修改对自定义特殊字符的支持 {#creatingfolderstructure}

使用以下步骤添加对自定义特殊字符的支持：

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de` 并以管理员身份登录。
1. 在apps文件夹中，创建一个名为 **[!UICONTROL 特殊字符]** 路径/结构与specialcharacters文件夹（位于libs下的textEditorConfig文件夹中）类似：

   1. 右键单击 **特殊字符** 路径下的文件夹并选择 **覆盖节点**：

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **叠加位置：** /apps/

      **匹配节点类型：** 已选中

      >[!NOTE]
      >
      >请勿更改/libs分支。 您所做的任何更改都可能会丢失，因为每当您：
      >
      >
      >
      >    * 在实例上升级
      >    * 应用热修复程序
      >    * 安装功能包
      >
      >

   1. 单击 **确定** 然后单击 **全部保存**. 在指定的路径中创建specialcharacters文件夹。

      创建叠加后，验证节点结构标记。 在/apps中使用覆盖创建的每个节点都应具有与该节点在/libs中定义的相同的类和属性。 如果/apps位置下的节点结构中缺少任何属性或标记，请将其标记与/libs中的相应节点同步。

1. 确保 **[!UICONTROL textEditorConfig]** 节点具有以下属性和值：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | cmConfigurationType | 字符串 | cmTextEditorConfiguration |
   | cssPath | 字符串 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 右键单击 **[!UICONTROL 特殊字符]** 路径下的文件夹并选择 **创建>子节点** 然后单击 **全部保存**：

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. 刷新文本编辑器\创建通信UI页。 您添加的节点是UI中特殊字符列表的最后一个节点。
1. 单击&#x200B;**全部保存**。
1. 根据需要更改特殊字符：

<table>
 <tbody>
  <tr>
   <td><strong>收件人...</strong></td>
   <td><strong>完成以下步骤</strong></td>
  </tr>
  <tr>
   <td>添加自定义特殊字符</td>
   <td>
    <ol>
     <li>在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下添加具有强制属性的子节点。</li>
     <li>单击全部保存</li>
     <li>刷新文本编辑器\创建通信UI，以便您能够看到所做的更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>更新现有特殊字符的属性</td>
   <td>
    <ol>
     <li>按照上文所述覆盖要更新的节点，并验证标记和类。</li>
     <li>更改任何值，例如caption、value、endValue和multipleCaption。 </li>
     <li>单击全部保存。 </li>
     <li>刷新文本编辑器\创建通信UI，以便您能够看到所做的更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>隐藏特殊字符</td>
   <td>
    <ol>
     <li>覆盖要在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下隐藏的节点</li>
     <li>将sling：hideResource（布尔值）属性添加到节点（在应用程序下）以隐藏。 </li>
     <li>单击全部保存。 </li>
     <li>刷新文本编辑器\创建通信UI，以便您能够看到所做的更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>隐藏多个特殊字符</td>
   <td>
    <ol>
     <li>将属性“sling：hideChildren （String或String[]）”添加到“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”。 </li>
     <li>添加节点名称（要隐藏的特殊字符）作为“sling：hideChildren”属性的值。 </li>
     <li>单击全部保存。 </li>
     <li>刷新文本编辑器\创建通信UI，以便您能够看到所做的更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>排序特殊字符</td>
   <td>
    <ol>
     <li>在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下添加具有强制属性的子节点。 </li>
     <li>将“sling：orderBefore (String)”属性添加到新创建的子节点。 </li>
     <li>将节点名称添加为值，新添加的特殊字符将显示在该值之前。 </li>
     <li>单击全部保存。 </li>
     <li>刷新文本编辑器\创建通信UI，以便您能够看到所做的更改。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
